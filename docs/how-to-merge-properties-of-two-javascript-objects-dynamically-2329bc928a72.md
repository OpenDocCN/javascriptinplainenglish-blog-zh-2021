# 如何动态合并两个 JavaScript 对象的属性

> 原文：<https://javascript.plainenglish.io/how-to-merge-properties-of-two-javascript-objects-dynamically-2329bc928a72?source=collection_archive---------14----------------------->

![](img/a8f05b612fdc02173ad9e4b0dfee5df5.png)

Photo by [Sebastian Schuppik](https://unsplash.com/@supa_95?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 对象具有动态属性。

这意味着我们可以动态合并两个 JavaScript 对象的属性。

这是一个经常做的手术。

在本文中，我们将看看如何动态合并两个 JavaScript 对象的属性。

# 传播算子

从 ES2018 开始，扩展操作符可用于对象。

它让我们可以轻松地将两个对象的属性合并在一起。

例如，我们可以写:

```
const obj1 = {
  a: 1
}
const obj2 = {
  b: 2
}
const merged = {
  ...obj1,
  ...obj2
};
```

扩展操作符是 3 个点。

它按照写入的顺序从`obj1`和`obj2`复制属性。

因此，`merged`就是`{a: 1, b: 2}`。

如果两个对象具有相同的属性，则最后一个合并的对象的值会覆盖之前的值。

例如，如果我们有:

```
const obj1 = {
  a: 1
}
const obj2 = {
  a: 2
}
const merged = {
  ...obj1,
  ...obj2
};
```

那么`merged`就是`{a: 2}`。

# 对象.分配

`Object.assign`方法还让我们将两个对象组合在一起，并返回一个合并的对象作为结果。

例如，我们可以写:

```
const obj1 = {
  a: 1
}
const obj2 = {
  b: 2
}
const merged = Object.assign(obj1, obj2);
```

那么`merged`就是`{a: 1, b: 2}`。

第一个论点中的对象是突变。

因此，如果我们想返回一个具有两个对象属性的新对象，而不改变它们，我们传入一个空数组作为第一个参数:

```
const obj1 = {
  a: 1
}
const obj2 = {
  b: 2
}
const merged = Object.assign({}, obj1, obj2);
```

`Object.assign`从 ES6 开始提供

# for-in 循环

如果以上两种方法都不可用，那么我们可以使用`for-in`循环作为最后的手段。

这是绝对不推荐的，因为上面的两个选项已经存在好几年了。

而且它们更加简单易用。

但是如果我们需要使用`for-in`循环，我们写:

```
const obj1 = {
  a: 1
}
const obj2 = {
  b: 2
}const merged = {}
for (const prop in obj1) {
  merged[prop] = obj1[prop];
}for (const prop in obj2) {
  merged[prop] = obj2[prop];
}
```

我们用`for-in`循环遍历`obj1`和`obj2`的所有属性，并将所有属性值放入`merged`对象。

`prop`有属性名。

所以`merged`是:

```
{a: 1, b: 2}
```

# 结论

我们可以使用扩展操作符和`Object.assign`将不同对象的属性合并到一个对象中。

*更多内容请看*[***plain English . io***](http://plainenglish.io)