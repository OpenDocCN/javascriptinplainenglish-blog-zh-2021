# 如何将 Moment.js 对象转换成 JavaScript 日期对象或字符串？

> 原文：<https://javascript.plainenglish.io/how-to-transform-moment-js-objects-to-javascript-date-objects-or-strings-fb23c61c0ec6?source=collection_archive---------1----------------------->

![](img/21fa922bff07cd3dbac55f5ae3cc0c2b.png)

Photo by [Sarah Dorweiler](https://unsplash.com/@sarahdorweiler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Moment.js 是一个有用的库，让我们可以轻松地操作日期。

然而，在许多情况下，我们不得不将 moment 对象转换回原生的 JavaScript date 对象，以让我们做我们想做的事情。

在本文中，我们将研究如何将 moment.js 对象转换为 JavaScript 日期对象或字符串。

# toDate 方法

moment 对象附带的`toDate`方法让我们可以将 moment 对象转换为本地 JavaScript 日期对象。

例如，我们可以写:

```
console.log(moment().toDate());
```

将存储当前日期时间的 moment 对象转换回本地 JavaScript date 对象。

我们应该得到这样的结果:

```
Fri Feb 19 2021 17:08:49 GMT-0800 (Pacific Standard Time)
```

从控制台日志中。

# 输出到字符串

我们可以使用`format`方法从 moment 对象返回格式化的日期字符串。

例如，我们可以写:

```
console.log(moment().format("YYYY-MM-DD HH:mm:ss"));
```

`YYYY`是一个 4 位数年份的格式代码。

`MM`是一个 2 位数月份的格式代码。

`DD`是一个 2 位数日期的格式代码。

`HH`是一个 2 位数小时的格式代码。

`mm`是 2 位数分钟的格式代码。

`ss`是 2 位数秒的格式化代码。

因此，我们应该得到这样的结果:

```
2021-02-19 17:10:17
```

从控制台日志中。

# 将时间转换为给定时区中的等效时间

我们可以把一个给定时间的力矩物体转换成它在给定时区的等效物。

首先，我们通过编写以下代码来包含这些库:

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js" integrity="sha512-qTXRIMyZIFb8iQcfjXWCO8+M5Tbc38Qi5WzdPOYZHIlZpzBHG3L3by84BBBOiRGiEb7KKtAOAs5qYdUiZiQNNQ==" crossorigin="anonymous"></script><script src="https://cdnjs.cloudflare.com/ajax/libs/moment-timezone/0.5.33/moment-timezone.min.js" integrity="sha512-jkvef+BAlqJubZdUhcyvaE84uD9XOoLR3e5GGX7YW7y8ywt0rwcGmTQHoxSMRzrJA3+Jh2T8Uy6f8TLU3WQhpQ==" crossorigin="anonymous"></script>
```

第一个脚本标签用于 moment.js。

第二个脚本标签用于时刻时区。

第二个脚本标签将把`tz`方法添加到 moment 对象中，让我们将时间转换成不同时区的时间。

例如，我们可以写:

```
moment.tz.add([
  'America/Los_Angeles|PST PDT|80 70|0101|1Lzm0 1zb0 Op0',
  'America/New_York|EST EDT|50 40|0101|1Lz50 1zb0 Op0'
]);
console.log(moment().tz("America/New_York").format("YYYY-MM-DD HH:mm:ss"));
```

我们调用`moment.tz.add`来添加时区数据。

然后我们可以使用这些数据通过`tz`方法进行转换，就像在控制台日志中一样。

`tz`返回一个带有转换时间的 moment 对象，所以我们可以对它调用`format`来返回一个格式化的日期字符串。

要将力矩对象转换为 UTC 中的等效对象，我们可以使用`utc`方法:

```
console.log(moment().utc().format("YYYY-MM-DD HH:mm:ss"));
```

`utc`方法内置在核心的 moment.js 库中，所以我们不需要 moment-timezone 库来使用它。

# 结论

我们可以使用 moment.js 和 moment-timezone 库提供的各种方便的方法将 moment 对象转换为 date 对象或字符串。

*更多内容看* [***说白了. io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报在这里***](http://newsletter.plainenglish.io/) *。*