# 给定 YYYY-MM-DD 格式的出生日期，如何用 JavaScript 计算年龄？

> 原文：<https://javascript.plainenglish.io/how-to-calculate-the-age-given-the-birth-date-in-yyyy-mm-dd-format-with-javascript-78c256e770e2?source=collection_archive---------7----------------------->

![](img/2e6d13be81e5f11072e6a6e571eef853.png)

Photo by [Philippe Leone](https://unsplash.com/@philinit?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望根据 JavaScript 代码中的出生日期来计算年龄。

在本文中，我们将看看如何用 JavaScript 计算 YYYY-MM-DD 格式的出生日期的年龄。

# 使用本地日期方法

我们可以使用本地日期方法，根据 YYYY-MM-DD 格式的出生日期来计算一个人的年龄。

为此，我们写道:

```
const calculateAge = (birthday) => {
  const ageDifMs = Date.now() - new Date(birthday).getTime();
  const ageDate = new Date(ageDifMs);
  return Math.abs(ageDate.getUTCFullYear() - 1970);
}console.log(calculateAge('1960-01-21'))
```

我们创建了带有`birthday`参数的`calculateAge`方法，该参数接受一个日期字符串，我们可以将该字符串转换为日期，并基于该日期计算年龄。

在函数中，我们减去了`Date.now`，它有当前日期时间的时间戳，以毫秒为单位。

我们创建一个新的`Date`实例，并调用`getTime`来获取我们传递的`birthday`的时间戳，以毫秒为单位。

然后我们把结果赋给`ageDifMs`。

然后，我们将`ageDifMs`传递给`Date`构造函数以获得`ageDate`，这是从 1970 年 1 月 1 日午夜 UTC 创建的日期加上我们传递的 timespan 指定的 timespan。

我们调用`getUTCFullYear`得到年份减去 1970 得到年龄。

然后调用`Math.abs`以确保它是正的，不管`birthday`是否在 1970 年 1 月 1 日午夜 UTC 之前。

因此，控制台日志应该记录 61。

# 使用 moment.js

为了使计算日期差异更容易，我们可以使用 moment.js 库。

为此，我们写道:

```
const calculateAge = (birthday) => {
  const startDate = new Date();
  const endDate = new Date(birthday);
  return Math.abs(moment.duration(endDate - startDate).years());
}console.log(calculateAge('1960-01-21'))
```

在`calculateAge`函数中，我们像以前一样采用`birthday`参数。

但是我们没有使用本地日期方法，而是使用`moment.duration`方法来计算持续时间。

我们用`endDate — startDate`调用它来获取矩持续时间对象。

然后我们调用`years`得到持续时间作为年数。

然后我们调用`Math.abs`来确保返回的数字是正数。

那么控制台日志应该会给出和以前一样的结果。

# 结论

我们可以通过使用本地 JavaScript 日期方法或 moment.js 来计算给定日期字符串的年龄。

*更多内容看* [***说白了***](http://plainenglish.io/)