# 如何知道何时使用 Redux

> 原文：<https://javascript.plainenglish.io/how-to-know-when-to-use-redux-ab5a8b9bd657?source=collection_archive---------11----------------------->

![](img/7fff67b08e6d3bb433b855fc7aa73abd.png)

Image credits to [Startup Stock Photos](https://www.pexels.com/photo/man-wearing-black-and-white-stripe-shirt-looking-at-white-printer-papers-on-the-wall-212286/)

有很多博客都在谈论*如何*使用 Redux，但是很少有关于*何时*使用 Redux 的。辨别这一点很困难，也很棘手，这也是我一直在纠结的事情。

## Redux 是什么？为什么被创造出来？

Redux 是由 Dan Abramov 和 Andrew Clark 创建的用于状态管理的第三方库。

首先，状态管理在前端开发中是一个复杂的挑战。 [JavaScript 是异步的](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing)，这意味着可以有很多函数在后台运行等待完成，我们不知道它们什么时候完成并返回。

当引入 React 时，它通过使用类组件来提供内置的状态对象。随着时间的推移，Redux 被引入来处理状态管理。更具体地说，它旨在使状态更可预测。

![](img/baf68da9e3c05b87972f2fde0b4d4323.png)

Image credits to Redux.JS

## (简要)Redux 是如何工作的？

Redux 需要安装到您的项目中。根据您的需要，可以在[这里](https://redux.js.org/introduction/getting-started/)找到文档。

状态包含在一个`**store**`对象中，这就是它的独特之处。您可能还记得我之前提到过 Redux 使状态更容易预测。事实上，它是通过将状态对象设置为只读来实现的:也就是说，我们可以读取和显示它的值，但不能更改或改变状态本身。这必须通过行动来实现。Actions 告诉我们的代码我们希望它采取什么类型的(因为没有更好的词)动作。Reducers 是接受参数的函数，其中一个参数是动作，它将返回更新后的状态。

此外，还有`**mapStateToProps**`和`**mapDispatchToProps**`，这两个函数允许我们访问和读取状态(前者)和改变状态(后者)。声明:突变状态是不可取的，所以我们用`**mapDispatch**`实际做的是复制状态，对复制的版本进行突变，返回新突变的版本。

## 使用 Redux 有哪些弊端？

如果你对我简单描述的感到困惑，你并不孤单。Redux 旨在使管理和维护状态变得更容易，但是正如您所看到的，有相当多的东西需要用 Redux 构建到您的代码中。

然而，更重要的是，你可能不需要它。丹·阿布拉莫夫(Dan Abramov)自己也写到了这一点，他说“地方政府很好”。如果你正在启动一个应用程序并考虑可扩展性，很容易认为 Redux 是必要的。

## 那我怎么知道呢？

不幸的是，我不会为你提供一个清单来确定你是否需要 Redux。

首先确保您理解 React 的状态管理和数据流。局部状态和全局状态有什么区别？这个组件*需要*访问状态吗？如果有的话，什么数据需要传递给这个组件？

接下来，理解 Redux 是为了解决什么问题而构建的，以及它是如何做到的。

然后，评估问题或情况。在我看来，Redux 不应该是您的第一种方法，尤其是因为有 React 挂钩，但也不应该避免。一旦你理解了它，它就是一个强大而有用的库。Redux 为这种方法提供了什么，而 useState 和/或 useContext 没有或不能提供什么？

如果您认为局部和全局状态还不够，那么 Redux 可能是一个不错的选择。

Redux 是前端开发中最受欢迎的技能之一。虽然理解它很重要，但并不是每个应用程序都需要它。我希望这能对管理状态的其他方法有所启发。我发现下面的资源对我写这篇文章很有帮助，我想你也一样。

## 资源

[](https://en.wikipedia.org/wiki/Redux_%28JavaScript_library%29) [## Redux (JavaScript 库)-维基百科

### Redux 是一个用于管理应用程序状态的开源 JavaScript 库。它最常用于库，如…

en.wikipedia.org](https://en.wikipedia.org/wiki/Redux_%28JavaScript_library%29)  [## 你可能不需要 Redux

### 人们往往在需要之前就选择 Redux。“如果没有它，我们的应用无法扩展怎么办？”后来，开发商皱眉…

medium.com](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367) [](https://medium.com/rexlabs/redux-is-dead-long-live-redux-745d0cb26423) [## 雷杜死了，雷杜万岁

### 快速回顾一下为什么 Redux 没有死，为什么你不应该总是听别人的

medium.com](https://medium.com/rexlabs/redux-is-dead-long-live-redux-745d0cb26423) [](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing) [## 介绍异步 JavaScript -学习 web 开发| MDN

### 在这篇文章中，我们简要回顾了与同步 JavaScript 相关的问题，并先看一看一些…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing) [](https://redux.js.org/introduction/getting-started/) [## Redux | Redux 入门

### Redux 是 JavaScript 应用程序的可预测状态容器。它帮助您编写行为一致的应用程序…

redux.js.org](https://redux.js.org/introduction/getting-started/) 

*更多内容尽在*[plain English . io](http://plainenglish.io/)