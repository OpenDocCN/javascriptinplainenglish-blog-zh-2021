# 如何在 JavaScript 中检查数组是否包含值

> 原文：<https://javascript.plainenglish.io/how-to-check-if-an-array-includes-a-value-in-javascript-488f265ef03?source=collection_archive---------19----------------------->

![](img/f6d2b2d3a33038bcae66ab7b3d99d766.png)

Photo by [Tiko Giorgadze](https://unsplash.com/@domenika?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

检查数组是否包含值是我们在 JavaScript 应用程序中经常要做的事情。

在本文中，我们将看看如何在 JavaScript 中检查数组是否包含给定值。

# 数组.原型.包含

`includes`方法是包含在数组实例中的一个方法。

它获取一个值，并将其与`===`进行比较，以检查是否包含一个元素。

例如，我们可以写:

```
console.log(['apple', 'orange', 'grape'].includes('orange'));
```

如果包含，那么它返回`true`。

否则返回`false`。

# Array .原型. indexOf

我们还可以使用数组实例的`indexOf`方法来检查它是否包含给定的元素。

它还使用`===`进行比较。

并且它返回一个项目的第一个实例的索引，如果它存在的话。

否则，它返回-1。

为了使用它，我们写:

```
console.log(['apple', 'orange', 'grape'].indexOf('orange') >= 0);
```

# 写我们自己的

我们可以编写自己的函数来搜索一个值。

例如，我们可以写:

```
function contains(a, obj) {
  let i = a.length;
  while (i--) {
    if (a[i] === obj) {
      return true;
    }
  }
  return false;
}console.log(contains(['apple', 'orange', 'grape'] , 'orange'));
```

我们创建了`contains`函数，它使用一个`while`循环来搜索一个项目。

如果`a[i]`与`obj`具有相同的值，那么我们返回`true`。

如果我们遍历整个`a`数组，没有找到任何匹配的内容，那么我们返回`false`。

# 数组.原型.一些

`some`方法是 JavaScript 数组附带的另一个数组实例方法。

它让我们传入一个回调函数来检查是否有任何条目匹配给定的条件。

例如，我们可以写:

```
const items = [{
  a: '1'
}, {
  a: '2'
}, {
  a: '3'
}]console.log(items.some(item => item.a === '3'))
```

我们有一个包含一堆对象的`items`数组。

我们用回调函数调用`items.some`来检查是否存在任何`a`属性等于 3 的`items`条目。

`some`如果存在符合给定条件的项目，则返回`true`，否则返回`false`。

# 结论

有很多方法可以发现 JavaScript 中是否存在数组项。

*更多内容尽在* [***说白了***](http://plainenglish.io)