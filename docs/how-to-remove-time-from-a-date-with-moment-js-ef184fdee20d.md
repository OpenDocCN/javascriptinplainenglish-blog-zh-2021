# 如何用 Moment.js 去掉日期中的时间？

> 原文：<https://javascript.plainenglish.io/how-to-remove-time-from-a-date-with-moment-js-ef184fdee20d?source=collection_archive---------9----------------------->

![](img/bacd32f4b9a3c56f31b4d131aec94232.png)

Photo by [Nathan Dumlao](https://unsplash.com/@nate_dumlao?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望从 JavaScript 应用程序中删除日期的时间部分。

我们可以通过 moment.js 库轻松做到这一点。

在本文中，我们将研究如何使用 moment.js 删除日期的时间部分。

# 方法的开始

我们可以用`startOf`方法删除日期中的时间部分。

例如，我们可以写:

```
const day = moment(new Date(2021, 1, 1, 1, 1)).startOf('day')
console.log(day.toDate())
```

我们传递一个日期，并在`moment`函数中设置小时和分钟。

然后我们调用带有`'day'`参数的`startOf`来返回一个时间设置为同一天午夜的 moment 对象。

然后我们调用`toDate`将其转换回原生的 JavaScript 日期。

所以我们得到:

```
Mon Feb 01 2021 00:00:00 GMT-0800 (Pacific Standard Time)
```

因此，如果我们设备的时间是在太平洋时区。

# 格式方法

`format`方法让我们按照自己想要的方式格式化日期。

我们可以传入`'LL'`格式化代码来返回一个只包含日期的日期部分的日期字符串。

例如，我们可以写:

```
const day = moment(new Date(2021, 1, 1, 1, 1)).format('LL')
console.log(day)
```

我们用同样的方法创建力矩对象。

但是在那之后，我们用`'LL'`格式化代码调用`format`。

那么`day`将是下面的日期字符串:

```
'February 1, 2021'
```

同样，我们可以传入`'L'`来获得 MM/DD/YYYY 格式的日期字符串。

所以我们可以写:

```
const day = moment(new Date(2021, 1, 1, 1, 1)).format('L')
console.log(day)
```

我们得到了:

```
'02/01/2021'
```

作为`day`的值。

我们也可以使用 MM 来获得 2 位数的月份。DD 得到 2 位数的日期。YYYY 得到 4 位数的年份。

所以我们可以写:

```
const day = moment(new Date(2021, 1, 1, 1, 1)).format('MM/DD/YYYY')
console.log(day)
```

获得与`'L'`相同的结果。

MMMM 获取完整的月份名称，D 获取不带前导零填充的日期。

所以我们可以写:

```
const day = moment(new Date(2021, 1, 1, 1, 1)).format('MMMM D, YYYY')
console.log(day)
```

获取与`'LL'`相同的日期字符串。

# 结论

我们可以使用`startOf`方法返回一个没有日期时间部分的时刻日期对象。

同样，我们可以使用`format`方法返回一个没有日期时间部分的日期字符串。