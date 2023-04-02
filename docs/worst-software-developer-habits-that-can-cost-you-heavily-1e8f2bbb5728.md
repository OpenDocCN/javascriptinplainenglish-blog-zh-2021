# 让你付出沉重代价的最糟糕的软件开发习惯

> 原文：<https://javascript.plainenglish.io/worst-software-developer-habits-that-can-cost-you-heavily-1e8f2bbb5728?source=collection_archive---------8----------------------->

## 避免这些可笑的错误。

![](img/07a4d3d453b3869d8c07abfe483ddf94.png)

Photo by [Nik Shuliahin](https://unsplash.com/@tjump?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编写一段代码对几乎每个程序员来说都是轻而易举的事情，但是，你的代码能自己说话吗？

最近，我的一个朋友通过 **GitHub** 与我分享了他的 JavaScript 代码，事实是我无法理解他到底写了些什么。我的 JavaScript 知识足以理解官方 [**文档**](https://developer.mozilla.org/en-US/docs/Web/JavaScript) 或 [**教程**](https://www.w3schools.com/js/DEFAULT.asp) 中的任何片段。但是，我的朋友犯了非常可笑的错误，使得他的代码完全不可读。

**以下是用任何编程语言编码时都应该避免的重要方面—**

## 不使用缩进

如果你是一个使用 Python 作为编程语言的开发人员，那么你会知道缩进的重要性。

缩进只不过是代码的一个新的相似部分前的一个**空格。当你使用 Python 时，这是必须的，否则你的代码会给出数百个错误。但是，另一种编程语言，如 C++或 Java，并不强迫你使用适当的缩进。所以如果缩进不是你的编程语言所必须的，为什么还要担心缩进呢？**

咄…这样人们可以阅读你的代码，而且通过适当的缩进，你可以专注于代码的任何部分。它还可以帮助您编辑代码，或者将代码片段的一部分转移到另一个文件中。

```
**Without Indentation your code will look like-**for(int i=0;i<3;i++){cout<<"What the heck?"<<endl;cout<<"This is how I write my Code"<<endl;}**With Proper Indentation-**for(int i=0;i<3;i++){
    cout<<"What the heck?"<<endl;
    cout<<"This is how I write my Code"<<endl;
}
```

正如你所看到的**通过适当的缩进**你的代码变得更加易读，如果需要的话，你可以在将来很容易地调试它。请注意，如果您和您的团队成员正在处理同一个项目，那么使用标准实践将最适合您，因为会有许多代码片段的交换。

## 不使用驼色外壳

如果发现使用 camel-case 是编写程序时最标准的做法。Camel Case 就是在你声明的任何变量的开头使用一个大写字母。

如果你和你的队友在同一个项目中工作，并且你们都在编辑代码的特定部分，那么你应该记住在声明一个新变量时使用 camel case。此外，只对要声明的变量使用合适的名称

```
**Without Camel Case-**string firstnameoflocaluser = "Aniket"; **With Camel Case-**string FirstNameOfLocalUser = "Aniket";
```

正如你所看到的，使用 Camel Case 你的代码的可读性增加了很多，在声明变量的时候也不要使用任何类型的短名称。我的一个朋友在声明一个变量时使用了 x 字母，当你实际上在一个项目中工作时，使用一个单词会引起很多混乱。

这些是大多数软件开发人员使用的一些标准实践。另外，记得在需要的地方使用**注释**。有时在 C++中，避免使用名称空间 std 声明**，如果您正在合并多个项目，则在需要的地方使用 **std** 。**

我希望你喜欢这篇文章，只是记得写一个整洁干净的程序，并为你自己和你的队友保持一个标准的实践。坚持练习，坚持编程！

[](https://aniketz.medium.com/membership) [## 通过我的推荐链接加入 Medium-Aniket

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

aniketz.medium.com](https://aniketz.medium.com/membership) [](/3-books-every-programmer-should-read-97ac12422cfb) [## 每个程序员都应该读的 3 本书

### 帮助我理解编程基础的书籍。

javascript.plainenglish.io](/3-books-every-programmer-should-read-97ac12422cfb) [](/top-10-programming-languages-of-2021-d2d48c634ae7) [## 2021 年十大编程语言

### 你是使用顶级编程语言的用户之一吗？

javascript.plainenglish.io](/top-10-programming-languages-of-2021-d2d48c634ae7) [](https://blog.devgenius.io/how-i-went-from-noob-to-expert-in-python-programming-8c4e141a0be1) [## 我是如何从新手成为 Python 编程专家的

### 我一直使用的资源汇编

blog.devgenius.io](https://blog.devgenius.io/how-i-went-from-noob-to-expert-in-python-programming-8c4e141a0be1) [](https://blog.devgenius.io/inbuilt-data-structures-every-developer-should-know-2c2cb513193a) [## 每个开发人员都应该知道的内置数据结构。

### 易于实现的便捷数据结构

blog.devgenius.io](https://blog.devgenius.io/inbuilt-data-structures-every-developer-should-know-2c2cb513193a) [](/3-weird-things-i-bought-as-a-programmer-5ab5bf90ed73) [## 我作为程序员买的 3 样奇怪的东西

### 我希望我开始编程的时候能轻松一点

javascript.plainenglish.io](/3-weird-things-i-bought-as-a-programmer-5ab5bf90ed73) 

对于任何**“赞助/写作项目”**你可以通过—**writeaniketz@gmail.com**联系我

*更多内容请看*[***plain English . io***](http://plainenglish.io/)