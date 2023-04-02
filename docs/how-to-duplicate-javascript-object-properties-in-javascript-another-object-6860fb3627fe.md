# 如何在 JavaScript 另一个对象中复制 JavaScript 对象属性？

> 原文：<https://javascript.plainenglish.io/how-to-duplicate-javascript-object-properties-in-javascript-another-object-6860fb3627fe?source=collection_archive---------14----------------------->

![](img/149ea15802721b5c5c9569bc2856a87e.png)

Photo by [Joe Green](https://unsplash.com/@jg?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们经常想要将一个 JavaScript 对象的属性复制到另一个对象中。

在本文中，我们将研究如何在另一个 JavaScript 对象中复制 JavaScript 对象属性。

# 使用 Object.assign 方法

将一个对象的属性复制到另一个对象的一种方法是使用`Object.assign`方法。

例如，我们可以写:

```
const firstObject = {
  a: 1,
  b: 2
}
const secondObject = {
  c: 3
}
Object.assign(secondObject, firstObject);
console.log(secondObject)
```

我们有具有某些属性的`firstObject`和`secondObject`对象。

然后我们调用`Object.assign`将`firstObject`对象的属性复制到`secondObject`中。

因此，从控制台日志中，我们看到`secondObject`是:

```
{c: 3, a: 1, b: 2}
```

之后我们叫`Object.assign`。

如果我们不想修改`secondObject`，我们可以写:

```
const firstObject = {
  a: 1,
  b: 2
}
const secondObject = {
  c: 3
}
const thirdObject = Object.assign({}, firstObject, secondObject)
console.log(thirdObject)
```

那么`thirdObject`就是:

```
{a: 1, b: 2, c: 3}
```

而`secondObject`是未修改的。

# 传播算子

将一个对象的属性复制到另一个对象的另一种方法是使用 spread 运算符。

例如，我们可以写:

```
const firstObject = {
  a: 1,
  b: 2
}
const secondObject = {
  c: 3
}
const thirdObject = {
  ...firstObject,
  ...secondObject
}
console.log(thirdObject)
```

我们创建了一个`thirdObject`对象，它是通过将`firstObject`和`secondObject`的属性扩展到其中而创建的。

因此，`thirdObject`是:

```
{a: 1, b: 2, c: 3}
```

# 结论

我们可以使用`Object.assign`方法或 spread 操作符将属性从一个对象复制到另一个对象上。