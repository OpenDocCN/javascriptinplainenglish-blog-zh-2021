# 如何在 JavaScript 中只比较日期对象的日期部分而不比较时间

> 原文：<https://javascript.plainenglish.io/how-to-compare-the-date-part-of-a-date-object-only-without-comparing-the-time-in-javascript-a1f0af96eb96?source=collection_archive---------8----------------------->

![](img/8f8463de947f4fd6321903ac570e6c23.png)

Photo by [Ashkan Forouzani](https://unsplash.com/@ashkfor121?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望只比较日期的日期部分，而不比较 JavaScript 应用程序中的时间。

在本文中，我们将研究如何用 JavaScript 在不比较时间的情况下比较日期。

# `Date.prototype.setHours`

要比较日期而不比较时间部分，我们可以使用 JavaScript date 对象附带的`setHours`方法将两个日期都设置为午夜。

例如，我们可以写:

```
const date1 = new Date(2021, 1, 1, 1, 1, 1)
date1.setHours(0, 0, 0, 0)const date2 = new Date(2021, 2, 1)
date2.setHours(0, 0, 0, 0)console.log(+date2 > +date1)
```

我们调用`date1`上的`setHours`将`date1`的时、分、秒全部设置为 0。

这会将日期设置为午夜。

然后，我们可以像在最后一行中那样，用>操作符比较这两个没有时间部分的值，

为了安全起见，我们首先用`+`操作符将它们转换成时间戳。

因此，控制台日志应该显示`true`，因为`date2`在`date1`之前。

为了更安全，我们可以在将两个日期都转换为 UTC 日期时间后进行比较。

为此，我们写道:

```
const date1 = new Date(2021, 1, 1, 1, 1, 1)
const date1Copy = new Date(Date.UTC(date1.getFullYear(), date1.getMonth(), date1.getDate()));
date1Copy.setHours(0, 0, 0, 0)const date2 = new Date(2021, 2, 1)
const date2Copy = new Date(Date.UTC(date2.getFullYear(), date2.getMonth(), date2.getDate()));
date2Copy.setHours(0, 0, 0, 0)console.log(+date2Copy > +date1Copy)
```

我们用从`date1`和`date2`检索的日期部分调用`Date.UTC`来创建一个 UTC 时间戳。

然后我们将它们传递给`Date`构造函数来创建新的日期对象。

然后我们在复制的日期上调用`setHours`，然后与它们进行比较。

我们应该从控制台日志中得到相同的结果。

# Moment.js

moment.js 库有一个`isAfter`方法，可以让我们比较两个没有时间部分的日期时间。

为此，我们写道:

```
const date1 = new Date(2021, 9, 20, 12, 0, 0);
const date2 = new Date(2021, 9, 20, 12, 1, 0);
const isAfter = moment(date2).isAfter(date1, 'day');console.log(isAfter)
```

我们在用`date2`日期对象创建的时刻日期对象上调用`isAfter`。

我们将`'day'`传入第二个参数，从比较中排除每个日期的时间部分。

因此，`isAfter`的结果应该是`false`，因为除了时间部分，它们都是同一个日期。

# 结论

我们可以使用本地 JavaScript 日期方法或 moment.js 来比较没有时间部分的日期。

*更多内容请看*[***plain English . io***](http://plainenglish.io)