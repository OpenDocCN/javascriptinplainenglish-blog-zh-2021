# 如何在 JavaScript 中比较两个日期

> 原文：<https://javascript.plainenglish.io/how-to-compare-two-dates-with-javascript-6faebd3e4d6?source=collection_archive---------12----------------------->

![](img/0f3715befda58529e4e26bbdb2243aa2.png)

Photo by [Lon Christensen](https://unsplash.com/@lonwake?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

比较两个日期是我们在 JavaScript 应用程序中经常要做的事情。

在本文中，我们将看看如何用 JavaScript 比较两个日期。

# 比较时间戳

比较两个日期的一个简单方法是比较它们的时间戳。

我们可以用`getTime`方法获得时间戳。

例如，我们可以写:

```
const d1 = new Date();
const d2 = new Date(d1);
const same = d1.getTime() === d2.getTime();
const notSame = d1.getTime() !== d2.getTime();
```

`getTime`以秒为单位返回 UNIX 纪元。

现在是 UTC 时间 1970 年 1 月 1 日午夜以来的秒数。

我们也可以写:

```
const d1 = new Date();
const d2 = new Date(d1);
const same = +d1 === +d2;
const notSame = +d1 !== +d2;
```

它用日期对象前的`+`替换了`getTime`。

它和`getTime`做同样的事情。

# 关系运算符

我们可以对日期对象直接使用关系运算符。

例如，我们可以写:

```
const d1 = new Date(2021, 0, 1);
const d2 = new Date(2021, 0, 2);
d1 < d2;
d1 <= d2;
d1 > d2;
d1 >= d2;
```

将它们与关系运算符直接进行比较。

`d1`和`d2`将在比较前转换为时间戳。

# 减去日期

我们也可以从一个日期中减去另一个日期，并将结果与我们想要的进行比较。

例如，我们可以写:

```
const d1 = new Date(2021, 0, 1);
const d2 = new Date(2021, 0, 2);
console.log(d1 - d2 === 0);
console.log(d1 - d2 < 0);
console.log(d1 - d2 > 0);
```

这是可行的，因为`d1`和`d2`在我们减去它们之前被转换成时间戳。

# 比较年、月和日

我们可以比较两个日期对象的年、月和日，以检查它们是否相同，从而确定它们是否是同一个日期。

例如，我们可以写:

```
const d1 = new Date(2021, 0, 1);
const d2 = new Date(2021, 0, 2);
const isSameDate = d1.getFullYear() === d2.getFullYear() &&
  d1.getDate() === d2.getDate() &&
  d1.getMonth() === d2.getMonth();
```

`getFullYear`返回 4 位数的年份数字。

`getDate`返回日期。

并且`getMonth`返回从 0 到 11 的月份。0 是一月，1 是二月，以此类推。

# 结论

我们可以用 JavaScript 通过各种运算符将两个日期转换成数字，从而轻松地对它们进行比较。

然后我们可以对比一下。

我们还可以分别比较它们的年、月和日值。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)