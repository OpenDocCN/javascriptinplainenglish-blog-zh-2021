# 如何在 React 中实现内存化以提高性能

> 原文：<https://javascript.plainenglish.io/react-performance-optimization-ft-memoization-61b765c4c619?source=collection_archive---------9----------------------->

## 用 useMemo 和 useCallback 反应性能优化

![](img/ccbccbf2773f86118590f81c9e55f594.png)

Optimize your react app with ease

React 优化可能是一件棘手的事情。React 本身进行了内部优化，以提高性能。当我们从可读性、维护友好性和可伸缩性的角度考虑组件的复杂性时，添加的优化技术会使前面提到的代码方面发生倒退。在最坏的情况下，旨在优化性能的技术会进一步降低性能。因此，简而言之，所有的优化技术都有成本，应该事先认真考虑。

但在某些情况下，React app 可能会使用大量数据或昂贵的数据计算，优化可能会成为需求之一。

所以，让我们开始吧。

React app 的性能可以通过减少不必要的 API 调用来优化，这要简单得多，值得推荐，也可以通过使用 memoization 来优化。

在本文中，我们将重点讨论 React 中的记忆技术。

记忆化是代码的时间复杂度和空间复杂度之间的权衡。通过记忆化，React 存储对象、回调函数或 props 的先前版本，并将它们与下一个即将到来的记忆化对象、回调函数或 props 的版本进行比较，以确定任何更改。只有在发生变化时，组件才会重新呈现，从而提高应用程序的性能。这里，浏览器内存用于提高性能。

**在应用 React 函数内存化技术之前，要知道您的代码应该可以在没有这些技术的情况下工作，因为 React 可能会在内部跳过这些技术来释放浏览器中的内存。**

记忆可应用于:

1.成分

2.目标

3.回调函数

React 为我们提供了 *React.memo* 和两个钩子: *useMemo()* 和 *useCallback()* 来应用记忆化技术。

让我们看看现在的行动。

Simple Memoized Component Demo

# **1。应用于组件的记忆化**

如果您的组件使用相同的属性呈现相同的结果，您可以将它包装在对`React.memo`的调用中，在某些情况下通过记忆结果来提高性能。这意味着 React 将跳过组件的渲染，并重用最后一次渲染的结果。

例如，当重新呈现父组件时，即使子组件不接受来自父组件的任何道具，它的子组件也会被重新呈现。在这种情况下，为了避免子组件不必要的重新呈现，可以使用`React.memo`。

`*React.memo*`浅浅地比喻道具中的物件。为了定制比较器，可以添加一个可选的定制比较器回调函数作为第二个参数。

这可以被想象成 React 类组件中的 *shouldComponentUpdate()* 生命周期方法的等价物。

> 你可能会尝试使用 *React。Memo* with comparator 作为解决方案的一部分来停止子组件的重新渲染，但是 [React 文档](https://reactjs.org/docs/react-api.html#reactmemo)警告不应该这样做，因为 React 可能会跳过内存化来为其他一些组件释放空间。

# **2。应用于对象的记忆化**

*useMemo()* hook 接受一个要记忆的函数和一个依赖数组。 *useMemo* 仅当其中一个依赖关系发生变化时，才会重新计算记忆值。这种优化有助于避免每次渲染时进行昂贵的计算。

**如果没有提供数组，将在每次渲染时计算新值。**

# **3。应用于 props** 中回调函数的记忆化

由于`React.memo`对道具做了浅显的比较，道具中的回调函数即使不做任何改动，仍然可能触发重新渲染。为了防止这种不必要的渲染`useCallback()`是有用的。

***如果我们在使用*** `***React.memo***` ***，为什么我们还要*** `***useCallback()***` ***？***

**答**:在每次组件渲染时，React 都会创建新的函数副本。新的副本将有新的引用。浅层比较使用引用相等来确定对象中的变化(在 JavaScript 中函数也是对象)。因此，这些会触发 props 中带有回调的子组件进行重新渲染。

*useCallback()* 如果所提供的依赖关系没有变化，则简单地跳过每个渲染函数的重新创建。这满足了引用相等性，防止了由于 props 中的回调函数而导致的重新呈现。

*useCallback()* 接受一个要记忆的回调和一个可选的依赖数组作为参数。

**如果没有提供数组，将在每次渲染时计算新值。**

> *`useCallback(fn，dependencies)`* 等价于` *useMemo(() = > fn，dependencies)* `。

[ [此处提供代码…](https://codesandbox.io/s/react-memoization-igth1?file=/src/components/ParentComp.tsx) ]

感谢阅读！

*更多内容看*[***plain English . io***](http://plainenglish.io/)