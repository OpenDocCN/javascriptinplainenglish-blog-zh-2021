# 构建一个自定义的 useFetch React 挂钩

> 原文：<https://javascript.plainenglish.io/creating-your-first-custom-hook-b44bf7e8892c?source=collection_archive---------13----------------------->

## 学习用简单易行的步骤构建你的第一个定制钩子

![](img/dc952caad4a00375a69a61e79f4d839f.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在我们开始创建我们的第一个定制钩子之前，我们需要有一些关于什么是钩子以及我们为什么使用它们的基本知识。如果你对 React 中的钩子不熟悉，可以点击[这里](https://pmehta18.medium.com/hooks-in-react-7ce87519a4ca)了解更多。🚀

## 什么是自定义挂钩

自定义挂钩是提供重用有状态逻辑的机制的函数，这样自定义挂钩中使用的所有状态和效果都保持完全隔离。我们也可以在一个自定义钩子中使用其他钩子。所有自定义钩子的名字应该以“use”开头，类似于其他钩子。

## 为什么要使用定制挂钩

*   允许共享可重用逻辑
*   不在组件之间共享数据
*   易于从组件中分离复杂的逻辑

## 如何构建自定义挂钩

***用例:*** *我们已经构建了从 API 获取数据的应用程序。在这样做的时候，我们通常会显示一个加载指示器，这样用户就可以知道一些事情正在进行中，可能很快就会加载。如果我们在获取数据时收到任何错误，我们会显示错误提示消息。*

***实现:*** *我们将创建一个名为“useFetch”的自定义钩子，它将进行 API 调用，并管理加载和错误状态。只要我们想使用 API 调用获取数据，就可以重用这个钩子，而不需要在任何地方单独管理加载和错误状态。*

useFetch hook

在上面的代码片段中，我们创建了一个名为“useFetch”的定制钩子，在这里我们将接收 API 端点。钩子将管理从 API 调用接收的加载、错误和响应的状态。它将管理对给定端点进行 API 调用的代码。最后，我们将简单地将这些状态值返回给调用函数。

using the useFetch hook

在上面的代码片段中，我们将根据从钩子接收的值显示一个加载指示器和一个错误提示。在这个定制钩子的帮助下，我们不需要管理每个 API 调用的错误和加载状态，因为它是由钩子本身管理的，并且在钩子中保持完全隔离。

## 资源

*   你可以在这里找到完整的源代码。
*   现场演示:[https://lwj09.csb.app/](https://lwj09.csb.app/)

请在评论区分享你最喜欢的定制挂钩！

这就是你的第一个定制钩子，伙计们！编码快乐！👩‍💻