# JavaScript 的亮点—日期和舍入

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-dates-and-rounding-2bd7adfb70b3?source=collection_archive---------15----------------------->

![](img/d8c376c334874ccb57b7e284e6e7a5c6.png)

Photo by [Mark Gosling](https://unsplash.com/@broadcast21?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 控制小数的长度

我们可以通过使用`toFixed`方法来控制小数的长度。

例如，如果我们有:

```
let total = (8.8888).toFixed(2);
```

那么`total`就是`'8.89'`。`toFixed`获取要舍入的位数，并返回带有舍入数字的字符串。

如果小数以 5 结尾，通常会向上取整。

但是有些浏览器可能会向下舍入。

# 获取当前日期和时间

为了获得当前的日期和时间，我们可以用`new Date()`创建一个新的`Date`实例。

然后，我们可以通过编写以下代码将`Date`实例转换为字符串:

```
let now = new Date();
let dateString = now.toString();
```

为了得到星期几，我们调用`getDay`方法:

```
let now = new Date();
let day = now.getDay();
```

它返回一个从 0 到 6 的数字，0 表示星期天，6 表示星期六。

如果我们想显示一个更容易阅读的日期，我们可以这样写:

```
let dayNames = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
let now = new Date();
let day = now.getDay();
let dayName = dayNames[day];
```

我们可以用`day`作为`dayNames`的索引，得到英文版的星期几。

# 提取部分日期和时间

`Date`实例带有各种方法来获取日期和时间的不同部分。

`getMonth`返回日期中从 0 到 11 的月份，其中 0 表示一月，11 表示十二月。

`getDate`给出本月日期的数字。

`getFullYear`返回年份的 4 位数版本。

`getHours`给出了一个从 0 到 23 的数字，对应于午夜和晚上 11 点。

`getMinutes`返回 0 到 59 之间的小时分钟数。

`getSeconds`返回 0 到 59 之间的分钟秒数。

并且`getMilliseconds`返回一个从 0 到 999 的数字。

`getTime`给出自 1970 年 1 月 1 日午夜 UTC 以来经过的毫秒数。

我们可以从一个日期实例中调用它们。例如，我们可以写:

```
let now = new Date();
let day = now.getMilliseconds();
```

# 指定日期和时间

我们可以用`Date`构造函数指定日期和时间。

要返回当前日期和时间，我们写:

```
let today = new Date();
```

我们可以通过减去两个日期之间的时间戳来计算天数差:

```
let msToday = new Date().getTime();
let msAnotherDay = new Date(2029, 1, 1).getTime()
let msDiff = msAnotherDay - msToday;
```

然后为了得到天数差，我们可以写出:

```
let daysDiff = msDiff / (1000 * 60 * 60 * 24);
```

如果我们想将天数返回到整数，我们用`Math.floor`向下舍入:

```
daysDiff = Math.floor(daysDiff);
```

# 结论

我们可以用时间戳来计算日期之间的差异。

同样，我们可以用`toFixed`将数字四舍五入到给定的小数位数。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**