# 如何在 JavaScript 中格式化一个浮点数？

> 原文：<https://javascript.plainenglish.io/how-to-format-a-floating-point-number-in-javascript-aae4890bba33?source=collection_archive---------11----------------------->

![](img/dd62988be62b78709c0194a44561c102.png)

Photo by [Erik Mclean](https://unsplash.com/@introspectivedsgn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

通常，我们不得不在 JavaScript 中将浮点数格式化成我们想要的格式。

在本文中，我们将看看如何用 JavaScript 将浮点数格式化成我们想要的格式。

# `Math.round`

我们可以使用`Math.round`通过将原始数字 10 乘以我们想要舍入到的小数位数的幂，将一个数字舍入到我们想要的小数位数。

然后我们将这个数字传入`Math.round`，我们将舍入后的数字除以与原始数字相乘的数字。

例如，我们可以写:

```
const original = 123.456
const result = Math.round(original * 100) / 100;
console.log(result)
```

我们把`original`乘以 100，也就是 10 的 2 次方。

所以我们四舍五入到小数点后两位。

我们除以 100。

那么`result`就是 123.46。

如果我们也四舍五入到其他小数位数，这也是可行的。

例如，我们可以写:

```
const original = 123.45678
const result = Math.round(original * 1000) / 1000;
console.log(result)
```

而`result`是 123.457。

# Number.prototype. `toFixed`

我们可以调用`toFixed`方法来返回一个字符串，其中的数字四舍五入到给定的小数位数。

例如，我们可以写:

```
const original = 123.45678
const result = original.toFixed(3)
console.log(result)
```

那么`result`就是`‘123.457’`。

3 是要舍入到的小数位数。

`result`是一个字符串，而不是上例中的数字。

这是将数字格式化为我们想要的小数位数的更简单的方法。

# 结论

我们可以用`Math.round`或 number 的`toFixed`方法将浮点数格式化成我们想要的小数位数。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)