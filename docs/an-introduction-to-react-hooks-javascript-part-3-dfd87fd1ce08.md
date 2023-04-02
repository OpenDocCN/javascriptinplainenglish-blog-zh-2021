# React 挂钩简介(JavaScript)

> 原文：<https://javascript.plainenglish.io/an-introduction-to-react-hooks-javascript-part-3-dfd87fd1ce08?source=collection_archive---------22----------------------->

## React 挂钩简介—第 3 部分

![](img/310ec4b5d33a45e4b3d335380bd1d86c.png)

本文是上一篇[*React Hooks(Javascript)介绍的续篇——第二部分*](https://kkapoor15904.medium.com/an-introduction-to-react-hooks-javascript-part-2-144dadac44fa) 。如果你还没看过，请一定要看:)。在本文中，我将介绍:

1.  `useContext`
2.  您的定制挂钩

# 反应上下文

React 上下文是跨 React 组件传递信息的一种方式，无需执行**道具演练**。道具钻取是指将道具向下传递给组件及其子组件，就像这样:

注意`prop`是如何被*钻入*子组件的。如果你厌倦了这样做，React context 可以帮助你避免这种情况。

## 使用

要使用 React 上下文，有三个步骤:

1.  定义您的上下文(如果需要，使用初始值)
2.  定义一个组件容器元素，它将**提供**上下文数据
3.  包装提供者中的任何组件以使用上下文数据

就这么简单。

这看起来是这样的:

# 创建您的自定义挂钩

最后，本系列的最后一部分(可能是),也是设计 React 应用程序时非常方便的东西——定制钩子。第一条规则是你的钩子应该总是从**开始使用**。

比如，你用什么钩子来获得一些`localStorage`值。这里有一个来自 useHooks.com 的极好的例子:

现在，在整个应用程序中重复使用这个钩子，而不必一次又一次地编写相同的逻辑！就像这样，您可以创建许多不同的挂钩来帮助您实现不同的功能。想了解更多定制挂钩的想法，我强烈推荐你去 useHooks.com 参观。另外，为了进一步调试，`useDebugValue` React 钩子可以帮助你调试你的定制钩子！阅读[文档](https://reactjs.org/docs/hooks-reference.html#usedebugvalue)了解更多信息。

**就这样结束了！感谢阅读！**

*更多内容请看*[***plain English . io***](http://plainenglish.io/)