# 如何使用 AbortController 通过 JavaScript Fetch API 设置超时

> 原文：<https://javascript.plainenglish.io/how-to-set-api-timeout-with-javascript-fetch-api-2d7c95782fa9?source=collection_archive---------1----------------------->

![](img/6fdc287840f6393834ac42163875eea9.png)

Photo by [Jose Aragones](https://unsplash.com/@jodaarba?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/stop?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

最近，我一直在构建需要对服务器进行 API 调用的示例项目。我选择了 JavaScript Fetch API，因为我不想用外部库和管理依赖项来膨胀我的应用程序。在测试其中一个项目时，我失去了互联网连接，应用程序在进行 API 调用时被卡住，它没有超时或显示适当的错误。

考虑到这一点，我研究了 Fetch API，看它是否在其接口、请求体或头中支持超时。不幸的是，它没有其他基于承诺的 HTTP 客户端支持的超时选项。

An example of [Axios](https://axios-http.com/)’s timeout option

在本帖中，我们将讨论如何在使用 Fetch API 时使用 AbortController 来设置超时。我们将使用 React 开发我们的前端应用程序。(*注意:您可以在其他前端库/框架上使用相同的方法。*)。

# 沙箱

我们在一个 [Codesandbox](https://codesandbox.io/s/magical-wave-53dgk?file=/src/App.js:173-217) 中完成了这个项目，你可以派生它来运行代码。

# 让我们编码

在开始之前，我们需要了解什么是**人工控制器**以及它是如何工作的。AbortController 是一个对象，它允许我们在需要时中止一个或多个 web 请求。它包含一个`signal`属性和一个`abort`方法，用于根据需要分别传递和停止请求。

没有超时的`fetch`函数如下所示:

using the Fetch API without a timeout

## **集成人工控制器**

为了将 AbortController 与`fetch` API 集成，我们需要创建一个`Timeout`函数，如下所示:

using the abort contoller

上述代码执行这些任务:

*   创建一个`Timeout`函数和一个 AbortController 实例。
*   使用`setTimeout`函数在指定时间后触发`abort`方法(通过乘以 1000 转换为秒)并返回控制器。

最后，要使用`timeout`函数，我们需要修改`fetch`请求对象`signal`，如下所示:

updated App.js with a timeout of 10 seconds

# 结论

这篇文章讨论了在用 Fetch API 调用 REST API 时，如何使用 AbortController 设置超时。

**参考:**

*   [获取 API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
*   [流产控制员](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)

*更多内容看*[***plain English . io***](http://plainenglish.io/)