# 理解 JavaScript 中的 Currying 函数

> 原文：<https://javascript.plainenglish.io/understanding-currying-function-in-javascript-c3e1c92b7579?source=collection_archive---------13----------------------->

![](img/c9a73d3428a29accc469dbf6aa59f68a.png)

Photo by [oxendine](https://unsplash.com/@oxendine_) on [unsplash](https://unsplash.com/photos/tJPFo1uJ3no)

Currying 是 JavaScript 中面对函数时应该知道的高级技术。正常情况下，JavaScript 箭头函数是这样写的。

```
const multiply = (a,b) => a*b
```

从上面的代码中，我们可以理解该函数是用来将两个变量`a`和`b`相乘并显示结果的。但是，让我们进入一个条件时，currying 被使用。我有这样的控制台程序

```
console.log(multiply(5)(6))
```

通过使用上面的函数，程序会出错，因为(6)变量不是函数。为了让程序工作，我们需要 currying 函数来完成他的工作。所以程序是这样写的

```
const multiply = (a) => (b) => a * b
```

如果我们再次运行代码，输出将打印出正确的答案。你知道它为什么有效吗？

简单地说，currying 就是将一个接受多个参数的函数转换成一个接受单个参数的函数序列的技术。这个功能可以帮助我们去除重复。这是我从[西蒙施瓦茨](https://gist.github.com/simonschwartz)那里得到的例子。

## 老办法

## currying 函数

从上面的例子中，我们知道我们不需要多次重复写“mysite.com”或“mysite-careers.com”。我们只需要第一次声明它，它就可以生成我们想要的 URL。

我已经讲了太多使用它的好处，但是我并不真的推荐它，因为并不是每个开发人员都知道这个先进的东西。我之所以写这篇文章，是因为这些小知识让你离掌握 JavaScript 更近了一步。

谢谢