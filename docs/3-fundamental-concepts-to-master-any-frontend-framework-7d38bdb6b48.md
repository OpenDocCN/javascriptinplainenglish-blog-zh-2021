# 掌握任何前端框架的 3 个基本概念

> 原文：<https://javascript.plainenglish.io/3-fundamental-concepts-to-master-any-frontend-framework-7d38bdb6b48?source=collection_archive---------4----------------------->

## Angular，React，Vue，Svelte，以及未来的许多框架。

![](img/1855cd64d5fe53743331385402d43e53.png)

Photo by [HalGatewood.com](https://unsplash.com/@halacious?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

目前有许多前端框架的选择，并且这个列表将会随着时间的推移不断扩展和发展。关于哪个框架是最好的，几乎有全面的在线争论，每一个都有自己的利弊，整个互联网上都是详细介绍它们的文章。

> 在选择前端框架时，我可以向你保证一件事——这并不重要。

历史已经证明，web 开发是一个指数级发展的领域，很简单，如果你没有准备好从一个框架跳到下一个框架，你要么沉沦，要么游泳。

只要掌握了这几个关键概念，无论哪种框架出现在你面前，你都将成为一名有竞争力的前端开发人员。

# 1.成分

![](img/8d58416cf6d6c71503d4db651897065c.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

组件是前端开发的构建块，也是驱动所有现代前端框架的最重要的概念。

组件是两件事:

1.  **可重复使用**
2.  **自成一体**

在前端框架中，组件应该被视为面向对象编程中的对象，就像 Java 中的类一样。

由于 JavaScipt 的灵活性，很容易抛弃面向对象的原则，而喜欢拼凑一些代码，直到 UI 看起来不错。同样，JavaScript 非常灵活。这有其优点和缺点，可能只适合整篇文章，但是最终，为了产生可读的前端代码，组件需要在概念上类似于对象。

> 任何傻瓜都能写出计算机能理解的代码。优秀的程序员编写人类能够理解的代码。
> 
> —马丁·福勒，2008 年。

这就是前端框架如此强大的原因。它们允许将浏览器语言的惊人结果与经典计算机科学语言的结构合理的模式结合起来。

## 组件由什么组成？

这些组成了所有的组件，但是对于这个例子，让我们考虑一个待办事项列表。对于组件，考虑列表中的单个项目。

**模板**

模板是组成组件的子组件的层次结构。对于待办事项列表组件，这将是待办事项组件的列表。对于待办事项组件，这可能是一个复选框、项目名称以及用于删除和编辑的操作按钮。

**脚本**

该脚本定义了组件的功能。每个动作按钮都需要一个相应的函数来向父组件发出一个事件，即待办事项组件中的待办事项列表。

该脚本还将定义生命周期事件，例如创建或销毁组件时发生的操作。

最后，该脚本为任何动态内容定义了输入属性。这通常与模板直接相关。对于待办事项，我们需要复选框布尔值和名称字符串的输入属性。

**造型**

样式是组件的最后一步。

样式库比前端框架多得多，所以还是选一个吧。没关系。对于初学者来说，[自举](https://getbootstrap.com/)是一个可靠的选择，使造型简单。

我也强烈推荐学习 [SASS](https://sass-lang.com/) 为 CSS 带来现代功能。

# 2.按指定路线发送

![](img/29d14350524e2b94283f9aec631abc95.png)

Photo by [Jamie Templeton](https://unsplash.com/@jamietempleton?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

客户端路由是我们今天看到的单页面应用程序框架的关键。这些通常都有很好的文档记录并且易于实现，但是理解路由层次结构仍然很重要。

首先，了解动态路由。回到我们的 to-do 列表示例，让我们将 todo-list 组件放在 route 中，`/todos`。当用户点击一个待办事项时，他们应该被带到一个专门为该待办事项准备的页面。这将通过路由`/todos/:id`来完成。

在加载这个路由时，应用程序需要接受动态 ID 并找到具有相应 ID 的待办事项，并正确处理使用 404 组件找不到待办事项的情况。

最后，对于路由，您应该理解延迟加载。这是让你的框架的模块捆绑器，比如 Webpack，分割你的代码来减少加载时间的概念。这对于独立的页面来说通常是有效的，比如登录页面和主页。当用户在登录页面时，不需要加载主页。

# 3.状态管理

![](img/38c5c5df9e9a99e6fd2e35df601f53dc.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

正如我前面解释的，组件在理想情况下是自包含的。处理大量数据的大型应用程序的问题是，它们需要正确地管理数据。

如果没有状态管理，大型组件层次结构中的子组件将需要沿着一条长线向下传递属性才能到达它。这是完全没有效率的。

每个框架都有自己的状态管理风格，但基本概念是拥有一个非 UI 组件来保存应用程序范围内的数据状态。

我相信前端开发比框架更深入，掌握这些基本概念将允许你掌握任何前端框架。

感谢您的阅读！