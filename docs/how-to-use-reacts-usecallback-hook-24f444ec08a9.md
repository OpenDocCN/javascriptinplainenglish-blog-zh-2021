# 如何使用 React 的 useCallback 钩子

> 原文：<https://javascript.plainenglish.io/how-to-use-reacts-usecallback-hook-24f444ec08a9?source=collection_archive---------9----------------------->

React 中的 useCallback 钩子到底是什么，为什么要用它？在本文中，您将了解 useCallback 钩子到底是什么，它的优点是什么，以及如何使用它来优化应用程序的性能。听起来不错？让我们开始吧。

![](img/ece3ddcaeea65d0984f53f7d28d33d20.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 文档将 useCallback 钩子定义为“**一个记忆化的回调”。回调只是函数的一个花哨的名字。所以回调基本上是一段代码，它接受一个输入并返回一些信息。**

那么**记忆化**回调到底是什么意思呢？这意味着它被存储起来，不必在每次组件重新呈现时重新初始化。为了理解这一点，让我们以下面的例子为例:

那么这段代码发生了什么呢？首先，我们创建两个组件，一个 ParentComponent 和一个 ChildComponent。在 ParentComponent 中，在*第 4 行*上，我们初始化了一个函数，你必须想象这个函数执行一个 API 请求并返回结果。我们将这个函数传递给第 11 行上的 ChildComponent。然后，在我们的 ChildComponent 中，我们使用 useMemo 钩子进行了一次昂贵的计算，并将其存储在内存中。在*第 27 行*我们呈现了这个昂贵计算的结果。

这段代码的性能对您的应用程序来说可能是毁灭性的，您能猜到原因吗？

问题在于“getSomethingFromApi”函数是“expensiveCalculation”的依赖项。当我们的父组件重新呈现时，所发生的是函数“getSomethingFromApi”被重新初始化。这意味着我们的“expensiveCalculation”的依赖性将会改变，这意味着每次重新呈现父对象时，将会重新触发昂贵的计算。**这样对性能不好！**

现在让我们看看如何使用 useCallback 钩子来获得一个' **Memoized** '回调，并防止代价高昂的计算重新触发。

在我们的代码中没有太多变化，在第 6 行，我们已经将函数包装在一个 useCallback 钩子中。就是这样。

我们的函数现在被记忆化了，这意味着在重新呈现 ParentComponent 时它不会被重新初始化。这也意味着引用不会在 ChildComponent 中改变，并且 expensiveCalculation 不会被重新执行！太神奇了！如果子组件被渲染很多次，你的小添加将会产生巨大的效果。这显示了 useCallback 钩子的威力。

在不同的情况下，您可能会发现使用 useCallback 挂钩很有趣。在依赖关系比较的上下文中，正如在这个例子中看到的，它当然有助于实现我们编写高性能应用程序的目标。

在本文中，您了解了 useCallback 钩子，以及它如何帮助您提高应用程序的性能。请注意，这种解决方案并不适合所有的用例，有时记忆计算或回调的成本更高，然后使用像 useMemo 或 useCallback 这样的钩子可能是有害的。小心，继续测试，祝你好运！

这个月，我将介绍一些鲜为人知的 React 钩子以及它们的具体用途。我的上一篇文章介绍了“useReducer”挂钩，如果您有兴趣阅读，可以在这里找到它:

[](https://diederik-mathijs.medium.com/create-a-comment-system-using-1-react-hook-4169ba8f4d6a) [## 构建一个只有 1 个 React 钩子的评论系统。

### 最近，我发现了 React 中各种钩子的惊人的可能性。这就是为什么每周…

diederik-mathijs.medium.com](https://diederik-mathijs.medium.com/create-a-comment-system-using-1-react-hook-4169ba8f4d6a) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)