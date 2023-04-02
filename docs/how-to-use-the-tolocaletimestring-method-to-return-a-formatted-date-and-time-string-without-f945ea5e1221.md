# 如何使用 toLocaleTimeString 方法返回不包含秒的格式化日期和时间字符串？

> 原文：<https://javascript.plainenglish.io/how-to-use-the-tolocaletimestring-method-to-return-a-formatted-date-and-time-string-without-f945ea5e1221?source=collection_archive---------7----------------------->

![](img/49f19e393e49a14f287fa641a335dceb.png)

Photo by [Sonja Langford](https://unsplash.com/@sonjalangford?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望将 JavaScript 日期对象格式化为时间字符串，但忽略字符串中的秒。

在本文中，我们将研究如何使用`toLocaleTimeString`方法返回格式化的时间字符串，而不在字符串中包含秒。

# 将小时和分钟设置为两位数

我们可以将`hour`和`minute`属性设置为`'2-digit'`，从返回的时间字符串中去掉秒。

例如，我们可以写:

```
const dateWithoutSecond = new Date();
const formatted = dateWithoutSecond.toLocaleTimeString([], {
  hour: '2-digit',
  minute: '2-digit'
});
console.log(formatted)
```

我们创建一个`Date`实例，并将其存储在`dateWithoutSecond`变量中。

然后我们用一个对象调用它的`toLocateString`，将`hour`和`minute`选项设置为`'2-digit'`，返回一个不带秒的时间字符串。

所以`formatted`应该是一个类似于`'04:05 PM’`的字符串。

# 将 timeStyle 设为 short

我们还可以将`timeStyle`选项设置为 short，以便从返回的时间字符串中忽略秒。

例如，我们可以写:

```
const dateWithoutSecond = new Date();
const formatted = dateWithoutSecond.toLocaleTimeString([], {
  timeStyle: 'short'
});
console.log(formatted)
```

来做这个。

那么`formatted`就是类似于`'4:07 PM’`的东西。

# 结论

我们可以用`toLocateTimeString`设置各种选项来返回一个没有秒部分的时间字符串。

*更多内容请看*[***plain English . io***](http://plainenglish.io)