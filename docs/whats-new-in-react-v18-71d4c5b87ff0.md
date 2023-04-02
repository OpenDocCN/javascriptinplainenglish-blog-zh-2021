# React v18 有什么新功能？

> 原文：<https://javascript.plainenglish.io/whats-new-in-react-v18-71d4c5b87ff0?source=collection_archive---------7----------------------->

## 让我们了解 React 18 的最新功能。

![](img/67b8f62a9cd8af572e05269a19263045.png)

[Image source](https://reactjs.org/)

**React 18** 推出新的测试版，很快就会推出。这一次，React 18 将带有最新的功能，不同于 v17 的更新。尽管 React 是一个受欢迎的 JavaScript 库，但是开发者社区对这个库有更多的期望。

在这篇博客中，让我们通过更详细的描述来深入了解 React 18 的主要功能。

# 1.开始过渡以进行并发渲染

在与用户界面(UI)进行交互时，如在输入框中键入内容或单击按钮，在大屏幕更新中可能会出现页面冻结，从而中断工作流程。

React 18 引入了一个名为`**startTransition**`的新 API，即使在大屏幕更新期间，也有助于保持应用程序的响应。这个 API 通过将特定的动作标记为**转换**，从而告知 React 哪些更新重要，哪些不重要，从而极大地改善了用户交互。

`startTransition`将更新移至后台，包括复杂的处理或因网络连接而导致的缓慢数据提取。这里的转换会被紧急更新中断，先前不相关的转换会被忽略，从而使 UI 能够忽略本质上可能较慢的二次更新。

一个真实的例子可以在这个链接[这里](https://github.com/reactwg/react-18/discussions/65)看到。

# 2.自动配料

自动批处理意味着在一次渲染中反应多个状态更新以增强性能的组称为批处理。

它还会阻止组件呈现*半成品*状态，同时更新单个状态变量，导致应用程序中的某些错误。超时、承诺甚至本机事件处理程序中的更新将按照与 React 事件中的更新相同的方式进行批处理。这将增加现成的渲染时间，甚至更好的性能。React 18 使批处理过程更加高效和一致。

点击[此处](https://codesandbox.io/s/morning-sun-lgz88?file=/src/index.js)查看新配料技术如何工作的演示。

Source — React’s Github

# 3.支持悬念:SSR

对于那些不知道 SSR 的人，这里有一个简单的解释:**服务器端渲染(SSR)** ，是一个让你直接在服务器上从 React 组件生成 HTML 的过程，生成的 HTML 可以显示给用户。甚至在 javascript 包加载和运行之前，用户就可以看到服务器提供的内容。因此，给用户提供了更快和更好的感觉。

但有时，后端的 javascript 需要很长时间来处理，这段时间被称为*补水时间*。React 18 更新将允许**直接在服务器上流式传输 HTML** ，从而提高性能，即服务器在使用另一个名为`**Suspense**`的组件渲染组件时发送组件，该组件决定应用程序的哪些部分可能需要更长时间加载，哪些部分应该直接渲染。被悬念包裹的成分不会再阻碍水合作用。这被称为选择性水合方法。一旦浏览器获得其内容和 javascript 代码，每个就绪的组件都将开始水合。

点击[此处](https://codesandbox.io/s/festive-star-9hfqt?file=/src/App.js)观看实时演示。

# 4.根 API 改进

React 中的根 API 是 React 用来跟踪渲染树的应用程序顶层数据结构的指针。在 React 18 中，将有两种不同的根 API——传统的根 API 和 ReactDOM.createRoot。新的根 API，称为`ReactDOM.createRoot`，将通过允许并发模式功能，为应用程序添加所有改进。

*旧根 API :*

```
import ReactDOM from 'react-dom';
import App from 'App';
const container = document.getElementById('root');
ReactDOM.render(<App />, container);
```

此根 API 在运行更新时存在一些问题。我们需要继续将`container`传递到渲染中，即使它从未改变。

*新的根 API :*

```
import ReactDOM from 'react-dom';
import App from 'App';
const container = document.getElementById('root');
const root = ReactDOM.createRoot(container);
root.render(<App />);
```

新的根 API 修复了这个问题，因为我们不再需要将`container`传递到渲染中。

# 结论

新的 React 18 更新看起来很有影响力，尽管还有许多小的更新尚未公布。许多功能可以帮助开发人员简化工作，提高应用程序的速度和效率。让我们继续关注发布日期。要了解更多关于如何安装 React 18 测试版的信息，请点击链接[此处](https://github.com/reactwg/react-18/discussions/9)。

感谢阅读！

# 参考

[](https://reactjs.org/blog/2021/06/08/the-plan-for-react-18.html) [## React 18 - React 博客的计划

### React 团队很高兴分享一些更新:我们已经开始了 React 18 版本的工作，这将是我们的下一个…

reactjs.org](https://reactjs.org/blog/2021/06/08/the-plan-for-react-18.html) [](https://github.com/reactwg/react-18) [## GitHub-React WG/React-18:React 18 发布工作组。

### 这是 React 18 发布的工作组。它的成立是为了通过发布……

github.com](https://github.com/reactwg/react-18) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)