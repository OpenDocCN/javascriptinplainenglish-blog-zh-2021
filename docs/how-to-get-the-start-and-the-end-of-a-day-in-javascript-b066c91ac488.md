# 如何在 JavaScript 中获取一天的开始和结束

> 原文：<https://javascript.plainenglish.io/how-to-get-the-start-and-the-end-of-a-day-in-javascript-b066c91ac488?source=collection_archive---------6----------------------->

![](img/e09a4c8aa95230dbc5242931e0d5698a.png)

Photo by [Mike Yukhtenko](https://unsplash.com/@yamaicle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们可能想用 JavaScript 来获取一天的开始和结束。

在本文中，我们将研究用 JavaScript 获取一天的开始和结束的方法。

# 使用本地日期方法

用 JavaScript 获取一天的开始和结束的一种方法是使用本地日期方法。

我们可以使用`setHours`方法将一天的时间设置为一天的开始或结束。

例如，我们可以写:

```
const start = new Date(2020, 1, 1, 1, 1);
start.setHours(0, 0, 0, 0);
console.log(start)
```

我们用`Date`构造函数创建`start`日期。

然后我们调用全零的`setHours`将日期时间设置为午夜。

所以`start`是:

```
Sat Feb 01 2020 00:00:00 GMT-0800 (Pacific Standard Time)
```

如果我们在太平洋时间。

同样，我们可以使用`setHours`来设置日期结束时的小时、分钟、秒和毫秒。

为此，我们写道:

```
const end = new Date(2020, 1, 1, 1, 1);
end.setHours(23, 59, 59, 999);
console.log(end)
```

创建一个日期，并通过传入几个参数将其设置为日期的结尾。

23 小时。

前 59 个是分钟。

第二个 59 是秒。

999 是毫秒。

因此，`end`就是:

```
Sat Feb 01 2020 23:59:59 GMT-0800 (Pacific Standard Time)
```

调用`setHours`后。

# 使用 Moment.js

或者，我们可以使用 moment.js 库来返回日期的开始和结束。

例如，我们可以写:

```
const start = moment(new Date(2020, 1, 1, 1, 1)).startOf('day');
console.log(start.toString())
```

使用`moment`函数创建一个 moment 对象，并将一个 JavaScript 本地日期对象作为其参数。

然后我们用`'day'`调用`startOf`来返回一个时间设置为一天开始的 moment 对象。

所以我们得到:

```
Sat Feb 01 2020 00:00:00 GMT-0800
```

作为`start.toString()`的值，如果我们在太平洋时区。

同样，我们可以使用`endOf`方法来获得日期的结束。

为此，我们写道:

```
const end = moment(new Date(2020, 1, 1, 1, 1)).endOf('day');
console.log(end.toString())
```

我们称之为`endOf`而不是`startOf`。

如果我们在太平洋时区，那么`end.toString()`返回`Sat Feb 01 2020 23:59:59 GMT-0800`。

我们也可以在使用`utc`方法调用`startOf`和`endOf`之前将时区转换为 UTC。

例如，我们可以写:

```
const start = moment(new Date(2020, 1, 1, 1, 1)).utc().startOf('day');
console.log(start.toString())const end = moment(new Date(2020, 1, 1, 1, 1)).utc().endOf('day');
console.log(end.toString())
```

进行转换。

然后`start.toString()`返回:

```
Sat Feb 01 2020 00:00:00 GMT+0000
```

而`end.toString()`回报:

```
Sat Feb 01 2020 23:59:59 GMT+0000
```

# 结论

我们可以用 JavaScript 的原生日期方法或 moment.js 来获取日期的开始和结束。

*更多内容请看*[***plain English . io***](http://plainenglish.io)