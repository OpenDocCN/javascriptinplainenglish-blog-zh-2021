# 如何测量一个 JavaScript 函数执行的时间？

> 原文：<https://javascript.plainenglish.io/how-to-measure-the-time-taken-by-a-javascript-function-to-execute-3b24dfc53b4f?source=collection_archive---------6----------------------->

![](img/e4dabf2e8e962c04dfcd4d8856797c72.png)

Photo by [William Recinos](https://unsplash.com/@iwillbmm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须找出一个 JavaScript 函数运行需要多长时间。

在本文中，我们将了解如何测量 JavaScript 函数运行所花费的时间。

# performance.now()方法

测量 JavaScript 代码运行时间的一种方法是使用`performance.now`方法。

它以毫秒为单位返回当前时间的时间戳。

因此，要使用它，我们可以写:

```
const t0 = performance.now()
for (let i = 0; i <= 1000; i++) {
  console.log(i)
}
const t1 = performance.now()
console.log(t1 - t0, 'milliseconds')
```

我们在运行代码之前和之后调用`performance.now`。

然后我们用代码运行前的时间减去代码运行后的时间，得到代码的运行时间。

# console.time 和 console.timeEnd 方法

我们可以使用`console.time`方法开始测量一段代码运行所需的时间。

然后我们可以用`console.timeEnd`的方法停止测量。

它们都把一个字符串作为参数，我们可以用它来标识我们要测量的东西。

所以为了开始测量，我们用一个字符串标识符调用`console.time`。

为了结束测量，我们使用与`console.time`相同的字符串标识符调用`console.timeEnd`。

例如，我们可以写:

```
console.time('loop')
for (let i = 0; i <= 1000; i++) {
  console.log(i)
}
console.timeEnd('loop')
```

在调用了`timeEnd`之后，我们应该得到标识符字符串，其中记录了`console.time`和`console.timeEnd`方法调用之间的时间，以毫秒为单位。

# 结论

我们可以用`performance`接口或控制台方法来测量运行一段 JavaScript 所需的时间。