# React Native 中的 JSX 入门指南

> 原文：<https://javascript.plainenglish.io/a-beginners-guide-to-jsx-in-react-native-c50b4037440b?source=collection_archive---------13----------------------->

## 学习 React Native 的基础知识

![](img/278857f5164e84950d879aa0e1891718.png)

Photo by [Dmitry Ratushny](https://unsplash.com/@ratushny?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好，在这里，我将涵盖您开始使用 React Native 所需的所有基础知识。

我将把它分成多个部分。第一部分将解释 JSX。

另一个将解释剩下的概念。敬请关注。

如果你是 React 原生应用开发的新手，你可以阅读初学者指南。使用 Hello world 应用程序设置 React 本地环境。

[](https://medium.com/javascript-in-plain-english/getting-started-with-react-native-for-beginners-958d39fee16a) [## 面向初学者的 React Native 入门

### 学习所有你想知道的关于 React Native 的知识。

medium.com](https://medium.com/javascript-in-plain-english/getting-started-with-react-native-for-beginners-958d39fee16a) 

现在，我们将学习 React Native 所需的基础知识。

所以开始吧。

React Native 主要使用 React.js 库。React.js 是一个有时被称为框架的库，主要用于前端 Web 开发。

有 [80+免费资源](https://medium.com/javascript-in-plain-english/80-free-resources-for-web-designers-and-web-developers-in-2021-f400be2875ea)供网页设计师和网页开发者学习网页开发，还有[网页开发者入门指南](https://medium.com/code-blog/getting-started-and-earning-105-813-yr-as-a-web-developer-for-beginners-19b2cd26fcc2)。

所以你要学习 React.js 才能成为 React Native 的专家。

**react . js 里面有什么？**

JSX、组件、道具、状态、生命周期和事件。

如果你不熟悉他们，不要紧张。我会在这里解释一切。

# 从 JSX 开始

首先，我们将在 React 中编写 Hello World 程序。

这就是了，

```
import React from 'react'; 
import ReactDOM from 'react-dom'; const hello = <h1>Hello World!</h1>; 
ReactDOM.render(hello, document.getElementById('root'));
```

这是什么？我们来详细解释一下。

我们引进了 React 和 ReactDOM。

**什么是 ReactDOM？** ReactDOM 提供了 render()、createPortal()等 DOM 特定方法。

在那之后，

```
const hello = <h1>Hello World</h1>; 
```

这是 JSX。

JSX 允许我们一起编写 JavaScript 和 HTML。根据 w3schools 的说法，JSX 代表 JavaScript XML。

我再举一个例子解释一下。

```
import React from 'react'; 
import ReactDOM from 'react-dom';const place = 'Mumbai';
const feature = <h1>Hello, {place}.</h1>;

ReactDOM.render( feature, document.getElementById('root') );//Output: Hello, Mumbai.
```

这里我们把孟买这样的地方定义为常数。

然后我们称之为 JSX 内部。然后我们使用 ReactDOM 渲染它。使用 JSX，我们可以访问变量，使用花括号的表达式。

**嘿 Nitin，document.getElementById('root ')怎么样。**你还没解释清楚。

是的，我的朋友。在这里，我们通过 Id 访问元素，称为 root。

如果你设置了 React.js 环境，那么转到公共文件夹= > index.html

在那里面，你可以看到

```
<div id="root"></div>
```

因此，无论您在 React 应用程序中编写什么，都将呈现在一个具有 id 根的 div 中。

就是这样。

觉得这篇文章有用？在 Medium 上关注我( [Nitin Sharma](https://nitinfab.medium.com/) )，看看我下面最受欢迎的文章！请👏这篇文章分享一下！

***如果你喜欢我的工作，想要支持，可以*** [***请我喝杯咖啡！***](https://www.buymeacoffee.com/nitinfab)

这是第二部分。

[](https://medium.com/code-blog/learn-react-components-for-your-next-react-or-react-native-project-bcf69cd81752) [## 为您的下一个 React 或 React Native 项目学习 React 组件。

### 学习 React 和 React Native 的基础知识

medium.com](https://medium.com/code-blog/learn-react-components-for-your-next-react-or-react-native-project-bcf69cd81752) 

第三部分。

[](/state-management-using-react-hooks-in-react-native-5f12895d29a8) [## 在 React Native 中使用 React 挂钩进行状态管理

### 有了 React 钩子，我们可以使用 state、componentDidMount、componentDidUpdate 和其他 React 特性，而不需要使用 Class…

javascript.plainenglish.io](/state-management-using-react-hooks-in-react-native-5f12895d29a8) 

这是第四部分。

[](/a-beginners-guide-to-react-router-34b4e86fded3) [## React 路由器初学者指南

### 使用 react-router-dom 轻松导航到不同的屏幕。

javascript.plainenglish.io](/a-beginners-guide-to-react-router-34b4e86fded3) 

谢谢:)