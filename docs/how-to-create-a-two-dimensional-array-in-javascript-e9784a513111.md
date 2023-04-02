# 如何用 JavaScript 创建一个二维数组？

> 原文：<https://javascript.plainenglish.io/how-to-create-a-two-dimensional-array-in-javascript-e9784a513111?source=collection_archive---------9----------------------->

![](img/7737eaee6f4a253edab10d7883813f4d.png)

Photo by [Stephen G](https://unsplash.com/@morningz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时我们不得不在 JavaScript 应用程序中创建一个二维数组。

在本文中，我们将看看如何用 JavaScript 创建二维数组。

# 嵌套数组

在 JavaScript 中，二维数组只是嵌套数组。

例如，我们可以写:

```
const arr = [
  [1, 2],
  [3, 4],
  [5, 6]
];
console.log(arr[0][0]);
console.log(arr[0][1]);
console.log(arr[1][0]);
console.log(arr[1][1]);
console.log(arr);
```

数组中有数组。

然后我们可以用方括号访问嵌套的项目。

第一个控制台日志记录 1。

第二个控制台日志记录 2。

第三控制台日志记录 3。

最后一个控制台日志记录 4。

# 创建一个空的二维数组

为了创建一个空的二维数组，我们可以使用`Array.from`和`Array`构造函数。

例如，我们可以写:

```
const arr = Array.from(Array(2), () => new Array(4))
console.log(arr);
```

`Array.from`方法让我们从另一个数组创建一个数组。

第一个参数是我们要从中派生新数组的数组。

第二个参数是一个函数，它将第一个数组中的值映射到我们想要的值。

我们返回一个包含 4 项的数组。

因此，我们得到一个 2×4 的二维数组。

同样，我们可以只用`Array`函数创建一个二维数组。

例如，我们可以写:

```
const arr = Array(2).fill().map(() => Array(4));
console.log(arr);
```

我们调用`fill`方法来填充空槽。

这样，我们可以调用`map`并在`map`回调中返回数组来创建二维数组。

# 结论

我们可以通过嵌套数组文字来创建 JavaScript 二维数组。

同样，我们可以用`Array`函数创建二维数组。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)