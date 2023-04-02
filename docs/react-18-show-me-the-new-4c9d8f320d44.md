# React 18 中的所有新功能

> 原文：<https://javascript.plainenglish.io/react-18-show-me-the-new-4c9d8f320d44?source=collection_archive---------2----------------------->

![](img/4546e968e875dce4fcbee3a235409d48.png)

React 团队透露了 React 18 即将推出的新功能，在这篇博客中，我们将探讨这些功能以及它们如何在不久的将来为您提供帮助！

## 严格模式🧑🏽‍🏫

[严格模式](https://reactjs.org/docs/strict-mode.html)增加了一些东西，比如一个叫做*“严格效果”*的新行为。这允许我们双重调用像`mount`和`unmount`这样的效果。它创建了一个在开发期间通过快速刷新来纠正行为的环境，而不仅仅是寻找更有弹性的组件。还有一个“屏幕外 API”目前正在构建中。

通过隐藏组件而不是卸载它们，保持状态，并仍然调用`mount` / `unmount`效果，屏幕外 API 将实现更好的性能。

## 自动配料⚙️

现在自动配料有了重大改进。我们首先来看看性能。

反应已经分批，换句话说，分组，多个状态更新到一个，以尽量减少不必要的重新渲染。然而，像承诺、超时或其他处理程序这样的元素没有利用它，因为它只限于 DOM 事件处理程序。

React 18 改变了这一切，它将无限制地批量更新状态，只要这样做是安全的。结果，你问？…这将在没有任何额外参与的情况下创造更好的性能。

## 并行渲染🔁

并发渲染肯定是值得期待的，因为它是 React 18 迄今为止最大的更新。

在此名称之前，它被称为“并发模式”。名称的改变意味着并行特性的逐渐采用。这允许我们在不重写代码的情况下采用并发特性，并且按照您自己的步调来做。

## 新 API🆕

在 React 18 中，我们获得了几种新的 API，它们有多种形式。

`startTransition` —它的目的是在**转换**时发现状态更新，使处理它们变得不紧急。

`useDeferredValue` —这个钩子将为您提供一个传递值的延迟元素，它将跟随原始元素，直到提供超时。

`SuspenseList` —该组件旨在处理各种情况，例如，提取的数据可能以不可预测的顺序到达。多亏了`<SuspenseList>`，一个组件可以被编排，它将检查 UI。

## 根 API🎴

`createRoot`将取代`render`功能。新的 API 是访问 React 18 新特性的门户。这意味着鼓励逐步采用并减少潜在的性能比较。

这里是即将到来的 React 18 的一些新更新，我希望你对它们以及它们能给 React 开发者带来的好处和效率感到兴奋！

*更多内容看*[***plain English . io***](http://plainenglish.io)