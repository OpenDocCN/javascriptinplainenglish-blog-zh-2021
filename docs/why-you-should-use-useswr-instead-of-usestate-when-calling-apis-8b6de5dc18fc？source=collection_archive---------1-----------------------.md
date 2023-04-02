# 为什么在调用 API 时应该使用 useSWR 而不是 useState

> 原文：<https://javascript.plainenglish.io/why-you-should-use-useswr-instead-of-usestate-when-calling-apis-8b6de5dc18fc?source=collection_archive---------1----------------------->

![](img/6b2d9a2da6462b2563c31cdfc2b2045f.png)

# 什么是 SWR？

SWR(重新验证时的状态)是一个用于从服务器获取数据的反应钩子。SWR 从缓存中提供数据，然后制作一个服务器进行验证，一旦验证完成，它就会组合数据以实现数据一致性。

我们可以使用 NPM 安装命令安装 SWR。

```
npm install swr
```

# 如何使用它？

SWR 是一个简单的反作用钩子，它返回数据以及对象模型中的错误。

以下是取自官方网站的例子。

# SWR 提供的特色

SWR 提供了大量的性能、正确性和稳定性方面的特性来构建用户体验更好的应用程序。

## 表演

SWR 是下一个建造的。高性能的 JS 团队。它有构建缓存系统和 [**重复数据删除**](https://swr.vercel.app/advanced/performance#deduplication) 系统，可以跳过不必要的网络。由于它是一个反作用钩子，它可以避免由于网络调用而导致的不必要的重新渲染。

所以好处是:

*   *无不必要的要求*
*   *无不必要的重渲染*
*   *无不必要的代码导入*

# 预取数据

您可以通过添加`<link ref="preload" href="..."/>`来预取数据。但是在某些情况下，您需要以编程方式预取数据。

SWR 提供了一个以编程方式预取数据的选项。

# 错误处理

错误处理对于任何提供更好用户体验的应用程序来说都是至关重要的。`SWR`提供了一个全局处理错误的选项，这减少了最终构建中的大量代码。

请尝试使用`SWR`，它会在很多方面提高你的应用性能。

# TL；速度三角形定位法(dead reckoning)

在 React 应用程序中，我们通常使用`useState`和`fetch`来获取数据和呈现内容。如果我们使用`[useSWR](https://swr.vercel.app/)`，它通过从缓存中提供数据来提供更好的性能，然后发送一个调用来验证，最后结合两个数据源来实现数据一致性。

办公地点:[https://swr.vercel.app/](https://swr.vercel.app/)

**感谢您的阅读！**如果你喜欢这个，考虑一下在推特上关注我，并和你的开发者朋友分享这篇文章。

*多内容见于* [***中***](http://plainenglish.io)