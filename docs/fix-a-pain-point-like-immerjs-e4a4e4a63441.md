# 如何使用 ImmerJS 修复软件开发痛点

> 原文：<https://javascript.plainenglish.io/fix-a-pain-point-like-immerjs-e4a4e4a63441?source=collection_archive---------8----------------------->

*只需修改当前树* [*Immer*](https://github.com/immerjs/immer) *即可创建下一棵不可变状态树。*

软件都是为了减少人们的痛点。我们可以看到软件使我们周围的生活变得比以前更容易。

但是软件开发者的痛点呢？

有时，一个出色的抽象会得到软件开发人员的喜爱。

[ImmerJS](https://immerjs.github.io/immer/) 就是其中之一。Immer 是 2019 年“年度突破”React 开源奖和“最具影响力贡献”JavaScript 开源奖的'*获得者。*'

![](img/b741e00c809e2fa04d8468dc74f26f2f.png)

Photo by [Kari Shea](https://unsplash.com/@karishea?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 痛点

不变性是一个增加代码库整体健壮性的概念。但是它有它的痛点。

看看可变和不可变数据结构之间的例子。

```
const user  = {
  name: 'John Doe',
  likes: 45,
}user.likes = user.likes + 1
```

相对

```
const user  = {
  name: 'John Doe',
  likes: 45,
}const updatedLikes = user.likes+1
const updatedUser = {
  ...user,
  likes: updatedLikes
}console.log(user, updatedUser)
```

我们包装了一个携带突变的新物体。

随着对象的大小和复杂性的增加，上面的例子会变得复杂。

如果您需要快速了解不变性，可以看看下面的文章。

[](https://karthickragavendran.medium.com/understanding-immutability-d00ed097e020) [## 理解不变性

### 在面向对象和函数式编程中，不可变对象是这样一种对象，它的状态在它…

karthickragavendran.medium.com](https://karthickragavendran.medium.com/understanding-immutability-d00ed097e020) 

## 不可变的. js

Immutable.js 提出了一个解决方案。

不可变的. js 提供了我们可以安全使用的数据结构，而不是像上面的例子那样使用 JavaScript 对象文字并重新创建一个对象。

```
const { **Map** } = require('immutable');const **user** = Map({ name: 'John Doe', likes: 45, });
const **updatedUser** = **user**.set('likes', user.get('likes')+1);user.get('likes') + ' vs. ' + updatedUser.get('likes'); 
// 45 vs. 46
```

即使`user`对象变得太复杂，方法也会很简单。

这些由 Immutable.js 给出的数据结构被 ***优化*** 以提高性能，就像实现开箱即用的结构共享一样。

## ImmerJS:鱼和熊掌不可兼得。

如果我们可以使用默认的 JavaScript 数据结构，并以更简单的方式执行更新，会怎么样？

ImmerJS 带着一个函数`produce`出现了。它的工作原理如下:

```
cosnt updatedObj = produce(obj, draft => {
  /* update the draft in a mutable way. */
})
```

produce 函数有两个参数

*   **状态**需要更新。
*   一个**回调**提供一个**草稿版本**的状态。我们可以修改 draft 对象，就好像它是可变的一样，ImmerJS 会相应地生成一个新对象。

现在，用 ImmerJS 看同一个例子。

```
const { **produce** } = require( "immer")const user = { name: 'John Doe', likes: 45, }const updatedLikes = user.likes+1
const updatedUser = produce(user, **draft => {
  draft.likes = updatedLikes
}**)console.log(user, updatedUser)
```

这有多简单？

我们也不需要知道对象的完整结构来处理它。上面的例子知道对象有`likes`属性，它需要被更新。我们不关心物体的其他部分。

ImmerJS 利用[结构共享](http://raganwald.com/2019/01/14/structural-sharing-and-copy-on-write.html)，一种 [*写时复制*](https://en.wikipedia.org/wiki/Copy-on-write) 机制，结合 [JavaScript 代理](https://hackernoon.com/introducing-javascript-es6-proxies-1327419ab413)使用。

## 实际应用

函数式编程中的 reducer 模式接受一个状态和动作，并返回更新后的状态。

还原器曾经是使用 redux 的难点。它也容易出错。如果我们重新创建一个复杂的对象，包括一个小的变化。

看看典型减速器的例子。

**不带浸没的减速器:**

Reducer without immer

我们需要使用 spread 操作符从头开始重新组织状态对象，以返回一个新的实例。

**与 ImmerJS 相同的减速器:**

现在已经大大简化了。这就是 ImmerJS。

谢谢你。下次见。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)