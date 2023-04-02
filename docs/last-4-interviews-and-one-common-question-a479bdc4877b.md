# 最后 4 次采访和一个常见问题😁😎

> 原文：<https://javascript.plainenglish.io/last-4-interviews-and-one-common-question-a479bdc4877b?source=collection_archive---------11----------------------->

如何开发一个具有无限滚动功能的类似 Twitter 的主页

![](img/d16aead147490b82337f95dcd03d0b1e.png)

Photo by [Steve Halama](https://unsplash.com/@steve3p_0?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 在后台

在我最近的 3-4 次面试中，我遇到了一个围绕一个单一概念的问题。我想分享这个错误的答案，这个答案帮助我澄清了今天故事中的采访。

## 概观

这个问题很简单。

你必须开发类似 Twitter 的主页，作为一个全栈开发人员，你的全部和唯一责任是在考虑性能的情况下执行后端和前端解决方案。

这听起来可能很难，但是再读一遍这个问题，他们不是告诉你去多详细，只是确保基本的技术细节都包括在内。此外，他们非常重视表现，这意味着如果你能在这个领域回答，你很有可能通过这一轮。

## 入门指南

让我们不要浪费时间，开始解决问题。

## 前端解决方案

我们在前端有无限的滚动，这意味着每条推文有无限的卡片。我想到的唯一概念是，除了通过使用缓存机制和纯组件来避免多次重新渲染之外，我们在前端没有什么可以做的。

为了处理大尺寸的图像，我们可以执行延迟加载和 CDN 来加载图像。要添加无限滚动，我们肯定需要添加滚动分页或窗口的概念。

分页和窗口是在前端处理大型数据集的两个强大的概念。它们确保仅在获取时加载下一个项目，并且仅在项目出现在屏幕视图中时呈现项目。这个完整的概念稍微提高了性能。

前端解决方案并不是火箭科学，如果您更多地阅读和研究性能，您可能会找到相同的解决方案。所以回答这些问题会有所帮助，但不一定能让面试顺利进行。

接下来的部分是让我完全放心的部分。让我们来谈谈后端解决方案—

## 后端解决方案

这是派对开始的地方😁在回答我将选择的 DSA 时，我也很紧张，因为我对数据结构和算法感到不太舒服。

## 关键因素

让我们从 API 和结构开始，我们必须发送 tweets，并且数量不受限制，因此必须有分页以提高性能。

接下来要注意的是，与其用一个 API 来发送前 10 条推文的全部数据，不如我们只发送推文 id。

您还可以使用压缩数据的概念来发送大量数据。这意味着我们可以压缩前 10 条 tweets 的 JSON 数据，然后发送给客户端作为响应。这是相当强大的，但老实说，我没有提到这个解决方案😁。

## 设计数据结构

一旦你提到关键因素，他们肯定会要求你打开 IDE 或编辑器来绘制 DSA 或设计 tweet API 的对象。

这也不是太难，但是思考这个解决方案需要一些实践，甚至是一个想法。因此，在今天的故事中，您了解了如何在后端服务中扩展这些解决方案的基本概念。

## 分解解决方案

让我们打破上述解决方案。首先，我们从 params 中的用户获取页码，声明他/她想要哪个页面的数据或 tweets。然后，我们只从数据库中获取特定页面的 tweets。完成后，我们可以将数据以 zip 格式或 JSON stringify 格式发送给客户端。

为了继续获取接下来的 10 个项目，客户端必须再次创建一个 API，但是这次使用 page = 2，我们对 page number 重复上面的步骤。

## 在前端执行解决方案

另一个反问题是如何在前端执行这个 API 调用特性。这也很简单，以下是操作步骤-

*   首先，我们将对 page = 1 进行 API 调用，并获取 10 条 tweets
*   然后，一旦用户向下滚动到屏幕高度的 50–70 %,我们将把页面值增加 1，并进行另一个 API 调用。
*   为了使前端更具性能，我们将使用窗口的概念，这意味着我们将只呈现那些在屏幕上可见的项目，而其余所有推文都将被卸载。

我建议你读两遍这个故事，即使你第一遍就明白了。这可能看起来太简单了，但是只有当你完全理解它的时候，你才能 100%确定你理解了。此外，一旦你执行了它，你甚至可以回答你肯定会遇到的反问题，这在今天的故事中我没有提到😁。

## 结论

今天就到这里，各位，我们看看接下来要讲什么。我希望你喜欢分享面试问题的概念，这有助于你理解和学习职业世界是如何工作的。

直到，下一次，有一个美好的一天，人们。

```
For more visit our website 💻 [**iHateReading**](http://www.ihatereading.in)
```

## 更多阅读

[](https://medium.com/geekculture/5-tips-for-perfect-landing-page-b235b6bb0fb7) [## 完美登录页面的 5 个技巧

### 为了一个稳定的登陆页面，注意这 5 件事

medium.com](https://medium.com/geekculture/5-tips-for-perfect-landing-page-b235b6bb0fb7) [](https://medium.com/nerd-for-tech/5-steps-to-develop-custom-tabs-in-react-d0ec1c05d3af) [## 在 React 中开发自定义选项卡的 5 个步骤

### 不需要依赖 UI 库来使用选项卡

medium.com](https://medium.com/nerd-for-tech/5-steps-to-develop-custom-tabs-in-react-d0ec1c05d3af) [](https://medium.com/geekculture/the-full-stack-repository-for-mobile-application-7932853a8185) [## 面向移动应用的全栈存储库

### React Native 中的入门 Firebase

medium.com](https://medium.com/geekculture/the-full-stack-repository-for-mobile-application-7932853a8185) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)