# Epic React — React 基础知识

> 原文：<https://javascript.plainenglish.io/epic-react-react-fundamentals-cf76b6cedaf1?source=collection_archive---------3----------------------->

这是你的老朋友肯特·c·多兹的课程——史诗般的反应。展示本课程第一部分的阅读材料——学习反应基础知识。

![](img/127b4e3d948a2334441a37db67e602be.png)

Captivating isn’t it?

在做好自由职业、开源和一些实习工作后，我的冒名顶替综合症让我称自己为 React 开发者。尽管如此，还是有一句台词我很喜欢。这一缺失的线索引导我去寻找——史诗般的反应。你想知道为什么。你疯了吗？

钩子，类，CSS-In-JS，JSX，Redux，Context 等等。这些对于 React 的旅程非常重要。但是当涉及到更大的项目时，这些恶魔就出现了——性能、测试、可重用性、灵活性、反应悬念、优化等等。我们中的大多数人很可能会在失败时举手投降。承认吧(我承认)。

> React 的灵活性是一把双刃剑。—肯特·c·多兹

作为开发人员，我们需要构建可扩展的、经过良好测试的、架构良好的应用程序，*肯特说——不，*每个人都这样说。是的，这是我选择“史诗反应”的唯一原因。你可能也需要。看一看课程设置，我相信你不会被*抛弃*。

