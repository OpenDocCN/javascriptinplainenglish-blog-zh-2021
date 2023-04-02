# 针对初级反应型开发人员的 10 个面试问题

> 原文：<https://javascript.plainenglish.io/10-interview-questions-for-junior-react-developers-79600f7c7645?source=collection_archive---------6----------------------->

## 以下是我在面试初级反应职位时得到的另外 10 个问题和答案。享受吧！

![](img/bbe2262dbf1aac6622015e8b97cea3ef.png)

Photo by [ThisisEngineering RAEng](https://unsplash.com/@thisisengineering?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/coding?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 1.你能告诉我什么是 DOM 吗？如果你知道，DOM 和虚拟 DOM 之间的区别是什么？

## 数字正射影像图

DOM 代表*文档对象模型*，是结构化文本的抽象。文本是一个 HTML 代码，DOM 被简单地称为 **HTML DOM** 。HTML 的元素成为 DOM 中的*节点*。虽然 HTML 是文本，但是 DOM 是该文本的内存表示。HTML DOM 提供了一个接口(API)来遍历和修改节点。有像`removeChild`、`getElementById`这样的方法可以动态改变网页的内容。HTML DOM 的问题在于它总是树结构的。这通常没问题，因为我们可以很容易地遍历树，但速度并不快。而且，如今 DOM 树非常庞大，因为我们正在推动 SPAs ( *单页应用程序*)，随之而来的是不断修改 DOM 树的需求，这是一个真正的性能和开发难题。

正如我们所说的，一个现代的网站是由成千上万个 div 组成的，有很多处理点击、输入和提交等事件的方法。典型的 jQuery 事件处理程序应该找到每个对事件感兴趣的节点，并在必要时进行更新。这就带来了低效和管理等问题。这就是“反应”寻求帮助的地方。我们只需声明一个组件应该是什么样子，而不是像手动遍历 DOM 树这样的低级技术。React 为我们做底层工作——调用 HTML DOM API 调用，而不是我们手动进行。但是这并没有解决性能问题——虚拟 DOM 解决了。

## 虚拟 DOM

虚拟 DOM 是 HTML DOM 的抽象——一个轻量级的副本。它独立于浏览器特定的实现细节。正如我们所说的——DOM 是一个抽象，所以虚拟 DOM 实际上是一个抽象的抽象。它允许 React 在这个抽象的世界中完成它的工作，并跳过 DOM 操作，这些操作通常是特定于浏览器的并且很慢。想象一下，操纵虚拟 DOM 就像编辑一个蓝图，而不是在实际的房子里移动房间。

# 2.ShadowDOM 和 VirtualDOM 之间的区别是什么？

## 虚拟 DOM

虚拟 DOM 是为了避免对 DOM 进行不必要的更改，这在性能上是昂贵的，因为对 DOM 的更改通常会导致页面的重新呈现。虚拟 DOM 还允许同时收集多个要应用的更改，所以不是每个更改都会导致重新呈现，而是在一组更改应用到 DOM 后，重新呈现只发生一次。

## 阴影 DOM

影子 DOM 主要是关于实现的封装。单个定制元素可以实现或多或少复杂的逻辑和或多或少复杂的 DOM。任意复杂的整个 web 应用程序都可以通过导入和`<body><my-app></my-app>`添加到页面中，但更简单的可重用和可组合组件也可以实现为自定义元素，其中内部表示隐藏在影子 DOM 中，如`<date-picker></date-picker>`。

# 3.什么是 diffing 算法？

React 需要使用算法来找出如何有效地更新 UI 以匹配最近的树。差分算法是生成最少数量的操作来将一棵树变换成另一棵树。

# 4.给我们解释一下什么是 JSX，为什么浏览器不能读取它？

JSX 是 JavaScript XML 的简称。这是 React 使用的一种文件类型，它利用了 JavaScript 的表达能力以及类似 HTML 的模板语法。它使得 HTML 文件非常容易理解，应用程序也非常健壮。浏览器只能读取 JavaScript 对象，但 JSX 不是一个普通的 JavaScript 对象。因此，要使浏览器能够读取 JSX，首先，我们需要使用像 Babel 这样的 JSX 转换器将 JSX 文件转换成 JavaScript 对象，然后将它传递给浏览器。

# 5.React 中 render()的用途是什么？

每个 React 组件必须强制拥有一个 **render()** 。它返回一个 React 元素，这个元素是原生 DOM 组件的表示。如果需要呈现多个 HTML 元素，那么必须将它们组合在一个封闭标签中，例如 **< form >、< group >、< div >** 等。这个函数必须保持纯净，也就是说，它必须在每次被调用时返回相同的结果。

# 6.你知道什么是代码分裂和反应懒惰功能吗？

代码分割是 Webpack 和 Browserify 等捆绑包支持的一个特性，它们可以创建多个可以在运行时动态加载的捆绑包。react 项目通过动态导入()特性支持代码分割。`React.lazy`函数让您将动态导入渲染为常规组件。当组件被渲染时，它会自动加载包含其他组件的包。这必须返回一个承诺，该承诺解析为一个包含 React 组件的默认导出的模块。

# 7.React 的类生命周期方法有哪些？

1.  getDerivedStateFromProps
2.  组件安装
3.  shouldComponentUpdate
4.  getSnapshotBeforeUpdate
5.  componentDidUpdate
6.  组件将卸载

# 8.React 中的道具演练是什么？

有时候，在开发 React 应用程序时，需要将数据从层次结构中较高的组件传递到嵌套较深的组件。为了在这样的组件之间传递数据，我们从一个源组件传递属性，并继续将属性传递给层次结构中的下一个组件，直到到达深度嵌套的组件。

使用 prop drilling 的缺点是，本来不知道数据的组件可以访问数据。

# 9.什么是无状态组件？

无状态组件只不过是纯粹的函数，只根据提供给它们的属性来呈现 DOM。该组件不需要任何内部状态，更不用说构造函数或生命周期处理程序了。组件的输出纯粹是提供给它的属性的函数。

# 10.React 中的`StrictMode`是什么？

React 的`StrictMode`是一种帮助组件，可以帮助你编写更好的 react 组件，你可以用`<StrictMode />`包装一组组件，它基本上会:

*   验证内部的组件是否遵循了一些推荐的做法，如果不在控制台中，将向您发出警告。
*   验证不推荐使用的方法没有被使用，如果它们被使用，严格模式将在控制台中警告您。
*   通过识别潜在风险来帮助您预防一些副作用。

如果你想看更多我在面试时得到的问题，点击[这里](/10-junior-frontend-developer-technical-interview-questions-4342da7c7fd0)。

*在* [***获取更多内容***](https://plainenglish.io/)