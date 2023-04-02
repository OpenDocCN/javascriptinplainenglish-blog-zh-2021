# 关于 JavaScript 中的模板文字，您需要知道的一切

> 原文：<https://javascript.plainenglish.io/everything-you-need-to-know-about-template-literals-in-javascript-67590a99a132?source=collection_archive---------13----------------------->

模板文字的基础知识以及为什么应该使用它们。

![](img/88bdd8280277ba63cb3bdcc9dc20d356.png)

Photo by [Zany Jadraque](https://unsplash.com/@jenrielzany?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您曾经不得不在 JavaScript 中插入字符串的值，您可能不得不使用这样的语法:

虽然这段代码运行得非常好，并将正确的字符串打印到控制台，但是有一种方法可以让我们以更简洁的方式获得相同的结果。这可以通过使用**模板文字来实现。**

# 什么是模板文字？

模板文字是 ES6 的一个特性，它为开发人员提供了一种在 JavaScript 中声明字符串的新方法。不使用引号或双引号，而是使用反斜线来定义模板文字。反斜线的使用并不是普通字符串和模板文字之间的唯一区别。模板文字提供了比普通字符串更多的特性。其中一些特性包括但不限于编写多行字符串的更简单方法和插值的更简单方法。

Normal String vs Template Literals

# 模板文本中的多行字符串

模板文本字符串和普通字符串的第一个区别是换行字符的书写方式。在普通字符串中，你必须使用转义符，' **/n '，**来跳到下一行。

在模板文字中，编写多行字符串的方式要简单得多。你所要做的就是把这个单词写在下一行。

这可能很难理解，所以请看下面的代码:

这两个代码将包含相同的字符串。你好，纽林。*然后是*名字，在这里是 Aziz。

在我看来，这使得用模板文字编写多行字符串更加直观，就像用普通英语编写一样。通过添加空格和制表符。

# 在模板文本中插值

下一个特性可能是最常用的模板文字。

字符串中值的简单插值。

如果你看看简介中的代码片段，你会看到在字符串中插入值的正常方法。这还不错，但还可以做得更好。

模板文字为这种插值提供了一种更好的语法，因为您所要做的就是在括号内放置一个美元符号，而不是一个带您想要插值的值的左右括号。

其语法如下所示:

这个值将打印正确字符串的返回结果，在本例中是' Hello Aziz ',没有任何额外的麻烦。

# 结论

感谢您阅读完我的文章**“关于 Javascript** 中模板文字您需要知道的一切”。我希望你有美好的一天。以下是我的一些进一步的文章供你阅读:

[](/five-great-resources-to-learn-web-development-617aee7b1aea) [## 学习 Web 开发的 5 大资源

### 学习 web 开发没必要这么紧张。

javascript.plainenglish.io](/five-great-resources-to-learn-web-development-617aee7b1aea) [](https://medium.com/aziz-booker/7-javascript-libraries-you-need-to-know-about-27d6e9f1b0d9) [## 你需要了解的 7 个 Javascript 库

### Javascript 库将提高您作为 web 开发人员的效率

medium.com](https://medium.com/aziz-booker/7-javascript-libraries-you-need-to-know-about-27d6e9f1b0d9) [](/how-to-make-scroll-based-animation-in-javascript-using-gsap-cfd65e7cc81f) [## 如何使用 GSAP 制作基于滚动的 JavaScript 动画

### 如何使用 GSAP 动画库来制作动画？

javascript.plainenglish.io](/how-to-make-scroll-based-animation-in-javascript-using-gsap-cfd65e7cc81f) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)