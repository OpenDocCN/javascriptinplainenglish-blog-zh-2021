# JavaScript 承诺备忘单—处理承诺结果

> 原文：<https://javascript.plainenglish.io/javascript-promise-cheat-sheet-handing-promise-results-1da3ad25b053?source=collection_archive---------18----------------------->

![](img/19903f7cbba511e1a85a299fb01248aa.png)

Photo by [Andrew Petrov](https://unsplash.com/@andrewwwpetrov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript promises 让我们可以轻松地将非 IO 阻塞的异步代码顺序添加到我们的 JavaScript 应用程序中。

因此，它们在任何地方都被使用。

在本文中，我们将看看如何在 JavaScript 代码中使用承诺。

# 创造一个承诺来解决

我们可以创建一个用`Promise.resolve`解决的承诺。

例如，我们可以写:

```
Promise.resolve(1)
  .then((val) => console.log(val))
```

那么`val`就是 1，因为我们把 1 传递给了`Promise.resolve`。

# 做出拒绝的承诺

我们可以创建一个用`Promise.reject`解决的承诺。

例如，我们可以写:

```
Promise.reject('error')
  .catch((err) => console.log(err))
```

那么 err 就是`'error'`，因为`catch`回调捕捉到了被拒绝承诺的原因值。

# 捕捉被拒绝的承诺

我们可以用`Promise.prototype.catch`实例方法处理被拒绝的承诺引发的错误。

例如，我们可以写:

```
Promise.reject('error')
  .catch((err) => console.log(err))
```

那么 err 就是`'error'`，因为`catch`回调捕获了被拒绝承诺的原因值。

这让我们处理第一个被拒绝的承诺的值。

# 从承诺中获得价值

我们可以使用`Promise.prototype.then`方法从已解决的承诺中获取价值。

例如，我们可以写:

```
Promise.resolve(1)
  .then(() => Promise.resolve(2))
  .then((val) => console.log(val))
```

我们用带参数的回调调用`then`,从之前解析的承诺中获取解析的值。

所以`val`是 2。

# 不管承诺结果如何都运行代码

我们可以使用`Promise.prototype.finally`方法来运行代码，而不管承诺发生了什么。

例如，如果我们有:

```
Promise.reject('error')
  .catch((err) => console.log(err))
  .finally(() => console.log('finally'))
```

然后我们会看到`'error'`和`'finally'`被记录，因为`finally`回调运行，而不管承诺是被解决还是被拒绝。

# 结论

我们可以用承诺来简化异步 JavaScript 代码的编写。

*更多内容请看*[***plain English . io***](http://plainenglish.io)