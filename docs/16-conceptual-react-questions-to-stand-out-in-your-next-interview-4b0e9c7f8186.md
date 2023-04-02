# 16 个概念性反应问题，让你在下次面试中脱颖而出

> 原文：<https://javascript.plainenglish.io/16-conceptual-react-questions-to-stand-out-in-your-next-interview-4b0e9c7f8186?source=collection_archive---------4----------------------->

## 你能处理这些反应问题吗？让我们来了解一下！

![](img/6c1c4b4be3014a90c97ad70576d75d65.png)

Photo by [Ryan Stone](https://unsplash.com/@rstone_design?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/weird?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在面试中回答一个概念性的问题并不意味着你会比工作中的其他人更好，但它肯定意味着你有时间和兴趣去理解一个框架中的深层概念。

> 一个人对文档的理解将一个好的开发人员与一个伟大的开发人员区分开来。

嗯，今天，我们将探讨一些作为 React 开发人员可能想知道的概念性问题。如果您正在寻找简单的语法相关问题，那么这篇文章不适合您！

我们开始吧！

# 1.React 中渲染劫持是什么？

[正如谷歌先生所说](https://stackoverflow.com/questions/48144659/what-is-render-hijacking-in-react)，渲染劫持是

> “渲染劫持的概念是控制一个组件从另一个组件输出什么的能力”。

实际上，您用另一个高阶组件(HOC)包装您的组件。然后，根据需要注入道具，这会导致渲染逻辑发生变化。

基本上，你所做的就是让组件有不同的行为。

# 2.如果在构造函数中使用 setState()会怎么样？

当你使用`setState()` React 再次渲染整个组件。因此，如果在构造函数内部调用`setState()`，React 会尝试重新呈现不存在的组件，从而产生一个递归问题。

您会得到类似这样的错误:

```
Can only update a mounted or mounting component.
```

所以我们需要使用`this.state`来初始化构造函数内部的变量。像下面这样

```
constructor(props) {
    this.state = {
        // anything that you want inside state
    }
}
```

# 3.React 中的合成事件是什么？

事件是任何浏览器必不可少的部分。像`onclick`、`onscroll`等。但是由于 React 使用虚拟 dom，我们需要一个在不同浏览器上一致工作的包装器。

> React 将事件规范化，使它们在不同的浏览器中具有一致的属性。— [React 文档](https://reactjs.org/docs/events.html)

因此，总而言之，合成事件是不同事件的跨浏览器包装器。重要的是要注意:它们与浏览器的本地事件不是一一对应的。

# 4.React 中的门户是什么？

如果您想将一些子组件呈现到组件树层次结构之外的 DOM 节点中，那么 [React Portal](https://reactjs.org/docs/portals.html) 是一个不错的选择。

其语法是

```
ReactDOM.createPortal(child, container)
```

第一个参数是任何可呈现的 React 子元素，如元素、字符串或片段。第二个参数是 DOM 元素。

# 5.什么是和解？

当一个组件的道具或状态改变时，我们需要重新渲染这个组件。实际的 DOM 是否会被更新取决于这两个节点(以前的和当前的)之间的差异。

但是为了比较两个节点，我们需要一个 O(n)的复杂度，这在现实生活中是不实际的。这就是 React 团队决定使用启发式方法的原因。

这个过程的名字叫做和解。如果您有兴趣，请参考[文档](https://reactjs.org/docs/portals.html)。

# 6.为什么 React 使用 className 而不是 class？

`class`是 JavaScript 中的关键字，JSX 是 JavaScript 的扩展。这就是 React 使用 className 而不是 class 的主要原因。

ClassName.jsx

传递一个字符串作为类名属性。

# 7.什么是反应纤维？

纤程是 React v16 中核心算法的新的重新实现。我们已经讨论过协调，新的实现称为 React Fiber。

如果您有兴趣理解核心概念，这里的是很好的文档。

# 8.React Fiber 的目标是什么？

React Fiber 的目标是增加其在动画、布局和手势等领域的适用性。它的主要特点是增量渲染:能够将渲染工作分割成块，并分散到多个帧上。

# 9.什么是不受控制的组件？

在 react 组件中存储状态的通常方式是`useState`或`this.state`。但有一个问题是，它们与渲染过程紧密相关。因此，在某些情况下，你会面临一些困难。

如果你使用`ref`存储一个组件的状态，那么这个组件被称为非受控组件。它更像传统的 HTML

在下面的`UserProfile`组件中，使用 ref 来访问名称输入。

# 10.为什么片段比容器 div 好？

以下是原因列表，

1.通过不创建额外的 DOM 节点，片段速度更快，使用的内存更少。这只对又大又深的树有真正的好处。

2.一些 CSS 机制像 Flexbox 和 CSS Grid 有特殊的父子关系，在中间添加 div 很难保持想要的布局。

3.DOM 检查器不那么杂乱。

# 11.React 的局限性是什么？

除了这些优点之外，React 也有一些限制，

1.  React 只是一个视图库，不是一个完整的框架。
2.  对于刚接触 web 开发的初学者来说，有一个学习曲线。
3.  将 React 集成到传统的 MVC 框架中需要一些额外的配置。
4.  代码复杂性随着内联模板和 JSX 而增加。
5.  过多的小部件导致过度设计或锅炉板。

# 12.如何为 HOC 组件创建 props 代理？

您可以使用 props 代理模式添加/编辑传递给组件的 props，如下所示:

ProxyProps.jsx

# 13.如果在初始状态下使用道具会怎么样？

`constructor`函数从不更新组件的当前状态。它只在组件安装前被调用一次。

因此，假设我们正在使用 props 来初始化组件的状态。

```
function SomeComponent(props){ const [count , setCount]= useState(props.count);
}
```

现在，如果`props.count`从父节点改变，那么子节点将永远不会被更新，因为`useState`只被调用过一次。所以通过道具来初始化状态并不是一个好主意。

# 14.钩子会取代渲染道具和高阶组件吗？

渲染道具和高阶组件都只渲染一个子对象，但在大多数情况下，挂钩是一种更简单的方法，可以减少树中的嵌套。

# 15.可以不调用 setState 强制组件重新渲染吗？

每当你的组件的状态或道具改变，组件将重新渲染。但是如果因为某种原因，我们不得不强制一个组件重新渲染，那么我们可以称之为`foreUpdate()`函数。

```
component.forceUpdate(callback)
```

# 16.为什么不能在 React 里更新道具？

React 哲学认为道具应该是不可变的，自顶向下的。这意味着父母可以发送任何属性值给孩子，但不能修改收到的属性。

就是这样。也许你认识他们中的一些人，也许你不认识。我想(也希望)你已经从这篇文章中学到了一些东西。

祝您愉快！

**通过**[**LinkedIn**](https://www.linkedin.com/in/56faisal/)**或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**

## 资源:

**合成事件:**[https://reactjs.org/docs/events.html](https://reactjs.org/docs/events.html)
**反应入口:**[https://reactjs.org/docs/portals.html](https://reactjs.org/docs/portals.html)
**反应纤维:**[https://github.com/acdlite/react-fiber-architecture](https://github.com/acdlite/react-fiber-architecture)

**StackOverflow 论坛:**[https://stack overflow . com/questions/48144659/what-is-render-jacking-in-react](https://stackoverflow.com/questions/48144659/what-is-render-hijacking-in-react)

*更多内容看*[***plain English . io***](http://plainenglish.io/)