# 了解回调引用

> 原文：<https://javascript.plainenglish.io/understanding-callback-refs-107a21d831d7?source=collection_archive---------5----------------------->

## 学习反应 JS

## React refs 的另一种实现

![](img/835c0ccb86703a90d782420719512c2c.png)

Photo by [Rajan Shrestha](https://unsplash.com/@razaanstha?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@razaanstha?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

React 利用一个虚拟的`DOM`来防止使用`querySelectorAll()`或`getElementById()`方法来强制修改特定的节点。相反，您的站点通过在`state`中存储属性并根据需要重新呈现元素来动态响应输入。此外，对于一些需要强制修改节点的用例，引用是现成的。

在我之前的博客文章中，我介绍了 React 中 refs 的两个主要实现。对于类组件，ref 存储为在构造函数中使用`React.createRef()`实例化的属性。缺少自身属性的功能组件利用`useRef()`钩子将 ref 存储在一个变量中。第三种也是不太常见的策略是**回调 Ref** 。这有点奇怪，但是通过研究它们，我对 React 的内部工作方式有了更多的了解。

# 传入回调函数

那么回调 ref 是如何工作的呢？**不是传递一个由** `**React.createRef()**` **或** `**useRef()**` **创建的** `**ref**` **，而是传递一个回调函数。这个回调函数然后接收相应的元素/节点作为参数，然后可以根据需要存储、操作或使用它。**

A React class component utilizing a callback ref.

如上所示，我们没有在构造函数中使用`React.createRef()`，而是设置了一个名为`inputRef`的属性，该属性最初被设置为`null`。当组件挂载时，回调 ref 被执行，将所需的`DOM`元素存储为`this.inputRef`属性的值。

**注意要点:**

*   传递给`ref`属性的回调函数在组件挂载时立即执行。
*   存储的元素是可以通过`this.inputRef`***直接访问**(而不是存储为* `*React.createRef()*` *或*`*useRef()*`*创建的对象的 `*.current*` *属性)。**

# *安装和卸载*

*如前所述，**当组件挂载**时，任何作为 ref 传递的回调函数都会被执行(例如在 `componentDidMount`触发之前 ***)。在执行`componentDidUpdate`之前，引用的元素也保证是最新的。卸载时，再次执行回调函数，这次使用`null`而不是`DOM`节点作为参数。****

# *用例*

*首先，我认为学习回调引用让我对 React 如何实现引用有了更好的理解。在使用`createRef()`或`useRef()`API 时，React 的解释器没有魔力。React 只是利用一个回调函数将节点存储为引用对象的值`.current`。*

*就我个人而言，我只在我的一个项目中 [**实现无限滚动行为**](https://garrett-bodley.medium.com/implementing-infinite-scroll-behavior-2dabff25901f) 时使用过回调引用(这启发了我更深入地研究文档并撰写本文)。你在你的项目中使用过回调引用吗？欢迎在下面的评论中分享自己的经验！*

**更多内容请看*[*plain English . io*](http://plainenglish.io/)*