[](https://epicreact.dev/) [## 变得非常擅长反应

### 我正准备开始准备我们正在开发的应用程序的全面发布，这包括解决许多…

epicreact.dev](https://epicreact.dev/) 

我听起来像一个教程地狱计划，不是吗？嗯，这一切都取决于你和你如何对待学习。我最喜欢的一个人，Josh Comeau，对此有一句美丽的话

[](https://www.joshwcomeau.com/blog/how-to-learn-stuff-quickly/) [## 如何快速学习

### 人们常说，互联网已经使教育民主化:人类知识的总和只需要在谷歌上搜索一下…

www.joshwcomeau.com](https://www.joshwcomeau.com/blog/how-to-learn-stuff-quickly/) 

希望你觉得这是有关联的。

回到主要文章，这是一个基于课程部分的系列。今天的主题是“反应基本原理”。我写这篇文章是为了概括作者涵盖的要点。

登机，

1.  **设置**

这是作者把我带到的地方。从字面上看，这不是其他的课程设置，而是你自己的训练营。是的，如果遇到困难，可以参加一个带视频的代码互动研讨会。Epic React 团队在这方面做得非常好。在您的机器上安装该设置并不困难。只要阅读适当的文档，你就可以开始了。这是一个戏弄你的玩笑—

![](img/0830248cc966b0c38f24287165d83dfa.png)

This is the Workshop. This is it, Epic React.

如果你倾向于视频观看，那么只需通过研讨会的网站。阅读说明。解决习题。解决额外的学分练习。用作者为你写的测试反复检查你的解决方案。答对了。

2.**你没学会反应**

说真的，这是作者一开始就要告诉你的。他的意思是，你会知道幕后的事情，而不是直接做出反应。作者讲述了 DOM 及其必要性。

关键点-

*   DOM —与文档对象模型的交互
*   节点—使用 JavaScript 创建节点/元素

3.**生**

不是研究和分析部门，而是 React 的原始 API。在这里，您将使用这些 API 编写代码来打印您的“Hello World”。

关键点-

*   React 框架——负责创建 React 元素。类似于你在普通 JavaScript 中做的事情。
*   ReactDOM 呈现器——负责将这些 React 元素呈现给 DOM。有点像`rootElement.append()`。
*   嵌套问题—使用 React RAW APIs 创建嵌套元素时出现的问题，例如 React.createElement()。这导致了—

4. **JSX**

一个类似 HTML 的语法糖构建在 React RAW APIs 之上，以便于理解代码。JSX 不是 HTML，而是 javaScript 的语法扩展。这就是 JSX 对浏览器陌生的原因。

关键点-

*   JSX——用类似 HTML 的方式制作这些`React.createElement()`。
*   Babel —代码编译器，用于编译 JSX，以便浏览器能够理解
*   spread——JavaScript 中的一个运算符。当对象或数组中的所有元素都需要包含在某种列表中时使用。必须学。

5.**定制组件&造型**

您将看到自己从如何将重复代码转换成可在应用程序环境中的任何地方使用的定制组件。

关键点-

*   功能—功能是为了避免重复。那是你开始的地方。创建一个返回类似`div`的元素的自定义函数。但不是我们想要的组件。
*   React createElement —了解这些原始 API 的参数，它们接受函数并返回可呈现的内容。仍然不是组件。
*   JSX——在这里。就像对常规的`div`使用 JSX 比使用原始的`React.createElement` API 更好一样，对定制组件使用 JSX 也更好(摘自 Epic React，XD 的文档)。你将会见证巴别塔是如何用 JSX 诠释以各种形式书写的构件的。
*   PropTypes —更像是您希望您的数据成为的类型。假设，我送你一朵花，我希望你收到一朵花，而不是水果。这就是两个组件的作用。父组件希望其子组件拥有唯一特定类型的数据。作者解释了进行类型检查的优点和缺点。在额外学分练习中，你可以尝试同样的 [npm 包](https://www.npmjs.com/package/prop-types)。
*   造型——当然，你已经看到一些经验丰富的专家创造了那些恶心的动画和用户界面。作者欢迎您使用 React 中的样式，让您创建一个简单的样式对象&然后为其创建一个自定义组件。在结尾封装样式的道具。
*   反应片段—必要而非强制。将多个组件一起返回是 React 模式。

最后但同样重要的是，

6.**表单&按键**

在本次研讨会中，您将了解如何在 react 中处理表单提交、目标 dom 元素和一些验证。不要忘了，钥匙——啊，如果避免认为它很低调，那会让你头疼。

*   事件和引用—访问 dom 元素的方法。ref 是一个设置为 React 元素的对象，React 元素反过来设置对实际呈现的 DOM 节点的引用。
*   控制—让 React 控制表单中的输入值。带`onChange`手柄的`value`支架。
*   按键——如果你做了一些反应，那么你可能会在你的浏览器中看到按键警告。当您试图呈现 React 元素的数组时，会发生这种情况。Warning 试图告诉你，每个元素都应该有一些独特的属性，这样 React 就可以区分它们。你可以阅读为什么键是 React 的本质

[](https://epicreact.dev/why-react-needs-a-key-prop/) [## 为什么 React 需要一个关键道具

### 如果您使用 React 有一段时间了，您可能以前遇到过这种情况:index.js:1 警告:列表中的每个子元素都应该…

epicreact.dev](https://epicreact.dev/why-react-needs-a-key-prop/) 

唷，多么美好的学习啊(至少对我来说是这样，你自己做了之后也可能会这样)。你可以购买课程，或者反过来(你知道我的意思，对吧？).但是，有一件免费的事情是肯定的，那就是这个代码交互式研讨会。获取存储库并开始学习。

[](https://github.com/kentcdodds/react-fundamentals) [## GitHub-kentcdodds/react-Fundamentals:我的 React 基础研讨会的材料

### 了解构建 React 应用程序和库所必需的基本概念，了解您需要成为的一切…

github.com](https://github.com/kentcdodds/react-fundamentals) 

克隆。安装并开始学习̶R̶e̶a̶c̶t̶，不， **Epic React** 。

你可以在我的 ZTM 反应库找到我是如何完成第一部分的—

[](https://github.com/TidbitsJS) [## TidbitsJS -概述

### 很高兴见到你，我是 Sujata Gunale 又名 TidbitsJS🤓自学开发者👩‍💻从事 Web 开发📝写作…

github.com](https://github.com/TidbitsJS) 

至此，进入下一篇文章的下一部分。在那之前，

i̇yi·冈勒👋

*更多内容请看*[*plain English . io*](http://plainenglish.io/)