# 理解递归成为更高效的程序员

> 原文：<https://javascript.plainenglish.io/recursive-recursion-done-recursively-f95ce3d74dd?source=collection_archive---------15----------------------->

![](img/705519a2c9d7103bea62ac27d4ccba79.png)

在这个博客中，我们将讨论计算机科学中的一个关键概念。是的，你已经猜到了——递归！

## 什么是递归？🤔

递归帮助我们以更简单的方式解决复杂的问题。递归的基础是函数调用自身。请看下面这个函数的例子:

```
**function** recursion() {
  recursion();
}
```

好吧，无限递归是没有意义的，但是如果使用正确，它会是一个强大而有用的工具！

## 循环还是递归？➿

最常见的是，我们直接跳到循环来处理任何任务，但是让我们看看如何使用递归。

让我们来看看一个倒计时功能。今天是除夕，耶！我们都知道新年前最常见的是著名的 10 秒倒计时，所以让我们来看看下面的新年倒计时功能:

```
**function** newYearsCountdown(number) {
  **for** (**let** i = 0; i >= 0; i--) {
    console.log(i)
  }
}
```

漂亮的循环。但是我们可以更有效地用递归来代替。让我们看看下面会是什么样子:

```
**function** newYearsCountdown(number) {
  console.log(number);
  newYearsCountdown(number - 1);
}
```

那么，这是如何工作的呢？我们将把它分解成 4 个步骤，以提供清晰的理解。

**第一步:**我们调用函数`newYearsCountdown(10)`，解析以 10(秒)为自变量。

**第二步:**我们将`number`打印到控制台。这里我们看到的是倒计时过程。

**步骤 3:** 在`newYearsCountdown`函数完成之前，它调用`newYearsCountdown(9)`，因为`number — 1`将等于 9，因为我们从参数 10 开始。

**步骤 4:** `newYearsCountdown(9)`开始运行，然后将 9 打印到控制台。在`newYearsCountdown(9)`完成之前，它由于`(number — 1)`而调用`newYearsCountdown(8)`，并且该过程继续下去。

## 它停在哪里？🛑

现在，如果我们继续这个函数，就像我们写的那样，我们实际上会超过零，这不是我们想要的！

为了完善我们的函数，我们可以添加一个条件语句来防止我们超过零。让我们来看看新的解决方案:

```
**function** newYearsCountdown(number) {
 console.log(number);
 **if** (number === 0) {
   **return**;
 } **else** {
   newYearsCountdown(number - 1);
 }
}
```

现在，当`number`等于`0`时，我们将不再调用该函数，而只调用`return`来阻止调用`newYearsCountdown`。

## 阅读📖写✍🏼

熟悉递归需要一些时间，但这里有两个技巧会派上用场:

1.  **阅读递归代码**——有两件事需要注意。基本情况和递归情况。我们在寻找什么样的基本情况，递归情况如何最终达到这个结果？
2.  **写递归代码** —将思路从循环切换到递归。对通常使用循环的简单任务执行递归。将这些任务升级为更复杂的任务，为你的成就给自己一个鼓励！

我希望这篇关于递归的小文章对你的编程之旅有所帮助，你会发现实现递归的有用方法，从而变得更加高效。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)