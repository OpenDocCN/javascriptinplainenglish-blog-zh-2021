# 如何检查一个 JavaScript 字符串是否有数字？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-javascript-string-has-a-number-f111e818a82b?source=collection_archive---------12----------------------->

![](img/bafb5dbd0dde310e65cb4c2c5cb2f11f.png)

Photo by [Sarra Marzguioui](https://unsplash.com/@geist?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

检查一个 JavaScript 字符串是否是一个数字是我们经常要做的事情。

在本文中，我们将看看如何检查一个 JavaScript 字符串是否是一个有效的数字。

# 编写我们自己的函数

我们可以编写自己的函数来检查一个字符串是否是数字字符串。

例如，我们可以写:

```
const isNumeric = (str) => {
  if (typeof str !== "string") return false
  return !isNaN(str) &&
    !isNaN(parseFloat(str))
}console.log(isNumeric('123'))
console.log(isNumeric('abc'))
```

首先，我们用`typeof`操作符检查`str`是否是一个字符串。

这确保了我们检查的是一个字符串，而不是其他东西。

然后我们调用`isNaN`,看看我们是否能把它转换成一个数字，然后检查转换后的值是否是一个数字。

如果`isNaN`返回`false`，那么我们知道它很有可能是一个数字。

但是，如果字符串以数字开头，它也可以只取字符串的数字部分，然后将其转换为数字。

因此，我们还需要调用`parseFloat`将字符串解析成数字，以确保整个字符串都是数字。

然后我们可以对`isNaN`进行同样的检查，以确保`parseFloat`不会返回`NaN`。

因此，第一个控制台日志应该记录`true`。

第二个控制台日志应该记录`false`。

# 一元加运算符

我们还可以使用一元加号运算符将字符串转换为数字。

为此，我们写道:

```
console.log(+'123')
console.log(+'123abc')
```

第一个控制台日志日志 123

第二控制台日志记录`NaN`。

唯一的问题是空字符串用一元加号运算符转换为 0。

# `parseInt`

我们可以用`parseInt`把整数串转换成整数。

例如，我们可以写:

```
console.log(parseInt('123'))
console.log(parseInt('123abc'))
```

它们都记录 123，因为如果字符串以一个数字开始，那么`parseInt`将获取该字符串的数字部分，并将其转换为一个数字。

但是字符串不是以数字开头，那么它返回`NaN`。

# `parseFloat`

我们可以使用`parseFloat`方法将带有十进制数字的字符串转换成数字。

例如，我们可以写:

```
console.log(parseFloat('123.45'))
console.log(parseFloat('123.45abc'))
```

它们都记录 123.45，因为它也接受字符串的数字部分，如果字符串以数字开头，则尝试将其转换为数字。

但是字符串不是以数字开头，那么它也返回`NaN`。

# 正则表达式检查

因为我们处理的是字符串，所以我们也可以使用正则表达式来检查数字是否是数字字符串。

例如，我们可以写:

```
const isNumeric = (value) => {
  return /^-?\d+$/.test(value);
}console.log(isNumeric('123'))
console.log(isNumeric('123abc'))
```

`/^-?\d+$/` regex 让我们检查一个字符串是否以一个负号开始，后面有数字。

因此，第一个控制台日志记录`true`和第二个日志记录`false`。

# 结论

我们可以使用 regex 或者各种内置的函数和运算符来检查一个字符串在 JavaScript 中是否是数字。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)