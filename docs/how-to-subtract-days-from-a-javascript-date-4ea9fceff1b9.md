# 如何从 JavaScript 日期中减去天数？

> 原文：<https://javascript.plainenglish.io/how-to-subtract-days-from-a-javascript-date-4ea9fceff1b9?source=collection_archive---------2----------------------->

![](img/1390095ccbb0dd33a32c6ebe5d7f5ee9.png)

Photo by [Alan Quirvan](https://unsplash.com/@quirva?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从日期中减去日期是我们在 JavaScript 代码中经常要做的操作。

在本文中，我们将看看如何从 JavaScript 日期中减去天数。

# 日期.原型.获取日期和日期.原型.设置日期

我们可以使用`getDate`方法来获取日期。

然后使用`setDate`方法通过操作我们从`getDate`获得的日期并将返回值传递给`setDate`来设置日期。

例如，我们可以写:

```
const date = new Date(2021, 1, 1);
date.setDate(date.getDate() - 5);
console.log(date)
```

从 2021 年 2 月 1 日减去 5 天。

我们从`date`对象调用`getDate`。

然后我们从中减去 5 天。

然后我们将它传递给`setDate`。

所以`date`现在是`'Wed Jan 27 2021 00:00:00 GMT-0800 (Pacific Standard Time)’`。

`date`被替换为`setDate`。

# Date.prototype.getTime 和 Date.prototype.setTime

我们也可以调用`setTime`来设置日期的时间戳，而不是天数。

这更精确，因为时间是以毫秒为单位的。

为此，我们写道:

```
const dateOffset = (24 * 60 * 60 * 1000) * 5;
const date = new Date(2021, 1, 1);
date.setTime(date.getTime() - dateOffset);
console.log(date)
```

我们用毫秒来表示`dateOffset`。

我们有与上一个例子相同的`date`对象。

在第 3 行，我们用从`getTime`返回的时间戳值调用`setTime`，该值以毫秒为单位。

我们用`dateOffset`减去它，也就是 5 天，以毫秒为单位。

`date`替换为`setTime`。

所以现在字符串形式的`date`就是`‘Wed Jan 27 2021 00:00:00 GMT-0800 (Pacific Standard Time)'`。

# moment.js

我们可以使用 moment.js 库来简化日期操作。

例如，我们可以写:

```
const dateMnsFive = moment('2021-02-01').subtract(5, 'day');
console.log(dateMnsFive.toDate())
```

我们用`moment`为 2021 年 2 月 1 日创建一个 moment 对象。

返回的对象有`subtract`方法让我们减去我们想要的时间量。

第一个参数是金额。

第二个参数是要减去的量的单位。

然后我们可以用`toDate`将其转换回原生 JavaScript 日期对象。

所以我们得到了和前面例子一样的结果。

力矩对象也随`toISOString`方法而来。

例如，我们可以写:

```
const dateMnsFive = moment('2021-02-01').subtract(5, 'day');
console.log(new Date(dateMnsFive.toISOString()))
```

我们可以将由`toISOString`返回的字符串传递给`Date`构造函数，以获得一个本地日期对象。

所以我们得到了和上一个例子一样的结果。

# 结论

我们可以用本地 JavaScript 日期方法从日期中减去天数。

为了使工作更容易，我们也可以使用像 moment.js 这样的库来帮助我们。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。****