# 如何用 JavaScript 对整数数组进行正确排序？

> 原文：<https://javascript.plainenglish.io/how-to-sort-an-array-of-integers-correctly-with-javascript-1c33e693151f?source=collection_archive---------5----------------------->

![](img/d71d8bb9c70b5c894243a431e998aac3.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

对整数数组进行排序是我们在 JavaScript 应用程序中经常遇到的事情。

在本文中，我们将看看如何在我们的 JavaScript 应用程序中对整数数组进行正确排序。

# 数组.原型.排序

`sort`方法让我们通过传递一个比较器函数来对数组进行排序。

为了用它来排序数字，我们写:

```
const arr = [4, 2, 1, 3]
const sorted = arr.sort((a, b) => a - b);
console.log(sorted)
```

进行升序排序。

所以`sorted`就是`[1, 2, 3, 4]`。

如果回调的返回值是正的，那么数字将被交换，所以我们将它们按升序排序。

要按降序排序，我们只需在返回的表达式中交换`a`和`b`:

```
const arr = [4, 2, 1, 3]
const sorted = arr.sort((a, b) => b - a);
console.log(sorted)
```

我们必须在回调中使用`sort`，这样我们就可以比较这些数字。

那么`sorted`就是`[4, 3, 2, 1]`。

如果我们没有传入回调，那么`sort`假设我们正在对字符串进行排序。

它会尝试按字母顺序对项目进行排序。

如果参数是负数，我们可以使用`Math.sign`返回-1，如果参数是 0，返回 0，如果参数是正数，返回 1。

所以我们可以写:

```
const arr = [4, 2, 1, 3]
const sorted = arr.sort((a, b) => Math.sign(a - b));
console.log(sorted)
```

按升序排序。

并且:

```
const arr = [4, 2, 1, 3]
const sorted = arr.sort((a, b) => Math.sign(b - a));
console.log(sorted)
```

按降序排序。

# 结论

为了用数字正确地排序一个 JavaScript 数组，如果我们使用`sort`，我们应该传入一个比较器函数来比较数字。

否则，它会假设我们在对字符串进行排序，并尝试按字母顺序对条目进行排序。

*更多内容请看*[***plain English . io***](http://plainenglish.io)