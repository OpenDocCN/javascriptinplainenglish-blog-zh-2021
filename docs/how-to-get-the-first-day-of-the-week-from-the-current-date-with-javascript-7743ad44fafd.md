# 如何用 JavaScript 从当前日期获取一周的第一天？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-first-day-of-the-week-from-the-current-date-with-javascript-7743ad44fafd?source=collection_archive---------4----------------------->

![](img/59e999ef96f927be227545737c313338.png)

Photo by [Sai De Silva](https://unsplash.com/@scoutthecity?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 从当前日期中获取一周的第一天。

在本文中，我们将研究如何用 JavaScript 从当前日期获取一周的第一天。

# 使用本地日期方法

我们可以使用各种日期方法从当前日期获得一周的第一天。

为此，我们可以写:

```
const getMonday = (d) => {
  const dt = new Date(d);
  const day = dt.getDay()
  const diff = dt.getDate() - day + (day === 0 ? -6 : 1);
  return new Date(dt.setDate(diff));
}console.log(getMonday(new Date(2021, 1, 20)));
```

我们创建的`getMonday`函数接受`d`日期参数。

在函数中，用`Date`构造函数创建一个`Date`实例。

然后我们调用`getDay`来得到星期几。

它为星期天返回 0，为星期一返回 1，以此类推，直到为星期六返回 6。

然后，我们通过减去`day`得到一周的当前日期和同一周的星期一之间的差值，如果`day`为 0，则加回`-6`，否则加 1。

然后我们通过用`diff`调用`dt`上的`setDate`再次使用`Date`构造函数，将日期设置为同一周的星期一。

因此，控制台日志应该记录:

```
Mon Feb 15 2021 00:00:00 GMT-0800 (Pacific Standard Time)
```

结果。

# 结论

我们可以通过获得星期几来获得给定日期的同一周的星期一。

然后我们用该日期减去一周中的某一天，然后再加上天数，得出该日期的同一周的星期一。

*更多内容请看*[***plain English . io***](http://plainenglish.io)