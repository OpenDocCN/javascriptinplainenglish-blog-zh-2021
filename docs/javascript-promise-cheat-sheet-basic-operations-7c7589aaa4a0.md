# JavaScript Promise 备忘单—基本操作

> 原文：<https://javascript.plainenglish.io/javascript-promise-cheat-sheet-basic-operations-7c7589aaa4a0?source=collection_archive---------10----------------------->

![](img/f09f96bce1cad943866eb378f71d0e9c.png)

Photo by [Katerina Pavlyuchkova](https://unsplash.com/@kat_katerina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript promises 让我们可以轻松地将非 IO 阻塞的异步代码顺序添加到我们的 JavaScript 应用程序中。

因此，它们在任何地方都被使用。

在本文中，我们将看看如何在 JavaScript 代码中使用承诺。

# 创造一个承诺

我们可以用`Promise`构造函数创建一个承诺。

例如，我们可以写:

```
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('foo');
  }, 300);
});
```

将回调传递给`Promise`构造函数。

`resolve`通过返回值实现承诺。

`reject`是一个抛出错误的函数。

# then 方法

我们可以使用`then`方法来获得承诺的解析值。

例如，我们可以写:

```
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('foo');
  }, 300);
});myPromise
  .then(
    val => console.log(val),
    err => console.log(err)
  )
```

第一个`then`回调将解析的值作为参数。

第二个`then`回调将被拒绝的值作为参数。

# 连锁承诺

我们可以通过在`then`回调中返回一个承诺来链接多个承诺。

例如，我们可以写:

```
Promise.resolve(1)
  .then(() => Promise.resolve(2))
  .then((val) => console.log(val))
```

我们称`Promise.resolve`为创造一个解决问题的承诺。

在第一个`then`回调中，我们返回由`Promise.resolve(2)`创建的承诺。

然后，我们用`val`参数获得该承诺的解析值。

所以`val`是 2。

# 同时运行所有承诺

我们可以使用`Promise.all`方法同时运行所有承诺。

例如，我们可以写:

```
Promise.all([
    Promise.resolve(1),
    Promise.resolve(2),
    Promise.resolve(3),
  ])
  .then((vals) => console.log(vals))
```

我们给`Promise.all`打电话，提出了 3 个解决问题的承诺。

然后在`then`回调中，我们有`vals`参数，它有一个已解析值的数组。

所以`vals`就是`[1, 2, 3]`，是所有承诺的解析值。

# 不管结果如何，都要等待所有的承诺得到解决

我们可以使用`Promise.allSettled`方法同时运行所有承诺，并获得它们的结果，不管它们是被解决还是被拒绝。

例如，我们可以写:

```
Promise.allSettled([
    Promise.resolve(1),
    Promise.reject('error'),
    Promise.resolve(3),
  ])
  .then((vals) => console.log(vals))
```

然后我们得到:

```
[
  {
    "status": "fulfilled",
    "value": 1
  },
  {
    "status": "rejected",
    "reason": "error"
  },
  {
    "status": "fulfilled",
    "value": 3
  }
]
```

作为`vals`的值。

`status`有出息的地位。

并且`value`有数值。

# 等到第一个承诺解决

方法让我们等到第一个承诺被解决。

例如，我们可以写:

```
Promise.any([
    Promise.reject('error'),
    Promise.resolve(1),
    Promise.resolve(3),
  ])
  .then((val) => console.log(val))
```

是 1，因为它是第一个解析的承诺。

`Promise.any`返回一个承诺，其值为解决的第一个承诺的值。

# 等到任何一个承诺被解决或拒绝

我们可以使用`Promise.race`方法等待，直到任何承诺解决或拒绝。

所以如果我们有:

```
Promise.race([
    Promise.reject('error'),
    Promise.resolve(1),
    Promise.resolve(3),
  ])
  .then((val) => console.log(val))
  .catch((err) => console.log(err))
```

然后`catch`回调将记录`'error'`，因为第一个承诺因`'error'`原因被拒绝。

# 结论

我们可以用承诺来简化异步 JavaScript 代码的编写。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)