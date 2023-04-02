# 如何在类型脚本中创建队列

> 原文：<https://javascript.plainenglish.io/how-to-make-a-queue-in-typescript-b56416970670?source=collection_archive---------8----------------------->

如何使用类型脚本制作队列数据结构

![](img/6bc153a943e75895d5dc74fd50487cd1.png)

Photo by [Maxwell Nelson](https://unsplash.com/@maxcodes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

无论您是哪种类型的开发人员，前端还是后端，对不同类型的数据结构及其用例有基本的了解都是很重要的。今天我们将讨论其中一个数据结构。**队列。**

# 什么是队列？

虽然我已经在我的文章 [4 中讨论了队列是什么，但是每个开发人员都应该知道的数据结构](https://bookeraziz.medium.com/4-data-structures-every-developer-should-know-368d156ea384)我将提供一些基本概念的快速复习。

队列是一种遵循先进先出(FIFO)原则的数据结构。这意味着放入队列的第一个元素——通常是一个数组——也是第一个离开队列的元素。这意味着队列先到先得

有两个与队列相关的主要功能:*入队*和*出列。*排队是向队列末尾添加新元素的过程。另一方面，出列是取出队列的第一个元素并将其返回的过程。

默认情况下，这些函数是不提供的，所以我们作为开发人员必须自己实现这些函数。

# 声明队列类

创建队列的第一步是创建一个 typescript 类。代码如下:

这段代码将允许我们保存任何类型的值的数组，不管它们是字符串、整数，甚至是 javascript 对象。构造函数中的 params 对象将允许我们在初始化时用任意数量的值填充 items 数组。

# 添加排队方法

下一步是向我们的队列添加排队功能。这可以通过使用阵列轻松实现。Push()方法将值添加到队列的末尾。其代码如下所示:

太好了。既然我们添加了这个，我们就可以向队列中添加更多的项目。下一步是将出列方法添加到*中，从队列的前面移除*项。

# 添加出列方法

我们将使用另一种数组方法来实现出列方法。这一次，我们将使用阵列。方法移除并返回数组中的第一个元素。代码如下:

# **添加显示项目的方法**

接下来的两个方法对于实现队列来说不是必需的，但是仍然有用。这个简单的方法将返回项数组的内容。代码如下:

有了这个，我们已经成功地使用 TypeScript 创建了一个队列！

# 结论

感谢您读到我关于**“如何在 TypeScript** 中创建队列”的文章末尾。我希望你有一个伟大的一天。下面是我的一些进一步的文章供你阅读:

[](/five-great-resources-to-learn-web-development-617aee7b1aea) [## 5 个学习网络开发的好资源

### 学习网络开发没必要这么紧张。

javascript.plainenglish.io](/five-great-resources-to-learn-web-development-617aee7b1aea) [](https://medium.com/aziz-booker/7-javascript-libraries-you-need-to-know-about-27d6e9f1b0d9) [## 你需要了解的 7 个 Javascript 库

### Javascript 库将提高您作为 web 开发人员的效率

medium.com](https://medium.com/aziz-booker/7-javascript-libraries-you-need-to-know-about-27d6e9f1b0d9) [](/how-to-make-scroll-based-animation-in-javascript-using-gsap-cfd65e7cc81f) [## 如何使用 GSAP 制作基于滚动的 JavaScript 动画

### 如何使用 GSAP 动画库来制作动画？

javascript.plainenglish.io](/how-to-make-scroll-based-animation-in-javascript-using-gsap-cfd65e7cc81f) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)