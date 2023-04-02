# 本地应用反应缓慢的 6 个原因

> 原文：<https://javascript.plainenglish.io/react-native-performance-dos-and-don-t-c3de8739e0a8?source=collection_archive---------2----------------------->

## 以及如何改善。反应本地性能做什么和不做什么

![](img/11f056d2d19abbb7c491fee624bcd9d5.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

反应本机应用程序在大多数时候真的很慢。大量的列表、图像、资产、API 响应和多重渲染、剖析、记忆、延迟加载，在改进应用程序性能的过程中，我遇到了这么多术语。

深入理解应用程序速度慢的原因并不是一件容易的事情，您也不能轻易地追溯出是哪个模块造成了性能问题。

## 衡量绩效？

测量 React 本机应用程序性能的最佳方法是使用 Perf monitor 了解 JS 线程及其每秒帧数。React native 依靠一个 Native 桥来对话 android 和 ios 软件的 Native 层。JS bridge 和本机软件之间的每个对话都被视为一个单独的框架。

任何类型的用户活动，如触摸事件和 API 响应以及 UI 中基本组件的呈现，都会直接影响帧速率和 JS 线程。所以你的 API 响应需要更多的时间，JS 线程会被阻塞，更多的帧会被丢弃，因此用户会感觉应用程序很慢或滞后。

API 或组件渲染的任何响应超过 100 毫秒将使帧速率降低 12。因此，您必须注意在 react 应用程序中的特定时间和位置应该调用哪个特定的 API。

许多开发人员仍然认为功能组件比类组件慢，所以他们倾向于在整个应用程序中进行转换。嗯，这只是一个神话，没有这样的研究或坚实的理由可以支持这个假设，这只是预测。

相反，这里是你的反应原生应用程序慢的原因。

## 1.减少重新渲染

这种情况下，降低帧速率的主要问题。大多数情况下，更新全局上下文会使用该上下文重新呈现最深的后代。

> 每当提供者的`value`属性改变时，作为提供者后代的所有消费者都将重新呈现。

这句台词在 [React-docs](https://reactjs.org/docs/context.html#contextprovider) 里面提到过。即使父组件的子组件 A 没有更新它的任何状态或属性，如果树中的任何组件将更新上下文 API，它也将被重新呈现。

您可以使用分析来计算渲染次数。通过简单地将 **onRender** 回调函数附加到主要组件上，你可以检查每个组件的渲染次数。

## 2.使用记忆

避免重新渲染就是记住组件。记忆化基本上是缓存数据，只有当他的状态或道具改变时才重新渲染。记忆化有助于组件不重新呈现，即使其附近的父组件属性或状态发生变化。

使用**使用记忆**和**使用回调**钩子你可以记忆组件。

## 3.使用纯组件

任何组件将是静态的，如图像，标题，标题应被视为一个纯粹的组件。尝试使这些组件成为一个纯粹的组件，这样可以避免多次渲染。

## 4.没有延迟加载和分页

如果您处理大量的数据和资产，总是喜欢添加分页和延迟加载。惰性加载有助于仅呈现视图中的组件，而分页有助于仅获取所需数量的数据。这两个过程都提高了性能。

## 5.停止过度提取数据

如果你处理实时图表，例如，股票市场，你倾向于在前端获取不需要的数据。过度获取不必要的数据将增加 API 响应时间，并最终降低帧速率，这又会导致性能问题。仅获取所需的数据将再次提高性能。

在前端做到这一点的一种方法是使用 GraphQL wrapper over REST API。这个包装器从 GraphQL 客户端调用 REST API，帮助 API 只返回所需的数据。

[](/calling-rest-api-inside-graphql-queries-e715c0f2da44) [## 在 GraphQL 查询中调用 REST API

### 您不需要将我们的后端从 REST 切换到 GraphQL，而是在 Graph QL 中获取 REST 查询。

javascript.plainenglish.io](/calling-rest-api-inside-graphql-queries-e715c0f2da44) 

## 6.在滚动视图上使用平面列表

我已经讲述了为什么 Flatlist 比 React Native 中的 ScrollView 组件更好。Flatlist 提供了延迟加载、分页功能，你可以使用简单的技巧，比如 useMemo 和 flatlist 中的纯组件，这样你就可以避免重新渲染。这些小变化大大提高了性能。

[](https://medium.com/nerd-for-tech/flatlist-is-still-underrated-796130a8b8f2) [## Flatlist 仍然被低估了

### 也许你使用 Flatlist 的方式是错误的，这里有一些提示和技巧

medium.com](https://medium.com/nerd-for-tech/flatlist-is-still-underrated-796130a8b8f2) 

## 摘要

*   避免重新渲染
*   使用记忆化和纯组件来避免不必要的渲染
*   添加延迟加载和分页来提高性能。
*   在前端实现 GraphQL over REST API，以避免数据的过量提取。
*   在 ScrollView 组件上使用 Flatlist

## 结论

我希望这个故事会有所帮助，因为我花了近一个月的时间来研究和了解为什么我的 React 本机应用程序很慢。更多这样的故事，请跟我来。直到，下一次，有一个美好的一天，人们。

```
For more reach our website 💻 [iHateReading](http://ihatereading.in/)
```

*更多内容尽在*[***plain English . io***](http://plainenglish.io)