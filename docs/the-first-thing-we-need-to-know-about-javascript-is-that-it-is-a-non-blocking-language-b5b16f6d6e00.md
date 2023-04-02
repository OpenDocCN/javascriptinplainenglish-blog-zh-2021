# JavaScript 运行时简介

> 原文：<https://javascript.plainenglish.io/the-first-thing-we-need-to-know-about-javascript-is-that-it-is-a-non-blocking-language-b5b16f6d6e00?source=collection_archive---------12----------------------->

![](img/d202b1f90671ae998ef5d3b4496c69d0.png)

Photo by [Florian Olivo](https://unsplash.com/@florianolv?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

关于 JavaScript，我们需要知道的第一件事是，它是一种非阻塞语言。如果您是 JavaScript 新手，您可能想知道非阻塞是什么意思。让我们从这个开始。

**阻塞**是代码执行的一种形式，它会显式地按顺序执行每一行代码，直到第一个进程完成后才会进入下一个进程。好吧，无阻塞几乎是相反的。这意味着，如果调用堆栈上有两个函数，JavaScript 不会等待第一个进程完成后再继续。

你很可能听说过异步和同步代码。JavaScript 既是异步的，也是同步的。让我们来看一个例子，让它更清楚。

```
function add(a, b) {
  return a + b
}
​
function average(a, b){
  return add(a, b) / 2
}
​
console.log(average(10, 20))
*//=> 15*
```

如您所见，JavaScript 返回 15，但这是如何实现的呢？在 JavaScript 执行代码之前，堆栈看起来像这样:

1.  添加()
2.  平均值()
3.  console.log(平均值())
4.  主()

如果你还不知道`main()`，是整个程序还是文件调用。JavaScript 将从上到下执行。这里的过程叫做后进先出(LIFO)。

您可能已经注意到，它既是“最后一个”，也是我们的第一行代码。因为在第一次传递过程中，JavaScript 是自下而上编译的。然后，在程序生命周期的运行时阶段，由于编译的方式，前面的代码行实际上是堆栈中的第一行代码。

我希望这已经把事情搞清楚了，现在你对 JavaScript 运行时有了一个基本的概念。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)