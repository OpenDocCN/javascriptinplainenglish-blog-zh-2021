# 如何检查一个 JavaScript 对象是否是日期对象？

> 原文：<https://javascript.plainenglish.io/how-to-check-whether-a-javascript-object-is-a-date-object-f5acb9bffea3?source=collection_archive---------9----------------------->

![](img/8c38b301e266463a4f08674977ec75ce.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须检查一个 JavaScript 对象是否是一个日期对象。

在本文中，我们将研究检查 JavaScript 对象是否是日期对象的方法。

# 检查日期对象具有的方法

我们可以检查日期对象拥有的方法。

为此，我们可以使用`typeof`操作符。

例如，我们可以写:

```
const date = new Date(2021, 1, 1);
console.log(typeof date.getMonth === 'function')
```

我们通过使用`typeof`操作符查看它是否返回`'function'`来检查`getMonth`方法是否是一个函数。

如果是`true`，那么我们知道`date`很可能是一个`Date`实例。

控制台日志应该记录`true`，所以它很可能是一个`Date`实例。

# 运算符的实例

更准确的检查是检查对象是否是从`Date`构造函数创建的。

如果是，那么我们知道它一定是一个`Date`实例。

例如，我们可以写:

```
const date = new Date(2021, 1, 1);
console.log(date instanceof Date)
```

检查`date`是否是用`instanceof`操作符从`Date`构造函数创建的。

左边的操作数是我们正在检查的对象。

右边的操作数是我们要检查的构造函数。

由于`date`是从`Date`创建的，控制台日志应该记录`true`。

为了检查一个对象是否是从`Date`构造函数跨越框架边界创建的，我们可以用`toString`方法将它转换成一个字符串并检查它的内容。

为此，我们写道:

```
const date = new Date(2021, 1, 1);
console.log(Object.prototype.toString.call(date) === '[object Date]')
```

我们称`toString`为`Object.prototype.toString.call`，因为`toString`可能会被我们自己的方法覆盖。

通过这样调用，我们确保调用内置的`toString`方法，而不是我们自己创建的方法。

# 检查无效日期

如果我们向`Date`构造函数传递不能解析为日期的东西，那么当对象被转换为字符串时，它返回`'Invalid Date'`。

因此，我们可以通过编写以下代码来检查这一点:

```
console.log(new Date('abc').toString() === 'Invalid Date')
```

我们将`'abc'`传入`Date`构造函数，它不能被解析为日期。

所以当我们调用`toString`时，它返回`‘Invalid Date’`。

因此，控制台日志应该记录`true`。

# 结论

有几种方法可以用来用 JavaScript 检查有效的日期对象或无效的日期对象。