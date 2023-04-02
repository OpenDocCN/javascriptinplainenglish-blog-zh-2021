# React Hooks:终极指南

> 原文：<https://javascript.plainenglish.io/react-hooks-the-ultimate-guide-usecallback-usememo-d68516b0767c?source=collection_archive---------4----------------------->

## 反应钩的最终指南。

![](img/ca594765c6375bde3e6cc2591d404121.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大多数人在使用 React.js 时都担心性能问题。React 是惊人的，如果使用得当，当状态改变时，你应该不会有重新渲染的问题。但是正如我们在本系列的第一部分开始所说的，我们不仅需要使用`useState`和`useEffect`来管理状态，还需要使用我们将在这里看到的其他钩子。

首先，让我们了解记忆化的概念以及我们为什么需要记忆化。

## 记忆化

> 在计算中，记忆化是一种优化技术，主要用于通过存储昂贵的函数调用的结果并在相同的输入再次出现时返回缓存的结果来加速计算机程序。

记忆化的思想是保存函数的返回值或函数本身，如果发送给它的值没有改变，就不要重新运行它。

## 了解 JavaScript 相等检查

JavaScript 中的函数是一等公民，这意味着函数是常规对象。函数对象可以像对象一样被其他函数返回，进行比较等。

但是如果我们有一个函数，运行它两次，设置它为两个不同的变量并比较它(如下)，这将返回`false`，我们将相同的逻辑应用于对象

## 使用回调

所以`useCallback`的目标是避免不必要的重新渲染，它接收两个值:一个将被记忆的函数和一个每次任何值改变时都将更新该函数的依赖数组。因此，要解决上一篇文章中的小问题，我们可以这样做:

## **使用备忘录**

钩子`useMemo`接收两个参数:一个计算并返回一个值的函数和一个依赖数组(比如`useCallback`)。当我们有一些基于道具的计算时(比如下面的例子)，或者当我们想用发送的道具记忆一个组件时，通常使用这个钩子。

很简单，对吧？

## useMemo vs useCallback

这两个钩子在 react 组件中有相同的目标，那就是记忆值，最大的区别是要记忆的值的类型。`useCallback`返回一个内存化的回调，`useMemo`返回一个内存化的值，但是这是什么意思呢？

在`useMemo`中，将运行函数(第一个参数), React 将记忆从该函数返回的值(每次依赖关系数组改变时),在`useCallback`中，每次依赖关系数组改变时返回其函数 uncalled，因此您可以稍后调用它(或不调用)。

如果你有一些大的计算或者一些需要花费一些时间在函数中计算的东西，你应该使用`useMemo`,这样这个计算只有在依赖关系改变的时候才会发生。

**将道具向下传递到子组件**

`useCallback`和`useMemo`真正有用的一点是在传递值给子组件的时候。假设你想传递一个函数和一个值给你的子组件，你想避免不必要的重新渲染。如果您传递函数和值本身，而没有将它包装在一个`useCallback`和`useMemo`中，它将重新呈现，即使函数本身没有改变(还记得 JavaScript 等式检查吗？).

## **什么时候不用它**

在现实生活中，没有什么是防弹的，所以即使是那些在某些情况下提高性能的挂钩也会降低你的应用程序的速度。

> 性能优化不是免费的。它们总是伴随着成本，但并不总是伴随着抵消成本的收益。

要使内存化工作，需要处理这些数据，计算并保存它们(处理垃圾收集器等)。我的观点是，只有在以下情况下才应该使用这些挂钩:

*   你有一些计算将是计算昂贵的
*   当你需要比较它的时候(比如把一个函数传递给一个子组件)

## **结论**

当谈到 React 应用程序时，性能非常重要，当处理复杂情况或计算或真正的大数据时，这些钩子将会给你很大帮助。

希望有帮助。如果我遗漏了什么或者有什么要补充的，请留下评论，我会编辑帖子！

干杯！

[](https://en.wikipedia.org/wiki/Memoization) [## 记忆化-维基百科

### 在计算中，优化或记忆是一种优化技术，主要用于通过…

en.wikipedia.org](https://en.wikipedia.org/wiki/Memoization) 

[https://reactjs.org/docs/hooks-faq.html](https://reactjs.org/docs/hooks-faq.html)

[https://kentcdodds.com/blog/usememo-and-usecallback](https://kentcdodds.com/blog/usememo-and-usecallback)

[https://reactjs.org/docs/hooks-reference.html#usecallback](https://pt-br.reactjs.org/docs/hooks-reference.html#usecallback)

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*