# React 钩子:最终指南(使用状态/使用效果)

> 原文：<https://javascript.plainenglish.io/react-hooks-the-ultimate-guide-usestate-useeffect-cdb3b1ce19c4?source=collection_archive---------4----------------------->

![](img/4a0dc61df0c9a79e32da46f20611d790.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你不是 React 新手(或者这些年一直住在山洞里)，你可能听说过 React hooks。我在这里的目的不仅是介绍它，而且是展示如何使用它来避免 React 经常发生的许多不必要的重新渲染。

# 基本的东西

## 什么是钩子？

*“React 钩子是 React 16.8 中引入的，允许我们在不使用类的情况下使用状态和其他 React 资源。”*

好吧，但那是什么意思？基本上，React 将允许更新变量值，并将触发这些变化，所以我们可以在屏幕上看到一些特定的动作发生时的结果。

## 什么是 DOM？

我知道。更多理论？为什么不直接看例子呢？

因为在使用前端时，理解这一点非常重要。DOM(文档对象模型)是加载网页时创建的浏览器元素的树对象。这个 DOM 表示整个页面及其元素(div、图像、文本等)。

## 使用状态

让我们创建一个计数器和一个给它加 1 的按钮。如果我们用 JavaScript 的方式来做，那么:

屏幕上什么都不会改变。为什么？因为 DOM 已经呈现了，即使您更改了`counter`的值，也不会在 DOM 上更新。

这一刻就是`useState`出现的地方。这个钩子将返回给我们一个有两个值的数组。第一个是您将使用的值，第二个是将更新该值的函数，如下所示:

现在我们有了一个可以工作的计数器！

让我更深入地解释一下正在发生的事情:

*   `counter`是我们将在屏幕中显示的值
*   `setCounter`是更新`counter`值的函数
*   `useState(0)`中的`0`是计数器的初始值
*   `setCounter((oldCounter) => oldCounter + 1)`是更新计数器值的函数。当使用这个函数时，我们有两个选择:像`setCounter(1)`一样返回我们想要的值，或者我们可以返回一个函数来获取我们状态的旧值(就像我们所做的)

很简单，对吧？！

## 使用效果

*“use effect 允许我们在功能组件中执行效果。获取数据、设置订阅以及在 React 组件中手动更改 DOM 都是副作用的例子。”*

它的作用基本上是让我们在特定状态改变时运行一些功能。`useEffect`接收两个参数:第一个参数是一个函数，它将在每次指定的一个状态发生变化时运行，第二个参数是一个数组，它包含了我们想要检查它是否发生变化的所有状态。

现在，让我们假设，如果计数器能被 2 整除，我们也想得到信息。一种方法是使用 useEffect:

所以在这段代码中，每次`counter`状态改变时，它都会运行函数`updateIsDivisibleByTwo`，就像这样简单。如果你已经在你的项目中配置了`eslint`(你应该这样做),它会告诉你

```
React Hook useEffect has a missing dependency: updateIsDivisibleByTwo. Either include it or remove the dependency array. (react-hooks/exhaustive-deps) eslint
```

发生这种情况是因为`updateIsDivisibleByTwo`可以在渲染之间改变，并且 linter 阻止我们引用那种“陈旧数据”。

我将在我们下一篇讨论 useCallback 和 useMemo 的文章中解释如何解决这个问题。

希望有所帮助！

干杯！

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费周报*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*