# 如何用 JavaScript 遍历一个日期范围？

> 原文：<https://javascript.plainenglish.io/how-to-loop-through-a-date-range-with-javascript-e88951d4f6c?source=collection_archive---------5----------------------->

![](img/b4ba2bdf63ff1aebbdf04f58e836cbfd.png)

Photo by [L.A Co.](https://unsplash.com/@teamlifeadventures?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 遍历一个日期范围。

在本文中，我们将看看如何用 JavaScript 遍历一个日期范围。

# 使用 while 循环

用 JavaScript 遍历日期范围的一种方法是使用`while`循环。

我们可以为开始和结束日期创建变量。

然后我们可以增加开始日期，直到它到达结束日期。

为此，我们写道:

```
const start = new Date("02/05/2020");
const end = new Date("02/10/2020");let loop = new Date(start);
while (loop <= end) {
  console.log(loop);
  let newDate = loop.setDate(loop.getDate() + 1);
  loop = new Date(newDate);
}
```

我们有分别带有开始和结束日期的`start`和`end`变量。

然后，我们创建了用作循环变量的`loop`变量。

我们递增`loop`的日期，直到它到达`end`。

我们通过用`loop.getdate() + 1`调用`setDate`来进行递增。

让我们知道一个月中的某一天。

我们将返回的日期分配给`loop`来增加它。

因此，我们得到:

```
Wed Feb 05 2020 00:00:00 GMT-0800 (Pacific Standard Time)
Thu Feb 06 2020 00:00:00 GMT-0800 (Pacific Standard Time)
Fri Feb 07 2020 00:00:00 GMT-0800 (Pacific Standard Time)
Sat Feb 08 2020 00:00:00 GMT-0800 (Pacific Standard Time)
Sun Feb 09 2020 00:00:00 GMT-0800 (Pacific Standard Time)
Mon Feb 10 2020 00:00:00 GMT-0800 (Pacific Standard Time)
```

从控制台日志中。

# 结论

我们可以用一个 while 循环遍历一个日期范围，这个 while 循环使用一个设置为开始日期的循环变量。

然后我们递增循环变量，直到它到达结束日期。