# 使用 Firestore 和更多类型脚本

> 原文：<https://javascript.plainenglish.io/using-firestore-with-more-typescript-8058b6a88674?source=collection_archive---------1----------------------->

## 用这个验证点符号对象键的 TS 4 魔术来升级你的 Firestore/TypeScript 游戏。

![](img/c6a5510a8978557384ebf8c04948f87c.png)

Photo by [Peter Conlan](https://unsplash.com/@peterconlan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 如果您想理解代码，请注意:

这篇文章是我上一篇关于 Firestore 和 TS 的文章的延续

[](https://medium.com/swlh/using-firestore-with-typescript-65bd2a602945) [## 将 Firestore 与 Typescript 一起使用

### 用几行干净的代码提升你的 Firestore 和 TS 技能。

medium.com](https://medium.com/swlh/using-firestore-with-typescript-65bd2a602945) 

我写`db`的时候，假设你知道我在说什么。以下是提醒代码:

```
// import firstore (obviously)
import { firestore } from "firebase-admin"// Import or define your types
// import { User } from '~/@types'const converter = <T>() => ({
  toFirestore: (data: Partial<T>) => data,
  fromFirestore: (snap: FirebaseFirestore.QueryDocumentSnapshot) => snap.data() as T
})const dataPoint = <T>(collectionPath: string) => firestore().collection(collectionPath).withConverter(converter<T>())const db = {
  // list your collections here
  // users: dataPoint<User>('users')
}export { db }
```

**TLDR**；
TS 游乐场的类型安全 Firestore 更新:
[https://bit.ly/2OhV1y4](https://bit.ly/2OhV1y4)
代码完整要旨:
[https://GIST . github . com/Jamie curnow/650 ea 759 c 277757 AE 5665 ea 52400713 b](https://gist.github.com/JamieCurnow/650ea759c277757ae5665ea52400713b)

# 问题是:

几个月来，我一直在使用我的另一篇文章中的代码(上面有链接),它在我读写 Firestore 时为我提供了可爱的类型安全和建议。然而，它有一个缺点:T1 方法。

Firestore 的`documentRef.update()`方法在不覆盖整个文档的情况下更新文档的一些字段，类似于做`set({}, { merge: true })`，但是有一个巧妙的技巧——使用点符号来更新嵌套属性。

以这个数据结构为例:

```
interface User {
  name: string
  email: string
  address: {
    line1: string
    line2: string
    postcode: string
    verified: false
    timeAtAddress: {
      days: string
      months: string
      hours: string
    }
  }
}
```

如果我们只想更新`user.adress.verified`，但保持地址对象的所有其他值不变，该怎么办？

**这将删除地址中的所有其他关键字:**

```
db.users.doc('1234').set({
  address: {
    verified: true
  }
})
// it would also throw a TS error because it's not a complete User
```

即使使用`merge: true`，地址中的所有**其他键也会被删除**:

```
db.users.doc('1234').set({
  address: {
    verified: true
  }
}, { merge: true })
```

这是因为`merge`选项没有深入执行合并。

这就是方便的`update`函数的用武之地。当您调用`update()`时，您可以使用“点符号”来引用文档中的嵌套字段:

```
db.users.doc('1234').update({
  ['address.verified']: true
})
```

使用 TypeScript 时只有一个问题…传递给`@google-cloud/firestore`中的 update 函数的单个参数的签名是这样的:

```
export type UpdateData = {[fieldPath: string]: any};
```

所以在实践中，我们可以将任何对象传递给`update()`函数，TypeScript 会很高兴。然后，我们有坏的数据挂在周围，没有类型安全时，我们写的对象！检查一下:

```
db.users.doc('1234').update({
  ['address.unkownKey']: true
  notName: 'Jamie'
})
// No Type errors at all!
```

所以我首先创建了一个`updates`对象，它被类型化以存储我的更新，但是这不适用于点符号键:

```
const updates: Partial<User> = {
  name: 'Jamie',
  notName: 'Jamie' // Type Error - Great!
  ['address.verified']: true // Type Error - Oh no!
}
db.users.doc('1234').update(updates)
```

# 解决方案是:

我考虑这个问题已经有一段时间了，并尝试过几次编写一些神奇的类型脚本，这些脚本将只强制已知的键，并为点符号键更正值。然后我在推特上找到了@diegohaz 的这个小片段:

```
type PathImpl<T, Key extends keyof T> =
  Key extends string
  ? T[Key] extends Record<string, any>
    ? | `${Key}.${PathImpl<T[Key], Exclude<keyof T[Key], keyof any[]>> & string}`
      | `${Key}.${Exclude<keyof T[Key], keyof any[]> & string}`
    : never
  : never;type PathImpl2<T> = PathImpl<T, keyof T> | keyof T;type Path<T> = PathImpl2<T> extends string | keyof T ? PathImpl2<T> : keyof T;type PathValue<T, P extends Path<T>> =
  P extends `${infer Key}.${infer Rest}`
  ? Key extends keyof T
    ? Rest extends Path<T[Key]>
      ? PathValue<T[Key], Rest>
      : never
    : never
  : P extends keyof T
    ? T[P]
    : never;
```

# 多传奇啊！

我很快将它扩展到 firebase 更新中，效果非常好:

```
type PathImpl<T, K extends keyof T> =
  K extends string
  ? T[K] extends Record<string, any>
  ? T[K] extends ArrayLike<any>
  ? K | `${K}.${PathImpl<T[K], Exclude<keyof T[K], keyof any[]>>}`
  : K | `${K}.${PathImpl<T[K], keyof T[K]>}`
  : K
  : nevertype Path<T> = PathImpl<T, keyof T> | keyof Ttype PathValue<T, P extends Path<T>> =
  P extends `${infer K}.${infer Rest}`
  ? K extends keyof T
  ? Rest extends Path<T[K]>
  ? PathValue<T[K], Rest>
  : never
  : never
  : P extends keyof T
  ? T[P]
  : nevertype UpdateData<T extends object> = Partial<{
  [TKey in Path<T>]: PathValue<T, TKey>
}>const updates: UpdateData<User> = {
  name: 'Jamie',
  'address.verified': true,
  notName: 'Jamie' // TS Error. Great!
  'address.unkownKey': false // TS Error. Fantastic :)
}db.users.doc('1234').update(updates)
```

我把这些类型保存在我的助手中，这样当我在应用程序中使用它们的时候，它会变得很好很干净。下面是一些完整的代码:

```
// utils/firestore-helpers.ts// import firstore (obviously)
import { firestore } from "firebase-admin"// Make the helper types for updates:
type PathImpl<T, K extends keyof T> =
  K extends string
  ? T[K] extends Record<string, any>
  ? T[K] extends ArrayLike<any>
  ? K | `${K}.${PathImpl<T[K], Exclude<keyof T[K], keyof any[]>>}`
  : K | `${K}.${PathImpl<T[K], keyof T[K]>}`
  : K
  : nevertype Path<T> = PathImpl<T, keyof T> | keyof Ttype PathValue<T, P extends Path<T>> =
  P extends `${infer K}.${infer Rest}`
  ? K extends keyof T
  ? Rest extends Path<T[K]>
  ? PathValue<T[K], Rest>
  : never
  : never
  : P extends keyof T
  ? T[P]
  : neverexport type UpdateData<T extends object> = Partial<{
  [TKey in Path<T>]: PathValue<T, TKey>
}>// Import or define your types
import { User } from '~/@types'const converter = <T>() => ({
  toFirestore: (data: Partial<T>) => data,
  fromFirestore: (snap: FirebaseFirestore.QueryDocumentSnapshot) => snap.data() as T
})const dataPoint = <T>(collectionPath: string) => firestore().collection(collectionPath).withConverter(converter<T>())const db = {
  // list your collections here
  // users: dataPoint<YourType>('users')
}export { db }// some-other-file.ts
import { db, UpdateData } from '~/utils/firestore-helpers.ts'
import { User } from '~/@types'export const verifyUserAddress = async (userId: string) => {
  // Make the updates object
  const updates: UpdateData<User> = {
    'address.verified': true
  }

  // do the update!
  await db.users.doc(userId).update(updates)
}
```

如果 Firestore 团队能够将这种新类型集成到 SDK 中，以便在使用`withConverter`技巧时自动进行更新，那就太好了。我已经查看了源代码，这很容易实现，但是需要他们从 3.8.3 更新到 TS ≥4.1，这可能会非常麻烦，需要大量的工作…我已经向他们提出了一个问题，请关注这个空间！https://github.com/googleapis/nodejs-firestore/issues/1448
T3

感谢阅读！

# 支持你的创作者！

如果你觉得这个故事有用，并希望我继续写有用的内容，请考虑在 [Patreon](https://www.patreon.com/jamiecurnow) 上支持我🤗

[](https://www.patreon.com/jamiecurnow) [## Jamie Curnow 正在开发软件| Patreon

### 今天就成为 Jamie Curnow 的赞助人:在世界上最大的…

www.patreon.com](https://www.patreon.com/jamiecurnow)