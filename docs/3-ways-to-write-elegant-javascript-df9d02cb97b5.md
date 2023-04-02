# 编写优雅 JavaScript 代码的 3 种方法

> 原文：<https://javascript.plainenglish.io/3-ways-to-write-elegant-javascript-df9d02cb97b5?source=collection_archive---------1----------------------->

## 是时候结束意大利面代码了。

![](img/8399a2a55dae6bbc939da030cabc19df.png)

Photo by [Christopher Robin Ebbinghaus](https://unsplash.com/@cebbbinghaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

每当我完成一个项目或者查看一些旧代码时，我总是试图找到重构和提高可读性的方法。实现这一点的方法可以包括编写定制的 React 钩子，将重复的代码封装到子例程中，等等。在本文中，我将分享三种模块化和提高代码可维护性的常用方法。让我们开始吧。

# **1。使用打字稿**

这可能会让一些人感到惊讶，但是 TypeScript 减轻了许多在某些情况下使 JavaScript 成为不安全语言的问题。这也使你的代码意图更加清晰。让我们看一个简单 React 组件`People`的 JavaScript 示例:

我们在这里可以看到，`People`接受了`peopleList`作为道具，这是一个对象列表，每个对象代表一个将被渲染为`<ListItem />`的人。所有这些都很好，但是如果其中一个人的财产丢失了呢？如果一个人的职业或薪水是`undefined`呢？你们中的许多人可能认为我们可以使用`prop-types`来处理这个问题，但是在我看来，TypeScript 提供了一个更好的解决方案。让我们看看用 TypeScript 编写的同一个`People`组件:

在这个例子中，我们定义了一个带有可选属性的接口`Person`。)通知编译器`peopleList`中的人可能只包含`Person`中属性的子集。我们还定义了一个`PeopleProps`接口，它指定了 prop `People`应该接收的类型，这是一个`Person`数组。因此，`People`组件更加灵活和坚固。

# **2。使用指纹**

如果您熟悉立即调用函数表达式(IIFE ),那么您肯定知道它们作为一种将两个语句合成一个语句的简洁方法是多么有用。假设您想用一些外部数据初始化一个数组:

在这个例子中，我们定义了一个函数`initList`，它返回一个包含外部数据的数组。然后我们调用该函数并将结果存储在`dataList`中。这并不是说这段代码有什么问题，但它可以写得更优雅，就像这样:

这里，我们通过将`dataList`分配给一个立即被调用的匿名函数来节省几行代码。

# **3 .关注点分离**

将代码库中的功能问题分开总是很重要的，尤其是在处理日益复杂的项目时。让一个函数同时执行多个任务通常是不理想的，尤其是当它们彼此没有关系时。让我们来分析一个依赖于一些外部 API 数据的组件`Example`的不良反应示例:

这个例子不好的原因是因为`Example`组件应该只负责在屏幕上显示数据，而不是获取外部数据。这会造成混乱，并使组件更难调试。幸运的是，我们可以通过编写自己的钩子来解决这个问题，钩子包含了发出请求的逻辑。这个钩子将是一个接受 url 和选项的函数，发出 post 请求，并返回如下数据:

既然调用 API 的所有逻辑都在这个自定义钩子中，我们的`Example`组件现在看起来如下:

随着`usePost`对请求后逻辑的抽象，现在`Example`组件只负责显示数据。通过做出这种改变，代码库变得更加容易维护。

如果你来了，谢谢你的阅读！我希望你觉得这篇文章很有见地。祝您一天愉快。

*更多内容参见* [*简明英语. io*](http://plainenglish.io/)