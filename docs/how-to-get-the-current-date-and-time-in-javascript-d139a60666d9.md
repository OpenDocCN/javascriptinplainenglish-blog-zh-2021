# 如何在 JavaScript 中获取当前日期和时间？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-current-date-and-time-in-javascript-d139a60666d9?source=collection_archive---------17----------------------->

![](img/df7b20ea2e235b9eaff8b56dfa01dc11.png)

Photo by [Olga Vyshnevska](https://unsplash.com/@vyshnevska?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

获取当前日期和时间是我们在许多 JavaScript 应用程序中必须做的事情。

在本文中，我们将研究如何用 JavaScript 获取当前日期和时间。

# 使用日期方法

我们可以使用本地 JavaScript 日期方法来获取日期时间的一部分。

例如，我们可以写:

```
const currentDate = new Date();
const dateTime = currentDate.getDate() + "/" +
  (currentDate.getMonth() + 1) + "/" +
  currentDate.getFullYear() + " @ " +
  currentDate.getHours() + ":" +
  currentDate.getMinutes() + ":" +
  currentDate.getSeconds();
```

我们调用`getDate`方法来获取一个月中的某一天。

`getMonth`返回一年中从 0 到 12 的月份。

所以我们必须加 1 来得到一个人类可读的月份数字。

`getFullYear`返回 4 位数的年份数字。

`getHours`返回一天中的小时数。

`getMinutes`返回小时的分钟数。

`getSeconds`返回分钟的秒数。

# `The toLocaleString Method`

我们可以使用 date 对象的`toLocaleString`方法返回一个人类可读的日期字符串。

例如，我们可以写:

```
const dateTime = new Date().toLocaleString();
console.log(dateTime)
```

然后我们会得到这样的结果:

```
2/24/2021, 3:04:27 PM
```

结果。

# `The` toLocaleDateString `Method`

另一种我们可以用来返回人类可读的日期字符串的方法是`toLocaleDateString`方法。

例如，我们可以写:

```
const dateTime = new Date().toLocaleDateString();
console.log(dateTime)
```

调用方法。

我们得到了:

```
2/24/2021
```

结果。

# `The toLocaleTimeString Method`

我们可以使用的另一种返回人类可读日期字符串的方法是`toLocaleTimeString`方法。

它接受一个地区字符串和一个带有我们想要设置的选项的对象，返回日期字符串作为第二个参数。

例如，我们可以写:

```
const dateTime = new Date().toLocaleTimeString('en-US', {
  hour12: false,
  hour: "numeric",
  minute: "numeric"
});
console.log(dateTime)
```

我们会得到这样的结果:

```
15:06
```

从控制台日志中。

`hour12`设置为`false`意味着我们返回一个 24 小时的日期。

`hour`和`minute`被设置为`'numeric'`表示我们以数字形式返回小时和分钟。

# 结论

我们可以使用各种日期方法来返回人类可读的日期字符串或获取日期的一部分。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)