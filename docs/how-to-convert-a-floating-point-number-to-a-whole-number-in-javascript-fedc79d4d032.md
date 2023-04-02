# 如何在 JavaScript 中将浮点数转换成整数？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-floating-point-number-to-a-whole-number-in-javascript-fedc79d4d032?source=collection_archive---------15----------------------->

![](img/6e77f1b822e6e6ce5696d5f2b069a5af.png)

Photo by [Robson Hatsukami Morgan](https://unsplash.com/@robsonhmorgan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 应用程序中，有时我们必须将浮点数转换成整数。

在本文中，我们将研究如何将 JavaScript 浮点数转换成整数。

# `Math.floor`

`Math.floor`方法让我们将一个数字向下舍入到最接近的整数。

例如，我们可以这样使用它:

```
const intvalue = Math.floor(123.45);
console.log(intvalue)
```

然后我们得到 123 作为`intValue`的值。

# `Math.ceil`

`Math.ceil`方法让我们将一个数字向上舍入到最接近的整数。

例如，我们可以写:

```
const intvalue = Math.ceil(123.45);
console.log(intvalue)
```

那么`intValue`就是 124。

# `Math.round`

如果第一个十进制数字是 4 或更小，那么`Math.round`方法让我们将一个数字向下舍入到最接近的整数。

否则，它会将数字向上舍入到最接近的整数。

例如，如果我们有:

```
const intvalue = Math.round(123.45);
console.log(intvalue)
```

那么`intValue`就是 123。

# `Math.trunc`

`Math.trunc`方法让我们通过移除小数来返回数字的整数部分。

例如，我们可以写:

```
const intvalue = Math.trunc(123.45);
console.log(intvalue)
```

那么`intValue`就是 123。

# `parseInt`

`parseInt`函数让我们将浮点数转换成整数。

它像`Math.trunc`一样工作，从返回的数字中删除小数。

例如，我们可以写:

```
const intvalue = parseInt(123.45);
console.log(intvalue)
```

而`intValue`是 123。

为了确保我们返回一个十进制数，我们将 10 传递给第二个参数:

```
const intvalue = parseInt(123.45, 10);
console.log(intvalue)
```

# 结论

JavaScript 提供了一些函数和方法让我们将浮点数转换成整数。