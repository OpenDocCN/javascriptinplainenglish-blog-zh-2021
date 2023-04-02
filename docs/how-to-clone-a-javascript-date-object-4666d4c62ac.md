# 如何克隆一个 JavaScript 日期对象？

> 原文：<https://javascript.plainenglish.io/how-to-clone-a-javascript-date-object-4666d4c62ac?source=collection_archive---------10----------------------->

![](img/9793e9bf2e7c776062a66afce1929bf9.png)

Photo by [Quaid Lagan](https://unsplash.com/@freshseteyes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能需要在代码中克隆一个 JavaScript 日期对象。

在本文中，我们将研究在 JavaScript 代码中克隆日期对象的方法。

# Date.prototype.getTime 和日期构造函数

我们可以将时间戳构造函数传递给`Date`构造函数。

因此，我们可以从现有的 date 对象中获取时间戳，然后将其传递给`Date`构造函数。

例如，我们可以写:

```
const date = new Date();
const copiedDate = new Date(date.getTime());
console.log(copiedDate)
```

我们调用`getTime`从`date`对象返回时间戳。

然后我们将它传递给`Date`构造函数来创建新的日期对象。

而`copiedDate`是新的日期对象。

# 日期.原型.值

我们还可以用 date 对象的`valueOf`方法获得时间戳。

例如，我们可以写:

```
const date = new Date();
const copiedDate = new Date(date.valueOf());
console.log(copiedDate)
```

我们得到了和上一个例子一样的结果。

# 一元加号运算符

从 JavaScript date 对象获取时间戳的另一种方法是使用一元加号运算符。

例如，我们可以写:

```
const date = new Date();
const copiedDate = new Date(+date);
console.log(copiedDate)
```

我们得到了和前面例子一样的结果。

# 将日期对象直接传入日期构造函数

`Date`构造函数也直接接受一个日期对象。

所以我们可以用它来创建原始日期对象的克隆。

例如，我们可以写:

```
const date = new Date();
const copiedDate = new Date(date);
console.log(copiedDate)
```

我们得到了和以前一样的结果。

# 结论

在 JavaScript 中有几种方法可以使用克隆日期对象。

一种方法是用各种操作符或方法获取时间戳，并将其传递给`Date`构造函数。

另一种方法是将`Date`实例本身传递给`Date`构造函数来创建一个新的`Date`实例。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)