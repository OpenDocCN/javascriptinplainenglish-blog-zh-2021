# 为什么需要了解 JavaScript 中的一级函数

> 原文：<https://javascript.plainenglish.io/why-you-need-to-know-about-first-class-functions-in-javascript-e83cde6ae578?source=collection_archive---------22----------------------->

打开了进一步理解 JavaScript 函数的大门

![](img/bff770c01007e0a315e80937e34602af.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

首先，让我澄清一些事情。本文将与飞机头等舱座位无关。相反，今天我们将讨论 Javascript 中的一级函数，这是每个 JavaScript 开发人员都需要知道的，因为它是理解回调和高阶函数等其他概念的基础。

# 什么是一流的功能？

一流的函数可以在很多语言中找到，比如 Python、Scala、Haskell，当然还有 JavaScript。本质上，一级函数是可以像对待其他变量一样对待的函数。要被认为是一流的函数，函数必须能够做到以下几点:

1.  赋给变量
2.  作为参数传递给函数
3.  由函数返回

现在我们将检查 JavaScript 中的函数是否满足成为一流函数的所有标准。

# 将函数分配给变量

现在我将向你展示 Javascript 中的函数**可以**赋给变量**。**为了证明这一点，我将创建一个名为 greet 的函数，它返回“Hello ”,然后将它赋给一个名为 greetOne 的变量。

从这个 Github 要点中，你可以看到我们将 Greet 分配给 greetOne，然后通过编写 *greetOne()调用它。*

这是一个在 javascript 中将函数赋给变量的例子，这意味着 JavaScript 中的函数满足成为一流函数的三个标准之一。

# 将函数作为参数传递

证明 JavaScript 中的函数可以作为参数传递。我将修改我们的 Greet 函数来接受两个参数。第一个参数是一个名字，第二个参数是接受一个函数的 *GreetMessage* 。这个新的和改进的 Greet 函数将返回一个包含 GreetMessage 和名称的字符串。代码如下:

如果您运行这段代码，您会看到它打印出“Hello There Aziz ”,这意味着该函数满足分类为一级函数所需的 3 个标准中的 2 个。

# 将函数作为参数返回

现在是时候看看 JavaScript 函数是否真的是一流的函数了。我要最后一次修改代码。这次我将把 GreetMessage 函数嵌套在 Greet 函数中。

现在，如果您运行这段代码，它将正确无误地运行。至此，我们已经展示了 JavaScript 中的函数确实是*一级函数*

# 结论

希望现在您已经很好地理解了为什么 JavaScript 中的函数是一级函数。这将在理解 JavaScript 的其他关键领域打开一扇新的理解之门。

感谢您阅读完我的文章**“为什么您需要了解 JavaScript** 中的一级函数”。我希望你有美好的一天。以下是我的一些进一步的文章供你阅读:

[](/how-to-make-scroll-based-animation-in-javascript-using-gsap-cfd65e7cc81f) [## 如何使用 GSAP 制作基于滚动的 JavaScript 动画

### 如何使用 GSAP 动画库来制作动画？

javascript.plainenglish.io](/how-to-make-scroll-based-animation-in-javascript-using-gsap-cfd65e7cc81f) [](https://medium.com/aziz-booker/7-javascript-libraries-you-need-to-know-about-27d6e9f1b0d9) [## 你需要了解的 7 个 Javascript 库

### Javascript 库将提高您作为 web 开发人员的效率

medium.com](https://medium.com/aziz-booker/7-javascript-libraries-you-need-to-know-about-27d6e9f1b0d9) [](https://blog.devgenius.io/10-vs-code-shortcuts-every-developer-should-know-f2d1058cfe8e) [## 每个开发人员都应该知道的 10 个 VS 代码快捷键

### 简单的快捷方式可以极大地提高你的生产力

blog.devgenius.io](https://blog.devgenius.io/10-vs-code-shortcuts-every-developer-should-know-f2d1058cfe8e) 

*更多内容尽在*[plain English . io](http://plainenglish.io/)