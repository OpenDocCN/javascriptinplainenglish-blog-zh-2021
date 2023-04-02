# 如何在 JavaScript 中递增一个日期？

> 原文：<https://javascript.plainenglish.io/how-to-increment-a-date-in-javascript-9ab8c9d38e86?source=collection_archive---------7----------------------->

![](img/184d562fc6a4875b9cc499efa4c75b20.png)

Photo by [Şahin Sezer Dinçer](https://unsplash.com/@sahinsezerdincer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，在我们的 JavaScript 代码中，我们需要用 JavaScript 增加一个日期对象。

在本文中，我们将研究如何用 JavaScript 增加日期。

# 使用本地日期方法

用 JavaScript 增加日期的一种方法是使用本地 JavaScript date 方法。

我们可以用 JavaScript 使用`setDate`方法来增加日期。

例如，我们可以写:

```
const tomorrow = new Date();
tomorrow.setDate(tomorrow.getDate() + 1);
```

我们用当前日期加 1 来调用`setDate`。

为了获得当前日期，我们使用了`getDate`方法。

那么`tomorrow`就是明天的日期。

此外，我们可以用`getTime`方法添加毫秒，并以毫秒为单位添加 1 天。

例如，我们可以写:

```
const tomorrow = new Date();
tomorrow.setTime(tomorrow.getTime() + 1000 * 60 * 60 * 24);
```

我们调用`setTime`来设置一个时间戳，单位是毫秒。

在方法调用中，我们调用`getTime`以毫秒为单位返回时间戳。

我们用`1000 * 60 * 60 * 24`把这 1 天加上去。

所以我们得到了和以前一样的结果。

# 使用 Moment.js

增加 JavaScript 日期的另一种方法是使用 moment.js 库。

为了使用它，我们写:

```
const today = moment();
const tomorrow = moment(today).add(1, 'days');
```

我们调用不带参数的`moment`函数来创建带有当前日期和时间的 moment 对象。

然后我们在当前日期调用`add`来添加一天。

我们传入要添加的数量和单位。

# 结论

我们可以用 JavaScript 的原生日期方法或 moment.js 来增加日期

*更多内容请看*[***plain English . io***](http://plainenglish.io)