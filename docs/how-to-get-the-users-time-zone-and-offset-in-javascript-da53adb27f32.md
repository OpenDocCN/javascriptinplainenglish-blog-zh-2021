# 如何在 JavaScript 中获取用户的时区和偏移量？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-users-time-zone-and-offset-in-javascript-da53adb27f32?source=collection_archive---------3----------------------->

![](img/144b7b99dced0e8fd89e2b953d50fd60.png)

Photo by [JL Magata](https://unsplash.com/@jlmagata?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要在 JavaScript web 应用程序中获取用户的时区。

在本文中，我们将研究如何在 JavaScript 中获取用户的时区和时差。

# date . prototype . gettimezoneoffset

JavaScript 的本机`Date`对象具有返回用户时区的`getTimezoneOffset`方法。

要使用它，我们可以写:

```
const offset = new Date().getTimezoneOffset();
console.log(offset);
```

它返回 UTC 和本地时间之间的差值。

因此，如果我们使用太平洋标准时间，我们会看到`offset`是 480。

当它落后于 UTC 时，偏移量为正，否则为负。

偏移量以分钟为单位，所以我们用它除以 60 来得到小时数。

夏令时防止该值保持不变。

# `The Intl.DateTimeFormat Constructor`

此外，我们可以使用`Intl.DateTimeFormat().resolvedOptions().timeZone`属性来获取用户的时区。

例如，如果我们有:

```
console.log(Intl.DateTimeFormat().resolvedOptions().timeZone)
```

如果我们在太平洋时区，我们可能会得到这样的结果:

```
'America/Los_Angeles'
```

已退回。

# 从日期字符串中提取时区

我们可以从 JavaScript 本地`Date`实例的`toString`方法返回的字符串中提取时区。

例如，我们可以写:

```
const split = new Date().toString().split(" ");
const timeZone = split.slice(-3).join(' ')
console.log(timeZone)
```

如果我们在太平洋标准时区，那么`timeZone`应该是`‘(Pacific Standard Time)’`。

我们将从`toString`返回的日期字符串用一个空格与`split`分开。

然后我们用-3 调用`slice`来获得字符串的最后 3 部分。

我们用`join`将它们连接在一起。

为了使提取更容易，我们可以使用一个 regex 对象。

例如，我们可以写:

```
const [timeZone] = new Date().toString().match(/([A-Z]+[\+-][0-9]+.*)/)
console.log(timeZone)
```

获取日期字符串中包含大写字母、加号或减号、数字和时区名称的部分。

我们在它上面调用`match`来获得匹配。

它返回一个对象，所以我们可以析构结果并将其赋给`timeZone`。

所以`timeZone`是:

```
'GMT-0800 (Pacific Standard Time)'
```

我们只能通过书写来提取字母和数字部分:

```
const [timeZone] = new Date().toString().match(/([A-Z]+[\+-][0-9]+)/)
console.log(timeZone)
```

我们用`timeZone`得到`'GMT-0800'`。

我们可以用以下内容提取括号中的文本:

```
const [timeZone] = new Date().toString().match(/\(([A-Za-z\s].*)\)/)
console.log(timeZone)
```

而`timeZone`将会是`‘(Pacific Standard Time)‘`。

此外，我们可以通过编写以下内容来提取 UTC 的小时差异:

```
const [timeZone] = new Date().toString().match(/([-\+][0-9]+)\s/)
console.log(timeZone)
```

如果我们在太平洋标准时间时区，就会得到`'-0800'`。

# 结论

我们可以用 JavaScript 以多种方式获取用户的时区。

我们可以从日期字符串中提取项目，或者我们可以使用库的内置方法来提取它们。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***