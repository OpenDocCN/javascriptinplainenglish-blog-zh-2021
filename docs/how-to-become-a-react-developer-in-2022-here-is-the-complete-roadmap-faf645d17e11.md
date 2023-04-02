# 2023 年如何成为 React 开发者？这是完整的路线图。

> 原文：<https://javascript.plainenglish.io/how-to-become-a-react-developer-in-2022-here-is-the-complete-roadmap-faf645d17e11?source=collection_archive---------0----------------------->

React 是构建优秀、快速、可伸缩以及最重要的可重用前端的领先技术。根据 StackOverFlow 进行的开发者调查，React 是使用最多的 web 框架。2023 年，比以往任何时候都有更多的公司在寻找 React 开发者。

![](img/55c7ca463030ccdbeb39daefbbd68d7a.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# React.js 是什么？

js 是一个 JavaScript UI 库，由脸书创建，用于构建可伸缩的 UI 组件。它可以用于构建单页应用程序、移动应用程序、pwa。其受欢迎背后最重要的因素是较低的学习斜率。

在这篇文章中，我们将逐步了解如何成为一名 React 开发人员。

> 用 React 写的大部分非反应式代码都是 javaScript。

# 先决条件

**a. JavaScript**

由于 React 是一个 JavaScript 库，所以具备 JS 背景并理解一些重要概念是很重要的。React 现在包括 React 钩子和功能组件，建议学习 ES6。

**JavaScript 概念，你应该知道:**

1.  JS 中的变量
2.  箭头功能
3.  数据类型及其方法
4.  Dom 操作和事件
5.  高阶函数和回调函数
6.  承诺
7.  异步 JS

**b. HTML / CSS**

React 中的表示组件是使用 HTML 开发的，并通过 CSS 或第三方工具进行样式化。假设您正在创建一个按钮组件。该组件将有一个标签、样式和一些属性。更常见的是，HTML 按钮元素将用于创建该组件，并且将使用 CSS 或任何其他样式库进行样式化。

[Source: Giphy](https://giphy.com/)

# 要掌握的核心反应概念

1.  **虚拟 Dom 和差分算法**

React.js 的幕后是虚拟 dom 和 Diffing 算法，操作真实 dom 比较慢，所以 React 利用了虚拟 Dom 的概念。虚拟 dom 是真实 dom 的抽象。每次呈现组件或元素时，虚拟 dom 对象都会更新。然后，它将最近更新的虚拟 dom 与更新前的虚拟 dom 的副本进行比较，并确定要更新哪个 dom 对象。比较两个虚拟 DOM 的过程称为差分。在下一步中，用虚拟 dom 更新真实 dom，并且更新后的虚拟 dom 变成用于下一次 dom 改变的预更新虚拟 dom。

**2。JSX:反应模板语言**

JSX 可以称之为 React 的句法。它代表 **JavaScript XML** ，帮助用 JavaScript 编写 HTML 代码，并在 UI 上呈现您的定制组件。

```
const blog = 'programinja'You can add variable "blog" in "p" element by using power of JSX.<p>Blog: {blog}</p>
```

**3。** **组件:React 应用程序的构建模块**

React 应用程序包含 React 组件。从简单的按钮到复杂的仪表板图表，React 应用程序中的每样东西都是一个组件。下面的代码片段是一个简单的 React 组件，将在 UI 上呈现一个链接。

```
import React from 'react'const SimpleComponent = () => {
  return (
        <a href='https://www.google.com'>Google!</a>
  )
}export default SimpleComponent
```

该组件不可重用，因为其标签和 URL 是固定的。为了使一个组件可重复使用的道具进来。

**4。道具**

Props 是属性对象，用于在 React 组件之间传递**只读数据**。道具可以作为变量或对象在**单向流**中传递。

```
/// simpleComponent.jsimport React from 'react'const SimpleComponent = ({ label, url }) => {
  return (
        <a href={url}>{label}</a>
  )
}export default SimpleComponent
```

链接组件现在是可重用的，可以用不同的标签和 URL 呈现，如下面的代码片段所示。

```
/// index.jsimport SimpleComponent from './simpleComponent'const App = () => {
  return (
      <SimpleComponent label='Google!' url='https://www.google.com' />
    )
}
```

**5。状态管理**

*通俗地说，状态就是一个 Javascript 对象，存储着* ***可变*** *数据，可以被组件使用和更新。*状态的任何变化都会重新呈现组件。历史上，状态是与基于类的组件相关联的，但是，使用 useState / useReducer 挂钩，它可以在功能组件中进行管理。

可以通过调用 **useState hook** 在组件级管理状态，通过 Redux、Context API、反冲等状态管理解决方案在全局级管理状态。

**6。反应挂钩**

React 16.8 在 2018 年推出了钩子。React 挂钩帮助管理功能组件中的状态和生命周期方法，并使基于类的组件变得多余。钩子只能在功能组件和顶层使用。

**基本挂钩**

1.  使用状态
2.  使用效果
3.  使用上下文

**高级挂钩**

1.  用户教育
2.  使用回调
3.  使用备忘录
4.  useRef
5.  useImperativeHandle
6.  useLayoutEffect
7.  useDebugValue

```
import React, { useState } from 'react'const App = () => {const [sum, setSum] = useState(1) */// The initial value of sum is 1.*return (
  <>
    <button onClick={() => setSum(sum + 1)} >+</button
    <span>{sum}</span>
    <button disabled={sum === 1} onClick={() => setSum(sum - 1)}>-    </button>
  </>
  )
}export default App
```

在上面的组件中，状态是通过本地级别的 useState 钩子来管理的。

7。创建您自己的定制挂钩

可以创建定制挂钩来跨多个组件共享可重用的功能逻辑。例如，可以创建一个自定义挂钩来检测浏览器窗口宽度或从 API 获取数据，并在整个应用程序中使用。自定义挂钩从**开始使用**。

在下面的例子中，创建了一个自定义钩子，它返回浏览器窗口的宽度和高度。它可以用于移动响应等。

```
import { useLayoutEffect, useState } from 'react'const useWindowSize = () => {const [size, setSize] = useState([0, 0])useLayoutEffect(() => {const updateSize = () => {setSize([window.innerWidth, window.innerHeight])}window.addEventListener('resize', updateSize)updateSize()return () => window.removeEventListener('resize', updateSize)}, [])return size}export default useWindowSize
```

您可以使用 useWindowSize 挂钩来检测窗口宽度，并根据各自的屏幕大小呈现桌面或移动组件。

```
const NavBar = () => {
  const [width] = useWindowSize()
  return (
    width > 786 ? <Desktop /> : <Mobile />
  )
}
```

如果你已经掌握了这些概念，你就可以称自己是一个初级的 React 开发者了。但是，有一些更高层次的概念要学习，以击败人群。

# 高级 React 主题

1.  高阶组件
2.  代码分割
3.  参考文献
4.  上下文 API
5.  服务器端渲染
6.  反应悬念
7.  React 服务器组件

学会这些概念后，你可以称自己为 React 开发人员。

So now you have learnt basic and advanced level React. [Source: Giphy](https://giphy.com/)

但是，由于 React 本身是一个库，所以我们需要使用其他库和节点包，例如用于路由的 React Router、用于状态管理的 Redux 等，以利用更多的功能。

# 反应生态系统

1.  **React 路由器/ React 路由器 Dom**

React Router 是一个路由库，用于通过修改 URL 在 React 组件之间导航。当用户登录到一个 URL 时，React Router 将检测组件是否被设置为根据该路由器进行渲染，并在 UI 上进行渲染。

**2。通过第三方库进行状态管理**

尽管 React 通过 useState 钩子和上下文 API 提供了组件级和全局级的状态管理。然而，如果一个应用程序非常复杂，并且你想要更多的控制，可以使用第三方工具，如 **Redux** 、**反冲**、 **Mobx** 。*个人建议配合 useReducer 使用 Context API。*

**3。表格**

创建带有验证和其他功能的动态复杂表单需要使用库。**蚁酸**和**反应钩子表单**广泛用于创建表单。这些库无缝地处理表单的所有方面。Yup 广泛用于添加验证。

**4。反应测试**

反应测试的概念是测试你的组件是否如预期的那样运行。例如，您创建了一个输入字段，并希望它以某种方式运行。测试将被编写来迎合这些用例。自动化测试有助于稳定组件，减少手动测试，并立即捕获错误。开发人员为您的组件编写测试用例是非常重要的。Jest、Cypress 和 React 测试库被广泛用于测试 React apps。

**5。样式/用户界面库**

可以使用任何 UI 库，而不是创建 UI 组件，如模式、按钮、菜单、下拉菜单等。常见的例子有 [Material-UI](https://mui.com/) 、 [Antd](https://ant.design/) 、 [Bootstrap](https://react-bootstrap.github.io/) 。此外，还有多个样式库来创建你自己的样式，如[样式组件](https://styled-components.com/)、[顺风 CSS](https://tailwindcss.com/) 。

**6。处理 API**

多个基于 promises 的库正在提供与 Rest 和 GraphQL APIs 协同工作的出色解决方案。Axios、Superagent 和是 Rest APIs 的热门。阿波罗和接力主宰 GraphQL。

# 你应该学习的相关工具

1.  NPM
2.  饭桶
3.  网络包
4.  Heroku / Netlify
5.  Firebase / AWS 放大器

# 要构建的项目

1.  电子商务商店
2.  待办事项应用
3.  一个基本的 SAAS 应用

[Source: Giphy](https://giphy.com/)

恭喜你。学习完这些概念后，你现在就是一名 ninja React 开发者了。开始申请，继续学习。

感谢阅读。

在 LinkedIn 关注我:[https://www.linkedin.com/in/thealiraza](https://www.linkedin.com/in/thealiraza/)

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费周报**](http://newsletter.plainenglish.io/) 。关注我们 [**推特**](https://twitter.com/inPlainEngHQ) ，[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**，**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**，以及** [**不和**](https://discord.gg/GtDtUAvyhW) **。**

## 想用内容来扩展你的科技创业吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。

我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。