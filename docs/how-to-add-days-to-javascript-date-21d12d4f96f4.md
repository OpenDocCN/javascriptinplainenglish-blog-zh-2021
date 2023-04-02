# 如何给 JavaScript Date 添加天数？

> 原文：<https://javascript.plainenglish.io/how-to-add-days-to-javascript-date-21d12d4f96f4?source=collection_archive---------22----------------------->

![](img/1216cb023293dc925dfc2588fdd8596e.png)

Photo by [Dakota Corbin](https://unsplash.com/@thedakotacorbin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

将日期添加到 JavaScript 日期是我们有时不得不做的操作。

在本文中，我们将了解如何向 JavaScript date 对象添加日期。

# setDate 方法

我们可以使用`setDate`方法轻松地给日期添加天数。

例如，我们可以写:

```
const addDays = (date, days) => {
  const result = new Date(date);
  result.setDate(result.getDate() + days);
  return result;
}const result = addDays(new Date(2021, 1, 1), 2)
console.log(result)
```

我们有`addDays`函数来添加天数。

在函数中，我们将`date`传递给`Date`构造函数。

然后我们用`getDate`方法调用`setDate`来得到一个月中的某一天。

然后我们给它加上`days`。

最后，我们返回`result`，它包含添加了`days`的新日期。

因此，当我们在倒数第二行调用它时，我们得到:

```
'Wed Feb 03 2021 00:00:00 GMT-0800 (Pacific Standard Time)'
```

作为`result`的值。

`setDate`将计算新的日期值，不管我们向它传递什么数字。

例如，如果我们写:

```
const addDays = (date, days) => {
  const result = new Date(date);
  result.setDate(result.getDate() + days);
  return result;
}const result = addDays(new Date(2021, 1, 1), 100)
console.log(result)
```

然后`result`就是`'Wed May 12 2021 00:00:00 GMT-0700 (Pacific Daylight Time)’`，还是我们期待的。

# 设置时间方法

同样，我们也可以调用`setTime`来设置日期的时间戳，而不是天数。

这让我们可以更精确地添加时间。

例如，我们可以写:

```
const date = new Date(2021, 1, 1)
const duration = 2;
date.setTime(date.getTime() + (duration * 24 * 60 * 60 * 1000));
```

`date.getTime`返回以毫秒为单位的时间戳。

然后我们加上以天为单位的`duration`，通过乘以`24 * 60 * 60 * 1000`转换成毫秒。

然后我们得到`'Wed Feb 03 2021 00:00:00 GMT-0800 (Pacific Standard Time)’`作为`date`的新值。

# 结论

我们可以使用本地 JavaScript date 方法向 JavaScript 日期添加天数。

*更多内容看* [***说白了***](http://plainenglish.io/)