# 如何将两个 JavaScript 数组连接或组合成一个数组？

> 原文：<https://javascript.plainenglish.io/how-to-join-or-combine-two-javascript-arrays-by-concatenating-them-into-one-array-5bfdd0c8a5d1?source=collection_archive---------6----------------------->

![](img/0cc848e78233b3c93b3ad05de4eb1ebc.png)

Photo by [Sarah Elisabeth](https://unsplash.com/@sarah_elisabeth?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望将两个 JavaScript 数组连接成一个数组。

在本文中，我们将看看如何通过将两个 JavaScript 数组连接成一个数组来连接或组合它们。

# 使用 Array.prototype.concat 方法

将两个 JavaScript 数组连接成一个数组的一种方法是使用 Javascript 数组的`concat`方法。

例如，我们可以写:

```
const a = ['a', 'b', 'c'];
const b = ['d', 'e', 'f'];
const c = a.concat(b);
console.log(c)
```

我们调用`a.concat(b)`将`b`的条目添加到`a`的条目之后，并返回包含所有条目的新数组。

因此，`c`是:

```
["a", "b", "c", "d", "e", "f"]
```

# 使用扩展运算符

将两个数组连接在一起的另一种方法是使用 spread 运算符。

例如，我们可以写:

```
const a = ['a', 'b', 'c'];
const b = ['d', 'e', 'f'];
const c = [...a, ...b]
console.log(c)
```

我们将`a`和`b`的条目分散到一个新的数组中，形成`c`数组。

它们将按照列出的顺序展开。

因此，`c`现在是:

```
["a", "b", "c", "d", "e", "f"]
```

# 结论

我们可以使用 JavaScript 数组的`concat`方法或 spread 操作符将两个 JavaScript 数组连接在一起。

*更多内容请看*[***plain English . io***](http://plainenglish.io)