# 45 个 NPM 软件包解决 16 个 React 问题

> 原文：<https://javascript.plainenglish.io/45-npm-packages-to-solve-16-react-problems-a9ab18946224?source=collection_archive---------0----------------------->

## 关于如何选择完美的 npm 包的深入指导

![](img/e7c55854e1d08b6574031d26471ad8f7.png)

Photo by [cottonbro](https://www.pexels.com/@cottonbro?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/man-in-black-crew-neck-t-shirt-sitting-on-brown-sofa-4553272/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

React 简直太棒了。它很受欢迎，很有表演性。但是 React 的一个重要方面是，它并没有打包所有的解决方案。

这就是为什么我们需要寻找额外的库，这些库有好有坏。如果你是一个初学者，那么你必须花相当多的时间来寻找解决问题的最佳方案。

今天，我们将进行对比讨论，以了解更多关于 react 中不同问题的备选解决方案

# 1.全局状态管理

在 99%的应用程序中，组件之间共享状态是强制性的。有一些好的解决方案——本地的和外部的。

## 被推荐的

如果你问我一个解决方案，我会说 **Redux** 。不是因为它是最好的，而是因为它是最实用的。许多公司已经在使用它，你将不得不在某个时候使用它。

*   `[redux](https://redux.js.org/)`同`[react-redux](https://react-redux.js.org/)`

此外，生态系统也很棒。你几乎可以找到任何问题的解决方案。redux 附带的一些很棒的库有:

*   `[redux-thunk](https://github.com/reduxjs/redux-thunk)` - >用于处理异步动作。
*   `[redux-persist](https://github.com/rt2zz/redux-persist)` - >用于本地存储数据(离线支持)。
*   `[reselect](https://github.com/reduxjs/reselect)` - >用于对店铺进行更快的查询。

## 可供选择的事物

*   `[context](https://reactjs.org/docs/context.html)` - >内置反应。适合简单使用。对性能不好。尤其是当您有大量不断变化的数据时。
*   `[recoil](https://recoiljs.org/)` - >为解决特定问题而设计。不适用于所有用例。先了解一下！你可以在这里了解更多[。](/state-management-in-react-with-recoil-984cfc1fcd63)
*   `[mobx](https://mobx.js.org/README.html)` - >遵循观察者模式。适用于反应式编程。不应在任何新项目中使用。

# 2.服务器状态管理

如果您的应用程序严重依赖某些外部数据源，那么管理这些数据(缓存、预取等)对于性能来说是至关重要的。

## 被推荐的

我个人是`react-query`的超级粉丝，还有很多人和我一样。它就像魔法一样管用。

*   `[react-query](https://react-query.tanstack.com/)`

它处理`caching`陈旧的数据，以及更多开箱即用的东西。它简单、强大、可配置！

## 供选择的

游戏里还有一个玩家叫`**SWR**`。这是一个类似于 React Query 的库。

*   `[SWR](https://swr.vercel.app/)`

这个库的主要好处是它是由 Vercel 构建的。他们是创造 NextJS 的同一批人。所以在使用 **NextJS 时，你可以期待更好的性能。**

# 3.脚手架

[从头开始创建 React 应用](https://betterprogramming.pub/complete-guideline-to-creating-a-modern-react-app-with-typescript-from-scratch-cebbb5817d8)很复杂。设置`Webpack`、`Bable`等会让人望而生畏！

## 被推荐的

`[NextJS](/start-your-journey-with-next-js-958705cfc299)`是我从头开始创建 React 应用程序时的选择。它被称为全栈 React 框架。

*   `[NextJS](https://nextjs.org/)`

在文件中，它说，

> Next.js 为您提供了最佳的开发人员体验，包括生产所需的所有功能:混合静态和服务器渲染、类型脚本支持、智能绑定、路径预取等等。不需要配置。

这其中最重要的特性是它的开箱即用的 SEO 支持。这太好了！你也可以做`[SEO in React](/3-easy-ways-to-solve-seo-problems-in-react-applications-d3d7873dc494)`。但它不像 Next 那样简单。

## 供选择的

如果您从 React 或构建一些基本项目开始，那么您有其他选择。

*   `[create-react-app](https://github.com/facebook/create-react-app)` - >构建单页面应用。适合初学者。
*   `[gatsby](https://www.gatsbyjs.org/)` - >构建静态内容导向型网站。不适合其他用例。

# 4.表单处理

90%的 web 应用程序都有某种形式。和处理表单输入是一件非常痛苦的事情。但是我们有一些好消息！

## 被推荐的

**React hook form** 是最新最伟大的(据我说:P)表单处理库。它的性能非常好，非常灵活。

*   `[react-hook-form](https://react-hook-form.com/)`

它对一些外部设计库有很好的支持，比如`material-ui`和`ant-design`。

[](/how-to-use-react-hook-form-with-typescript-2cf597c0c45f) [## 如何在 TypeScript 中使用 React Hook 表单

### 为您的应用程序构建高性能、简洁的表单

javascript.plainenglish.io](/how-to-use-react-hook-form-with-typescript-2cf597c0c45f) 

## 可供选择的事物

这个领域有一些很好的替代品。

*   `[Formik](https://formik.org/)` - > Formik 为输入验证、格式化、屏蔽、数组和错误处理提供了久经考验的解决方案。
*   `redux-form` - >不用。这会严重影响表演。

# 5.HTTP 呼叫

在现代世界中，几乎所有的网站都依赖于一些外部数据源。所以进行 HTTP 调用是非常琐碎的。

## 被推荐的

Fetch 是进行 HTTP 调用的推荐方法。

*   `[fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)`

它具有有限但强大的功能。它可以支持您 95%的工作负载。

## 供选择的

**Axios** 是对 fetch 的改进。很受欢迎。

*   `[axios](https://www.npmjs.com/package/axios)`

它有一些不错的特性，比如内置的 XSRF 保护和自动 JSON 转换，以及拦截 HTTP 调用的能力。如果你需要，你应该去争取。

# 6.式样

你需要做造型。这是毫无疑问的。有多种方法来设计你的应用程序。

## 被推荐的

许多人可能不同意我的观点。但是我认为当谈到 React 应用程序的样式时，样式化组件是最好的选择。

*   `[styled-components](https://styled-components.com/)`

它有助于创建关注点清晰分离的干净组件。此外，它很容易通过 props 管理和配置。

## 可供选择的事物

然而，正如我所说的，还有其他很好的选择！

*   `[plain old css](https://www.w3.org/Style/CSS/Overview.en.html)` - >支持开箱即用。对于较小的项目应该没问题。
*   `[sass](https://sass-lang.com/)` - >对 CSS 的改进。它为管理 CSS 提供了很好的特性。适用于中型甚至更大的项目。
*   `[styled-jsx](https://github.com/vercel/styled-jsx)` - >一个有很多类似`styled-components`功能的库。到处都有一些额外的功能。

# 7.用户界面库

在许多情况下，手工设计所有组件可能不是一个好主意。在这种情况下，使用某种 UI 库可能是个好主意。

## 被推荐的

对我来说最通用和可配置的 UI 库是 Material UI。

*   `[material-ui](https://material-ui.com/)`

它非常受欢迎，被许多公司使用。它高度可配置，这就是它如此强大的原因。

## 可供选择的事物

也有一些不错的选择。

*   `[semantic-ui](https://semantic-ui.com/)` - >内置组件多。
*   `[ant-design](https://ant.design/)` - >较少配置。有限但很好的组件。
*   `[chakra-ui](https://chakra-ui.com/)` - >最近人气高涨。

# 8.证明文件

好的文档可以在未来节省数百个小时。所以要积极主动，在项目的早期就采用文档库。

## 被推荐的

创建文档的推荐方法是 React StyleGuidist。

*   `[react-styleguidist](https://react-styleguidist.js.org/)`

很好用，真的很强大。

[](/document-your-react-applications-the-right-way-f648053c3a70) [## 以正确的方式记录 React 应用程序

### 逐步介绍指南

javascript.plainenglish.io](/document-your-react-applications-the-right-way-f648053c3a70) 

## 可供选择的事物

还有一些其他的选择。

*   `[js-docs](https://jsdoc.app/index.html)`->JavaScript 通用文档工具。
*   `[react-docz](https://www.docz.site/)` - >非常易用的文档指南。值得一试。

# 9.多语言支持

如果您正在构建一个全球性的产品，那么您可能希望在 React 应用程序中添加多语言支持。

## 被推荐的

**React i18next** 是[在 React 应用](/implement-multi-language-support-in-react-9854c52ddb55)中实现多语言支持的实际选项。

*   `[react-i18next](https://react.i18next.com/)`
*   `[i18next](https://www.npmjs.com/package/i18next)`

## 可供选择的事物

还有其他一些好的选择。

*   `[react-intl](https://www.npmjs.com/package/react-intl)`

这也支持其他库，比如 VueJS 和 Angular。

[](/implement-multi-language-support-in-react-9854c52ddb55) [## 在 React 中实现多语言支持

### 6 个简单的步骤

javascript.plainenglish.io](/implement-multi-language-support-in-react-9854c52ddb55) 

# 10.动画

动画让你的应用变得生动。在 React 中使用动画有一些不错的选择。

## 被推荐的

普通 CSS 是动画 React 应用程序的最佳方式。简单快捷。此外，这是更高的性能。

*   `[Plain CSS Animations](https://www.w3schools.com/css/css3_animations.asp)`

## 可供选择的事物

如果你想要现成的东西，这里有一些推荐给你

*   `[framer-motion](https://www.framer.com/motion/)` - >制作就绪动画
*   `[react-awesome-reveal](https://www.npmjs.com/package/react-awesome-reveal)` - >这用于简单的动画来展示一个组件
*   `[react-spring](https://react-spring.io/)` - >又一个伟大的现成库。

# 11.长列表呈现

呈现一个长列表会严重影响应用程序的性能。在这种情况下使用库可能是个好主意。

## 被推荐的

如果你有某种无限滚动的应用程序，那么你应该考虑**反应窗口**

*   `[react-window](https://react-window.vercel.app/)`

## 供选择的

如果你不需要一个无限滚动的列表，那么你就可以对数据进行分页

*   `[react-paginate](https://www.npmjs.com/package/react-paginate)`

[](https://betterprogramming.pub/how-to-improve-rendering-performance-in-a-1-000-item-react-list-85be129b8c0d) [## 如何提高包含 1000 个条目的 React 列表的渲染性能

### 让我们确保我们的 web 应用程序能够高效滚动

better 编程. pub](https://betterprogramming.pub/how-to-improve-rendering-performance-in-a-1-000-item-react-list-85be129b8c0d) 

# 12.代码质量工具

Linters 可以静态地发现你代码中的任何错误。使用某种棉绒是个好主意。

## 被推荐的

首选解决方案是 Eslint

*   `[eslint](https://eslint.org/)`

## 供选择的

*   `[jshint](https://jshint.com/)` - >旧图书馆
*   `[tslint](https://palantir.github.io/tslint/)` - >打字稿用的短打。现在不推荐。

[](/how-to-add-linting-and-formatting-for-your-react-app-78227b328910) [## 如何为你的 React 应用添加林挺和格式

### 做好这一点，否则你的代码会有问题

javascript.plainenglish.io](/how-to-add-linting-and-formatting-for-your-react-app-78227b328910) 

# 13.格式化

对于任何应用程序来说，拥有一致的视觉样式都是非常重要的，代码格式化程序可以为您完成这项工作！

## 被推荐的

*   `[Prettier](https://prettier.io/)`

这对你来说是最好的解决方案。你不需要别的了！

# 14.分析学

数据是未来。如今，大多数企业都是数据驱动的。因此，为您的应用提供一个好的分析工具非常非常重要！

## 被推荐的

最流行和最强大的工具是 React Ga。

*   [react-ga](https://github.com/react-ga/react-ga)

我想你不需要别的东西了。

[](/how-to-setup-and-add-google-analytics-to-your-react-app-fd361f47ac7b) [## 如何设置谷歌分析并将其添加到 React 应用程序中

### 谷歌让洞察你的网络应用变得非常容易

javascript.plainenglish.io](/how-to-setup-and-add-google-analytics-to-your-react-app-fd361f47ac7b) 

# 15.测试

我不需要重申测试对于任何应用程序是多么重要。所以给你。

## 被推荐的

推荐的方法是 React 测试库

*   [反应-测试-库](https://testing-library.com/docs/react-testing-library/intro/)

它非常易于使用，并设计为遵循现实生活中的使用。

## 可供选择的事物

*   `[jest](https://jestjs.io/)` - >用于单元测试
*   `[cypress](https://www.cypress.io/)` - >进行端到端测试

[](https://betterprogramming.pub/everything-you-need-to-get-started-with-testing-in-react-e16819b0eba7) [## 在 React 中开始测试所需的一切

### 给初学者的简明介绍

better 编程. pub](https://betterprogramming.pub/everything-you-need-to-get-started-with-testing-in-react-e16819b0eba7) 

# 16.构建可共享组件

如果你在一个大的团队中，那么轻松地共享组件会成为一个大问题！

## 被推荐的

如果你正在寻找最完整的解决方案，故事书是一个不错的选择

*   [故事书](https://storybook.js.org/)

就是这样。我想现在你对什么时候选择哪个库已经有了很好的理解。如果你有任何不同意见，请告诉我。

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) **或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**