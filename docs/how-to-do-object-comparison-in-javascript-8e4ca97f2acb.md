# JavaScript 中如何做对象比较？

> 原文：<https://javascript.plainenglish.io/how-to-do-object-comparison-in-javascript-8e4ca97f2acb?source=collection_archive---------32----------------------->

![](img/b9f1fd49dc865ad129c392bf0b6b3a6a.png)

Photo by [Coffee Geek](https://unsplash.com/@coffeegeek?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

比较对象属性和值是我们在 JavaScript 代码中有时需要做的事情。

在本文中，我们将看看如何在 JavaScript 中比较对象。

# JSON.stringify

`JSON.stringify`方法让我们将 JavaScript 对象转换成 JSON 字符串。

一旦我们将对象转换成字符串，我们就可以将字符串化的值与另一个字符串化的对象进行比较。

例如，我们可以写:

```
const obj1 = {
  a: 1
}
const obj2 = {
  a: 1
}
console.log(JSON.stringify(obj1) === JSON.stringify(obj2))
```

我们有两个对象，`obj1`和`obj2`。

然后我们在两个对象上调用`JSON.stringify`，并用`===`操作符检查是否相等。

属性的顺序很重要，因为它们将按照在对象中的顺序进行字符串化。

由于`obj1`和`obj2`是同一个字符串，那么最后一行的布尔表达式应该是`true`。

# 比较对象的每个属性

我们可以比较我们想要比较的对象的每个属性。

例如，我们可以写:

```
const obj1 = {
  a: 1
}
const obj2 = {
  a: 1
}function objectEquals(x, y) {
  if (x === y) {
    return true;
  } if (!(x instanceof Object) || !(y instanceof Object)) {
    return false;
  } if (x.constructor !== y.constructor) {
    return false;
  } for (const p in x) {
    if (!x.hasOwnProperty(p)) {
      continue;
    } if (!y.hasOwnProperty(p)) {
      return false;
    } if (x[p] === y[p]) {
      continue;
    } if (typeof(x[p]) !== "object") {
      return false;
    } if (!objectEquals(x[p], y[p])) {
      return false;
    }
  } for (const p in y) {
    if (y.hasOwnProperty(p) && !x.hasOwnProperty(p)) {
      return false;
    }
  }
  return true;
}console.log(objectEquals(obj1, obj2))
```

在`objectEquals`函数中，我们检查`x`和`y`是否与`===`运算符相等。

如果它们相等，那么我们返回`true`。

下一个`if`块用`instanceof`操作符检查它们是否不是一个对象文字。

如果它们中的任何一个都不是，那么我们返回`false`,因为如果它们中的任何一个都不是对象，它们就不可能是相同的。

接下来，我们遍历`x`的属性。

如果属性`p`不是`x`的自有属性，那么我们用`continue`忽略它。

如果`y`在`x`中没有继承的属性，那么它们就不一样，所以我们返回`false`。

如果`x[p]`和`y[p]`相同，则使用`continue`检查新属性。

如果`x[p]`不是一个对象，我们返回`false`，因为如果一个原始值不相等，那么`x`和`y`不可能相等。

然后我们还必须记得检查剩余的`x`和`y`的电平是否与`objectEquals(x[p], y[p])`相等。

如果它们中的任何一个不相等，那么我们返回`false`。

接下来，我们遍历`y`，检查`y`中是否有`x`中没有的非继承属性。

如果有，那么我们知道它们不相等，我们返回`false`。

如果所有检查都通过了，那么我们返回`true`，因为我们知道在这种情况下它们肯定是相等的。

# 结论

我们可以编写自己的代码来比较复杂的对象，或者我们可以使用`JSON.stringify`来比较 JSON 字符串形式的 2 个对象。

*更多内容请看*[***plain English . io***](http://plainenglish.io)