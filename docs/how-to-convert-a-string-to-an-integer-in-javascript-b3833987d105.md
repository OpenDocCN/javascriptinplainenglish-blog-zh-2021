# 如何在 JavaScript 中将字符串转换成整数？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-string-to-an-integer-in-javascript-b3833987d105?source=collection_archive---------15----------------------->

![](img/135adacdfb5af5ca73be1e8f3efe93e5.png)

Photo by [Sticker Mule](https://unsplash.com/@stickermule?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中把一个字符串转换成一个整数是我们有时不得不做的事情。

在本文中，我们将看看如何用 JavaScript 将字符串转换成整数。

# 数字函数

我们可以使用 tyhe `Number`函数将整数字符串转换成整数。

例如，我们可以写:

```
const num = Number("1000")
console.log(num)
```

那么`num`就是 1000。

# **parse int 函数**

`parseInt`函数也让我们将一个整数字符串转换成一个整数。

它分别接受我们要转换的数字的字符串和基数。

例如，我们可以写:

```
const num = parseInt("1000", 10);
console.log(num)
```

然后我们得到和上一个例子一样的结果。

# 一元加运算符

一元加号运算符也将字符串转换为整数。

所以我们可以把+运算符放在整数前面，把它转换成数字。

例如，我们可以写:

```
const num = +"1000"
console.log(num)
```

得到同样的结果。

# `Math.floor`

`Math.floor`方法将一个数字向下舍入到最接近的整数。

它还接受一个数字字符串，所以我们可以将它传递给`Math.floor`方法，它将返回四舍五入到最接近的整数。

例如，我们可以写:

```
const num = Math.floor("1000.05")
console.log(num)
```

我们得到`num`是 1000。

# `Math.round`

`Math.round`方法也可以让我们四舍五入一个数字。

舍入的规则是，如果参数的小数部分大于 0.5，则参数将被舍入到绝对值下一个最大的整数。

否则，它将被舍入到绝对值较低的最接近的整数。

它也接受一个字符串，并在舍入前转换成一个数字。

例如，我们可以写:

```
const num = Math.round("1000.05")
console.log(num)
```

# **parse float 函数**

`parseFloat`函数让我们将浮点数串转换成数字。

它还可以将整数字符串转换成整数。

例如，我们可以写:

```
const num = parseFloat("1000")
console.log(num)
```

# 结论

用 JavaScript 将整数字符串转换成整数的方法有很多。

*更多内容看* [***说白了. io***](http://plainenglish.io)