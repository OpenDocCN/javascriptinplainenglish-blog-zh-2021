# 如何在 JavaScript 中获取时间戳？

> 原文：<https://javascript.plainenglish.io/how-to-get-a-timestamp-in-javascript-63c05f19e544?source=collection_archive---------6----------------------->

![](img/665e10ccb702102f4feca9d3e9d598f4.png)

Photo by [Sonja Langford](https://unsplash.com/@sonjalangford?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

UNIX 时间戳是自 UTC 时间 1970 年 1 月 1 日午夜以来的秒数。

它经常被使用，以便我们可以很容易地计算时间。

在本文中，我们将研究如何用 JavaScript 从 date 对象中获取 UNIX 时间戳。

# +运算符

我们可以使用`+`操作符将 date 对象转换成 UNIX 时间戳。

例如，我们可以写:

```
+new Date()
```

date 对象之前的`+`操作符触发`Date`对象中的`valueOf`方法，以数字形式返回时间戳。

# getTime 方法

我们可以叫`getTime`做同样的事情。

例如，我们可以写:

```
new Date().getTime()
```

返回日期的 UNIX 时间戳。

# Date.now 方法

`Date.now`是`Date`构造函数的静态方法，它让我们获得当前的日期时间时间戳。

例如，我们可以写:

```
Date.now()
```

时间戳是以毫秒为单位返回的，所以我们必须将它除以 1000，并对其进行舍入，以获得以秒为单位的时间戳。

为此，我们写道:

```
Math.floor(Date.now() / 1000)
```

`Math.floor`将数字向下舍入到最接近的整数。

我们也可以用`Math.round`将它圆整成:

```
Math.round(new Date().getTime() / 1000);
```

# 数字函数

`Number`函数是一个全局函数，让我们将非数字对象或原始值转换成数字。

我们可以用它将日期转换成时间戳。

为此，我们写道:

```
Number(new Date())
```

然后我们得到以秒为单位返回的时间戳，因为它触发了类似于`+`操作符的`Date`实例的`valueOf`方法。

# Lodash _。现在方法

Lodash 还有一个返回当前时间戳的`now`方法。

为了使用它，我们写:

```
_.now();
```

它还会返回当前日期的时间戳。

# 结论

有很多方法可以获得当前日期和时间的时间戳，或者用 JavaScript 得到我们想要的日期时间。

*更多内容看* [***说白了. io***](http://plainenglish.io)