# 10 个你可能在工作面试中遇到的面试问题

> 原文：<https://javascript.plainenglish.io/10-react-interview-questions-youll-probably-encounter-in-job-interviews-1e55f445eb4b?source=collection_archive---------1----------------------->

## 用这些最受欢迎的人力资源问题为你的面试做准备。

![](img/e0e2951d5fea68e63bd55fb304cdf0b8.png)

Photo by [Sebastian Herrmann](https://unsplash.com/@officestock?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React.js 是一个非常流行的 JavaScript 库，由脸书的一位程序员创建，并作为一个开源项目得到了进一步的发展，其中开发该项目的主要人员是脸书的程序员。

在这篇文章中，我将提出一些我认为在前端开发人员面试中会被问到的常见问题，这次是用 React.js。

如果我必须招聘，我可能会问这些问题中的任何一个或全部。一定要在面试前阅读。

# 1.你怎么解释`setState`？

这个方法用于改变一个组件的内部状态，简单地将它分配到一个`this.state`新状态或者改变它的一个属性值不会导致组件重新呈现。当我们不需要将组件状态发布到组件之外时，通常会用到组件状态。否则，您将不得不使用 Redux 或上下文 API。

# 2.组件和元素的区别是什么

组件是从`React.Component`继承一些逻辑和/或包含其他组件和元素的函数或类。另一方面，元素是在 DOM 中有对应对象的对象，例如 div、span 或 input。

然而，这是一种心理上的简化，因为 react 本身不使用 DOM，只有额外的 ReactDOM 库增加了这种可能性(如果您对 React 中某个元素的确切含义感兴趣，您必须参考 React 源代码，但在我看来，该元素作为 DOM 中的一个元素是正确的解释，尽管不精确)，但毫无疑问，该元素也将是一个 Web 组件，因为它在 DOM 中也有其对等物。

元素只出现在 JSX 中，在生成的 JavaScript 中，它们被一个函数调用`React.createElement`所取代，其中第一个参数是标记的名称。

# 3.React 中事件处理的工作方式

React 中的事件行为类似于原生 DOM 中的事件，但有一些不同:

*   事件的名称用骆驼字体书写，
*   函数传递给事件的属性，而不是字符串，
*   事件处理程序的参数获取一个类为`SyntheticEvent`的对象，该对象引用字段`nativeEvent`中的原始事件，而`target`指向触发该事件的对象。

重要的是，React 中的事件不是唯一的，它们以不同的值被重用。这个属性叫做事件池，也就是说你不能在一个异步函数中使用事件，例如`fetch,`，因为当一个异步动作被触发时，事件对象可能会改变。这种机制用于优化的原因。不过这个机制可以通过调用`event.persist()`来关闭。

# 4.虚拟 DOM 如何工作

虚拟 DOM 是真实 DOM 树的内存表示。操作是在虚拟 DOM 上执行的，当发生变化时，会执行 diffs，然后执行使两棵树相同所需的最少数量的操作。使用 React 更新原生 DOM 的算法称为调和，翻译过来就是调和。

# 5.什么是受控组件

这些是组件，例如输入、选择或文本区域表单的元素，其值(value 属性)来自 React，因此，当它们的状态改变时，它们将使用新的状态再次呈现(当然，由于虚拟 DOM，不会创建新元素，但会改变其 value 属性)。这是以这样的方式完成的，即 undervalue 有例如来自状态和事件的值，例如 onChange 或 onKeyUp 改变该状态。

# 6.上下文 API 如何工作

当需要跨多个组件维护应用程序中的状态时，可以使用上下文 API 和 Redux(在版本中使用上下文 API)来最小化多属性继承(名为属性钻取或线程)。

Context API 允许您创建一个本地状态，该状态将被树中的其他组件继承，绕过不需要它的组件。这就是为什么在 Redux 库中使用 z 的原因。它就像一个功能`scope`一样工作，里面的所有功能都可以访问上面的所有作用域。

上下文 API 提供了一个函数`React.createContext`，它创建了一个包含两个组件的对象:`obiekt.Provider`和`obiekt.Consumer.`一个例子是，当我们需要为应用程序添加国际化时，所有的按钮都必须有翻译的文本。我们的按钮在 DOM 树中处于不同的层次。假设我们没有使用 Redux，如果没有上下文 API，我们将不得不向每个按钮的每个组件传递语言属性来获取它。

# 7.Redux 如何工作

这个库由 Store、Reducer 和 Actions 等元素组成。

*   缩减器是一个基于旧状态返回新状态的函数。接受两个参数，前一个状态和操作，
*   动作是被转移到缩减器的对象，基于它们的类型，应该返回应用程序的不同的新状态，
*   商店是属于我的财产。这样的函数:
    — `getState`，—返回当前状态，
    — `subscribe`，—用于添加一个新的函数，当状态发生变化时会调用这个函数，
    — `dispatch`，—我们把动作传递给这个函数，状态就会发生变化。

该库独立于任何框架工作。例如，您可以将它与 Angular 一起使用。要在 React 中使用这个库，您必须另外使用 ReactRedux 库并使用它的两个函数，`connect`和`Provider`。

`Provider`它是一个组件，具有一个名为`store`的属性，使应用程序状态对组件可用，其行为类似于一个 ErrorBoundary(即`Provider`一个包装其他组件的组件)，并使用 React 的上下文 API。另一方面，函数`connect`充当组件包装器。分配给它两个功能:

*   mapStateToProps —这是一个将应用程序状态作为参数的函数，
*   mapDispatchToProps —这是一个函数，它将`dispatch` Redux 作为一个参数，并返回一个带有函数的对象，这些函数通过适当的动作调用`dispatch`，即它们添加函数来改变应用程序的状态。

connect 函数是一个更高级别的组件，即它是一个采用普通组件并通过两个函数`mapStateToProps`和`mapDispatchToProps.`从 Redux 返回可以访问状态的新组件的函数

# 8.什么是高阶元件

原理类似于高阶函数。这种类型的组件是将组件作为参数并返回新参数的函数。Redux 库中的 connect 函数就是一个例子。

# 9.你能给我解释一下什么是反应纤维吗？

React Fiber 是 React 16 中的一个改进引擎，它提高了动画、手势和布局的性能，其主要功能是所谓的增量渲染，允许您将渲染分成几帧，这是通过可以暂停和恢复渲染来实现的。这使得更快地将更改发送到屏幕上成为可能。

# 10.什么是 Flux，Flux 和 Redux 有什么区别

Flux 是 React.js 框架的创始人脸书提出的应用架构。Flux 不是一个特定的库，而是一个架构，其主要元素是 Dispatcher 函数，整个事情使用类似于 Publish/Subscribe 或 EventEmitter 的架构。

Flux 使用单向数据流来维护应用程序状态。虽然 Flux 是架构的名字，但 Redux 已经是实现它的库了。

你不需要在工作面试中死记硬背你的答案。你需要用心学习 React 或者你正在使用的任何编程语言。这不是一个小抄，只是一个简单的工作面试问题的场景。祝你好运！