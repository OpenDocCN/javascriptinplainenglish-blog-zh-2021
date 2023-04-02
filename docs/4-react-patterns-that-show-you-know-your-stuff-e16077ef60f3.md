# 4 种反应模式，表明你了解自己的东西

> 原文：<https://javascript.plainenglish.io/4-react-patterns-that-show-you-know-your-stuff-e16077ef60f3?source=collection_archive---------3----------------------->

![](img/de43ecf01a474a0163763ea6e52fcfd3.png)

## 1.带挂钩的功能部件

现代的 React 代码允许将组件定义为由它们的`props`参数化的函数，如下所示。这比将组件定义为类更简洁、可维护和可读。

每个状态变量从`useState()`获得自己的设置器，而不是`setState()`。而且，我们现在可以触发像 API 调用这样的副作用，这依赖于`props`和`useEffect()`的第二个参数的某种组合。这比记忆不同组件生命周期挂钩的行为要简单得多。

```
import React, { useState, useEffect } from 'react';function myComponent(props) {
  const [count, setCount] = useState(0);
  useEffect(
    () => console.log(props.a),
    [props.a]
  );
  return (
    <div>
      <p>You clicked {count} times</p>
      <button 
       onClick={
        () => setCount(count + 1)
       }
      >
       Click me
      </button>
    </div>
  );
}
```

## **2。用于状态管理的 react-redux**

React-redux 是一个用于管理复杂应用程序状态的优秀库。Redux 充当应用程序状态的集中式内存存储。不同的组件可以使用 Redux 的`dispatch()`方法将状态变化发送到中央存储，Redux 将这些变化广播给与`connect()`和`mapStateToProps()`相关的组件。

如果您的应用程序进行多余的 API 调用，Redux 非常适合缓存这些结果。对于频繁安装和卸载的组件，这对于节省额外的状态计算也很有用。

## **3。将样式委托给组件库**

有时，CSS 对于实现应用程序的正确外观是必要的。然而大多数时候，情况并非如此。现代组件库有可预测的 API，这些 API 在内部以一致的方式处理复杂的样式。

以下是一些具有强大样式功能的组件库的优秀选择:

*   [物料界面](https://material-ui.com/)
*   [蚂蚁设计](https://ant.design/)
*   [语义 UI 反应](http://Semantic UI React)

## 4.**尽可能从组件中移除逻辑**

组件内部复杂的逻辑会使其难以阅读，甚至更难维护。更糟糕的是，在团队工作中，通过多次编写相同的功能来重复工作是很常见的。通过将依赖关系很少的长函数放在一个单独的文件中，可以更容易地避免这种情况。链式 API 调用就是一个很好的例子。

这是基于“不要重复自己”(干)的批判性软件工程教条。

React 是一个用于开发应用程序接口的现代、快速发展的库。希望本文能够帮助您了解开发应用程序的一些最佳实践。作为一名软件工程师，要学的东西太多了，这可能会令人望而生畏，但这也是它的乐趣所在。

现在，去做一些酷的东西吧！

如果你喜欢这篇文章，并想阅读更多，请考虑通过下面我的委托推荐链接注册一个付费媒体会员。这不增加你的额外费用，也是支持我写作的最好方式。谢谢！

[https://mildtechnologist.medium.com/membership](https://mildtechnologist.medium.com/membership)

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)