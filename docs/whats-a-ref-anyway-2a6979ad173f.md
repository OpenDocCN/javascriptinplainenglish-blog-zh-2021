# 裁判到底是什么？

> 原文：<https://javascript.plainenglish.io/whats-a-ref-anyway-2a6979ad173f?source=collection_archive---------11----------------------->

## 学习反应 JS

## 反应引用-强制修改子节点

![](img/2bf23771dad5ea51edc173e48da06f66.png)

Photo by [Ryunosuke Kikuno](https://unsplash.com/@ryunosuke_kikuno?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/library?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在普通 JavaScript 中，`DOM`的强制性修改相对简单。您通过`document.querySelector()`或`document.getElementById()`获取一个`DOM`节点，要么立即修改它，要么将它存储在一个变量中以备后用。然而，React 排除了这些方法，因为它使用了一个[虚拟 DOM](https://reactjs.org/docs/faq-internals.html) 。但是有一些用例需要直接访问一个节点，而不是通过状态和/或属性来控制它。

# 输入反应参考

> " Refs 提供了一种访问 DOM 节点或 React 元素的方法，这些元素是在 render 方法中创建的."—参考文献和 DOM

一个`ref`是一个普通的老式 JavaScript 对象，只有一个属性`current`。

好极了。那么一个`ref`是用来做什么的呢？从 React 文档中:

> 有几个很好的参考用例:
> 
> -管理焦点、文本选择或媒体播放。
> 
> -触发命令式动画。
> 
> -与第三方 DOM 库集成。

# 一个例子:管理焦点

上面的例子存储了一个对 input 元素的引用，作为对`this.inputRef.current`的值，允许对节点进行强制性修改。

# createRef vs useRef

那么 createRef 和 useRef 有什么区别呢？这两个功能的正确用例是什么？答案在于`useRef`是 React 的[钩子 API](https://reactjs.org/docs/hooks-reference.html) 的一部分。

所有前面的例子都利用了类组件，将`ref`存储为类的属性。功能组件缺少属性，因此策略不起作用。`useRef`记忆`ref`允许它在渲染之间持续。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)