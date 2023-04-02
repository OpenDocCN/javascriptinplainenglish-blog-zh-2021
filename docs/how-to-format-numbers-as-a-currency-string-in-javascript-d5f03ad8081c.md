# 如何在 JavaScript 中将数字格式化为货币字符串？

> 原文：<https://javascript.plainenglish.io/how-to-format-numbers-as-a-currency-string-in-javascript-d5f03ad8081c?source=collection_archive---------25----------------------->

![](img/8d4e31677e167481e9864646484efe04.png)

Photo by [Macau Photo Agency](https://unsplash.com/@macauphotoagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

将数字格式化为货币字符串是我们在 JavaScript 应用程序中有时不得不做的事情。

在本文中，我们将了解如何用 JavaScript 将数字格式化为货币字符串。

# 国际机场。数字格式构造函数

我们可以使用大多数浏览器自带的`Intl.NumberFormat`构造函数将数字格式化为货币字符串。

例如，我们可以写:

```
const formatter = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD',
});
const str = formatter.format(1500);
console.log(str)
```

我们传入 locale 和一个带有构造函数的格式化选项参数的对象。

`style`设置为`'currency'`，将数字格式化为货币字符串。

`currency`设置为`'USD'`，让我们把它的数字格式化成美元格式。

然后我们就用金额调用`format`，把结果赋给`str`。

所以`str`就是`‘$1,500.00’`。

我们还可以设置对象中的`minimumFractionDigits`和`maximumFractionDigits`属性来设置要返回的最小和最大小数位数。

# `toLocaleString`

JavaScript 字符串带有`toLocaleString`方法，该方法允许我们将数字格式化为货币字符串。

例如，我们可以写:

```
const str = (1500).toLocaleString('en-US', {
  style: 'currency',
  currency: 'USD',
});
console.log(str)
```

参数与`format`方法相同。

而且我们得到的结果和`Intl.NumberFormat`一样。

如果我们需要格式化大量数字，那么`Intl.NumberFormat`比`toLocaleString`快 70 倍，所以如果我们需要格式化大量数字，最好使用`Intl.NumberFormat`。

# 正则表达式替换

我们可以使用`toFixed`方法返回一个有两位小数的字符串。

然后我们可以使用`replace`给返回的字符串添加千位分隔符。

例如，我们可以写:

```
const str = (123.45).toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
```

`?=`是一个前瞻断言，让我们在一个数字后面的字符串中获得 3 个数字的组。

因此，如果它看到一组 3 个数字在另一个数字后面，那么它会在数字之间添加一个逗号。

`$&`表示我们希望在现有字符串中进行替换，而不是替换字符。

所以，`str`应该是`'123.45'`。

# 结论

我们可以通过使用内置方法用 JavaScript 将数字格式化成货币字符串。

此外，我们可以使用`replace`方法在 3 位数的组之间添加逗号。

*更多内容看*[***plain English . io***](http://plainenglish.io)