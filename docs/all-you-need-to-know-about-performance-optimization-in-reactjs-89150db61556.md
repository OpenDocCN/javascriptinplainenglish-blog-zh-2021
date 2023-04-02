# React 中的性能优化

> 原文：<https://javascript.plainenglish.io/all-you-need-to-know-about-performance-optimization-in-reactjs-89150db61556?source=collection_archive---------14----------------------->

![](img/54fcae7506d1250e0077752e440228d1.png)

Picture: [Railsware](https://railsware.com/blog/why-use-react/)

性能优化是一个流程，它使您的服务器尽可能高效，以便更快地提供 web 内容。

总的来说，React 以其令人难以置信的速度而闻名，性能是它的一大优势。React 用于此目的的特性有虚拟 DOM、服务器端呈现、捆绑支持和树抖动。因此，我们将看看如何使您的 React 应用程序高效的几种方法。

## [优化技术:](https://reactjs.org/docs/optimizing-performance.html)

**1。使用生产版本**

如果有任何性能问题，您应该使用缩小的产品版本。虽然，React 默认给出了在开发中有用的警告，但是为了确保构建过程使用 [React 开发工具](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)。

**2。用于分析组件的 DevTools profilier】**

`react-dom` 16.5+和`react-native` 0.57+通过 React DevTools Profiler 在开发模式下提供了增强的分析功能。

**3。长长的虚拟化列表**

如果您的应用程序呈现很长的数据列表(数百或数千行)，一种称为“窗口”的技术在任何给定时间只呈现一小部分行。它可以极大地减少重新渲染组件以及创建 DOM 节点的时间。 [react-window](https://react-window.now.sh/) 和 [react-virtualized](https://bvaughn.github.io/react-virtualized/) 是著名的窗口库。

**4。避免对帐**

调和是在 react 中更新 DOM 的过程。React 构建并维护呈现的 UI 的内部表示。它包括从组件返回的 React 元素。这种表示让 React 避免创建 DOM 节点和访问不必要的现有节点，因为这可能比 JavaScript 对象上的操作要慢。

**5。使用 shouldComponentUpdate**

即使 React 只更新更改的 DOM 节点，重新渲染仍然需要一些时间。在许多情况下，这不是问题，但如果速度明显下降，您可以通过覆盖生命周期函数`shouldComponentUpdate`来加快速度，这是在重新渲染过程开始之前触发的。这个函数的默认实现返回`true`，让 React 执行更新。如果你知道在某些情况下你的组件不需要更新，你可以从`shouldComponentUpdate`返回`false`，跳过整个渲染过程，包括调用这个组件上的`render()`和下面的。

**6。无数据突变**

避免这个问题的最简单的方法是避免改变您用作道具或状态的值。ES6 支持数组的[扩展语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)，这可以使这变得更容易。

当您处理深度嵌套的对象时，以一种不可变的方式更新它们会让人感觉很复杂。如果你遇到这个问题，请查看 [Immer](https://github.com/mweststrate/immer) 或[immutanbility-helper](https://github.com/kolodny/immutability-helper)。这些库让您可以编写可读性很高的代码，而不会失去不变性的好处。

在思考优化的同时，下一个问题浮现在脑海里，**我们应该什么时候进行优化？**所以，项目一开始就不用担心。因为如果你担心太多，你会浪费时间和资源，因为事情可能会变得复杂。当您注意到系统性能滞后时，您可以这样做。

**“我们应该忘记小的效率，比如说 97%的时候:过早的优化是万恶之源”**

- *唐纳德·克努特*

优化不应该与编码最佳实践相混淆。始终建议遵循编码约定，这有助于更好地执行 react 应用程序。以下是其中的一些:

> 在高阶函数上使用钩子。
> 
> 析构属性并定义它们的类型(如果尚未定义)。
> 
> 使用无状态函数来避免重新渲染。
> 
> 有条件地呈现。
> 
> 使用 [ESLint](https://eslint.org/) (对于 javascript)或 [TSLint](https://www.npmjs.com/package/tslint) (对于类型脚本)
> 
> React 开发者工具( [chrome 扩展](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en))用于调试。

在下一集，你可以了解更多关于过早优化的知识。

[](https://saba-saif.medium.com/examples-of-premature-optimization-ecff9eac67b7) [## 过早优化的例子

### 在上一集，我们已经了解了如何、何时以及为什么进行优化。在这篇文章中，你将…

saba-saif.medium.com](https://saba-saif.medium.com/examples-of-premature-optimization-ecff9eac67b7) 

## 进一步阅读

[](/5-tools-practices-to-help-you-develop-faster-in-react-b884c1b20fc2) [## 帮助您在 React 中更快开发的 5 种工具和实践

### React 工具、技巧和最佳实践将帮助您更快地构建应用

javascript.plainenglish.io](/5-tools-practices-to-help-you-develop-faster-in-react-b884c1b20fc2) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。*****