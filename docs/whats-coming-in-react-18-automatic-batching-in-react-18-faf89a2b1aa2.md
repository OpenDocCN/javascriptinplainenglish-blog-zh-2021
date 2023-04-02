# React 18 自动配料功能

> 原文：<https://javascript.plainenglish.io/whats-coming-in-react-18-automatic-batching-in-react-18-faf89a2b1aa2?source=collection_archive---------11----------------------->

## 不要错过 React 18 提供的自动配料功能

**React 18 出了**！它带来了一些新的功能来应对。

在本文中，我们将讨论 React 18 带来的**自动批处理功能**。欢迎来到 [Technofunnel](https://medium.com/technofunnel) ，让我们深入了解自动配料和相关概念的细节。此次更新为 React 带来了大量**性能提升。**

![](img/f9b7b36e9a7a755bdd4d41db3717cf8b.png)

React 18 is out. Try new features of React 18

## 理解批处理的概念

**批处理是将多个状态更新合并到一个渲染中的概念**。如果可以将多个状态更新批处理到单个更新中，并且重新渲染一次，将会提高 React 的性能。让我们寻找下面的代码来理解这个概念。

在上面的代码中，有一个按钮点击事件被触发。在点击按钮内部，我们更新了两次状态。我们在两个独立的“setState”函数中更新“userName”和“userAge”的值。以便提高应用程序的性能。React 17 提供了批处理特性，因此来自“setState”的更改可以合并在一起，并且组件将只呈现一次，并将同时对“userName”和“userAge”进行更改。

## **自动配料在反应中的优势**

在 React 中使用批处理的优点是:

*   通过避免不必要的重新渲染来提高性能
*   状态变化被合并成一个，并呈现有效的差异。
*   当只有几个变量被更新并且几个变量保持不变直到下一个渲染周期时，可以避免不一致的状态，这可能导致错误。

在上面的场景中，如果没有批处理，可能会出现这样的场景:在初始呈现期间，名称被更新，然后组件将重新呈现以显示更新的年龄。

# React 18 的更新

批处理有多种好处。在 React 17 之前，批处理只在浏览器事件中可用，如“点击”、“鼠标悬停”、“onchange”等。它在其他事件中不可用，如“Axios 订阅”、“获取”、“设置超时”、“设置间隔”、“用户定义的事件”。

**现在在 React 18 中，**所有更新的内容都将被自动批量处理，不管这些事件来自哪里。这意味着在承诺、超时、间隔、自定义事件中完成的更新也将被批处理。这将进一步提高性能。

为了达到同样的效果，我们需要使用“ **ReactDOM.createRoot** ”而不是“ReactDOM.render”。下面是一个相同的例子。

[https://gist.github.com/Mayankgupta688/4755d495b6753cb2cc38c507f471853b](https://gist.github.com/Mayankgupta688/4755d495b6753cb2cc38c507f471853b)

**所以继续前进，开始使用 React 18 吧！**

*多内容于* [***浅显易懂***](http://plainenglish.io/)