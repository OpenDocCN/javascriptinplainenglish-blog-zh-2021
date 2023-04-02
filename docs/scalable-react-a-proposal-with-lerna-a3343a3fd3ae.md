# 可伸缩 React:与 Lerna 的一个提议

> 原文：<https://javascript.plainenglish.io/scalable-react-a-proposal-with-lerna-a3343a3fd3ae?source=collection_archive---------12----------------------->

## 大型项目的 React/Redux 文件结构

![](img/2f3ca8a54f292e408f155da748cd401d.png)

Photo by [lukechesser](https://unsplash.com/@lukechesser) on [Unsplash](https://unsplash.com/s/photos/growth)

# 什么是可扩展性

对于高风险的大型项目，可伸缩性是圣杯。很少完全实现，一篇优秀的论文把它分成四个部分。

前三个不言自明:**负载**可伸缩性、**性能**可伸缩性、**空间**可伸缩性。

最后一个可能更难理解，也是今天讨论的内容:**结构性**可伸缩性。从[介绍**可扩展性的特点及其对性能的影响**](https://www.win.tue.nl/~johanl/educ/2II45/2010/Lit/Scalability-bondi%202000.pdf) :

> 结构可伸缩性是一个系统在一个选定的维度上扩展而不需要对其架构进行重大修改的能力。

从 computertechreviews 给出了另一个定义:

> 结构可伸缩性是系统的标志，其实现不会显著阻碍在自定义范围内增加对象的数量。

[](https://www.computertechreviews.com/definition/scalability/#Time-Spatial_Scalability) [## 什么是可伸缩性？定义、类型、功能等

### 可伸缩性是一个 IT 系统的能力。系统能够适应硬件和软件性能的提高或降低…

www.computertechreviews.com](https://www.computertechreviews.com/definition/scalability/#Time-Spatial_Scalability) 

在 web 应用程序的环境中，今天的基础设施和云计算服务使得获得**负载**、**性能、**和**空间**可伸缩性变得相当简单。现在，如何用更简单的术语定义**结构**可伸缩性，并实现它？

当谈到软件开发时，结构可伸缩性可以被看作是以稳定的速度添加新功能的能力。它意味着作为一个团队来计划、创造和交付。

常见实践有助于实现结构可伸缩性，其中包括:

*   版本控制系统(GIT、CVS)
*   合适的自动化工作流(GitFlow、语义发布)
*   质量流程(SonarQube，…)
*   证明文件
*   测试

这些实践解决了关于团队工作的问题。在某种程度上，它们也有助于保持从计划到交付的稳定速度。

# React 有什么问题

我在加入 React project 时面临的最大问题总是一样的:架构。在软件中，架构是最重要的基础之一。如果仓促行事，可能会在短短几个月内拖垮一个项目。

在当今时代，许多制作精良的框架都是可用的，它们都带有自己的架构，旨在进行扩展。

但是 React 不在其中。 React 是一个库，对你的组件和[文件结构](https://reactjs.org/docs/faq-structure.html)没有意见。同样的[也适用于 Redux](https://redux.js.org/faq/code-structure) 。

作为一名对软件架构和 React 充满热情的工程师，这几年来一直是一场噩梦。在我的旅程中，我从一个多年来不断改进的基本结构开始。

> 我在这里的目的不是提供代码示例，而是讨论项目组织，重点是文件结构。
> 
> 每个文件的内容，如何编写函数和组件，导出它们可以根据您喜欢的实践而改变。

## 开始

像每个人一样，我从一个基本项目和一个**组件/** 目录开始:

```
my-app
├── src
│   ├── components
│       ├── Component.js
├── package.json
```

事实上…这是一个好的开始。当你只需要一个简单的图形来展示时，一个**组件/** 目录就可以完成这项工作。

现在，我们想要创建复杂的应用程序。我们的需求包括:

*   使用[导航](https://reactrouter.com/web/guides/quick-start)。
*   存储[全局状态](https://redux.js.org/)。
*   发送[请求](https://axios-http.com/)到我们的服务器。
*   编写[类型化的 JavaScript](https://www.typescriptlang.org/) 。

## 航行

有时候，简单更好。这就是为什么我添加了一个**导航/** 目录来处理导航。

我使用一个 **Routes** 组件来定义我的可能页面列表，一个 **PublicRoute** 组件来处理连接用户不应该访问的页面，一个 **PrivateRoute** 组件用于连接用户:

```
my-app
├── src
│   ├── components
│       ├── Component.js
│   ├── navigation
│       ├── PrivateRoute.js
│       ├── PublicRoute.js
│       ├── Routes.js
├── package.json
```

在我的 **Routes** 文件中，我需要每页使用一个组件。开始时，它们位于**组件/** 目录中，但这产生了两个问题:

*   当需要时，这些页面更难找到。
*   **组件/** 目录已经存储了很多文件。

相反，我创建了一个 **screens/** 目录，其唯一目的是存储页面专用的组件:

```
my-app
├── src
│   ├── components
│       ├── Component.js
│   ├── navigation
│       ├── PrivateRoute.js
│       ├── PublicRoute.js
│       ├── Routes.js 
│   ├── screens
│       ├── HomeScreen.js
├── package.json
```

## Redux

关于 **Redux** ，我是用一个常用的模式开始的。即使在今天，我还能看到它被我加入的团队使用，尽管对我来说，它更像是一种反模式。

[Redux](https://redux.js.org/faq/code-structure) 将它作为大多数 Redux 开发人员倾向于使用的*常见模式来谈论*:

> Rails-style:用于“动作”、“常数”、“缩减器”、“容器”和“组件”的独立文件夹

实际上，如下所示:

```
my-app
├── src
│   ├── store.js
│   ├── components
│       ├── Component.js
│   ├── navigation
│       ├── PrivateRoute.js
│       ├── PublicRoute.js
│       ├── Routes.js
│   ├── screens
│       ├── HomeScreen.js
│   ├── actions
│       ├── xActions.js
│   ├── reducers
│       ├── rootReducer.js
│       ├── xReducer.js
├── package.json
```

很长一段时间，我的软件架构师告诉我有什么不对劲，但是我不知道具体是什么。

那是直到我一直在 Redux 文档上徘徊。我是不是说 Redux 没有怀孕？是的，除了最后一部分:[风格指南](https://redux.js.org/style-guide/style-guide)。

[](https://redux.js.org/style-guide/style-guide) [## 风格指南| Redux

### 这是编写 Redux 代码的官方风格指南。它列出了我们推荐的模式、最佳实践和…

redux.js.org](https://redux.js.org/style-guide/style-guide) 

《Redux Style guide》的简介告诉我们以下内容:

> Redux 核心库和大部分 Redux 文档都是未绑定的。有很多种使用 Redux 的方式，而且很多时候都没有一种“正确”的方式来做事情。
> 
> 然而，时间和经验表明，对于某些主题，某些方法比其他方法更有效。此外，许多开发商要求我们提供官方指导，以减少决策疲劳。

关于我们的目录，我们强烈建议[将文件作为具有单文件逻辑的特征文件夹](http://Structure Files as Feature Folders with Single-File Logic):

> 虽然旧的 Redux 代码库通常使用“逐类型文件夹”的方法，将“动作”和“缩减器”分开，但是将相关的逻辑放在一起可以更容易地找到和更新代码。

该文档甚至给了我们两种以这种方式实现 Redux 的方法: [Redux Toolkit](https://redux-toolkit.js.org/) 和[duck](https://github.com/erikras/ducks-modular-redux)。这些都是很好的解决方案，在类型上比我们的文件夹要好，但是我没有使用它们中的任何一个。原因是，我喜欢 [Redux-Saga](https://redux-saga.js.org/) ，它可以解决我所有的副作用问题。

Redux Toolkit 改为与 Redux Thunk 一起工作。另一方面，即使 Ducks [给出了 Redux Thunk](https://github.com/cyrilluce/saga-duck) 的例子，也有人建议使用 Redux-Saga 实现[。](https://github.com/cyrilluce/saga-duck)

不幸的是，这个实现很重，没有说服我。相反，我保留了每个功能都有一个 **store/** 文件夹和另一个文件夹的想法，同时仍然分离文件类型:

```
my-app
├── src
│   ├── components
│       ├── Component.js
│   ├── navigation
│       ├── PrivateRoute.js
│       ├── PublicRoute.js
│       ├── Routes.js
│   ├── screens
│       ├── HomeScreen.js
│   ├── store
│       ├── store.js
│       ├── rootReducer.ts
│       ├── xFeature
│           ├── actions.js
│           ├── reducer.js
│           ├── saga.js
├── package.json
```

## 要求

我开发的每个应用程序都需要以某种方式获取外部数据。最常见的用例是使用 [axios](https://github.com/axios/axios) 从 web 服务请求数据。

这里没有什么复杂的，我仍然通过使用一个**服务/** 文件夹将相关的逻辑放在一起，每个公共端点一个文件。

例如，在一个博客应用程序中，我将有一个文件专用于登录，另一个文件专用于创建和获取文章。

```
my-app
├── src
│   ├── components
│       ├── Component.js
│   ├── navigation
│       ├── PrivateRoute.js
│       ├── PublicRoute.js
│       ├── Routes.js
│   ├── screens
│       ├── HomeScreen.js
│   ├── store
│       ├── store.js
│       ├── rootReducer.ts
│       ├── xFeature
│           ├── actions.js
│           ├── reducer.js
│           ├── saga.js
│   ├── services
│       ├── xService.js
├── package.json
```

## 以打字打的文件

当我使用 TypeScript 时，我的结构需要一点小小的改变。主要是用**重命名我的文件。ts** 扩展并添加一个**类型/** 文件夹:

```
my-app
├── src
│   ├── components
│       ├── Component.tsx
│   ├── navigation
│       ├── PrivateRoute.tsx
│       ├── PublicRoute.tsx
│       ├── Routes.tsx
│   ├── screens
│       ├── HomeScreen.tsx
│   ├── store
│       ├── store.ts
│       ├── rootReducer.ts
│       ├── xFeature
│           ├── actions.ts
│           ├── reducer.ts
│           ├── saga.ts
│   ├── services
│       ├── xService.ts
│   ├── types
│       ├── xType.ts
├── package.json
├── tsconfig.json
```

## 完成

我不时会遇到新的问题。

首先，使用环境变量和其他指定的值。为了以一致的方式访问这些值，我决定添加一个 **constants/** 目录。同样，将公共值保存在同一个文件中。

然后，我开始需要定制方法来测试、转换对象或处理函数。这些不是库，而是我的应用程序所需的小函数。我想出了一个 **utils/** 目录和每期一个文件。

我意识到 **utils** 被认为是一种反模式，在 OOP 中可能更多。在我们的 JavaScript 用例中，utils 模块的良好设置对我来说是可以接受的。

最后，对于专用于给定特性的 React 组件，我可以很容易地在 **components/** 中创建子目录。但是常见的反应元件如**按钮**或**卡**呢？我没有把它们存储在根目录下的**组件/** 目录中，而是很快发现了片段的概念。

在每个应用中重复使用公共组件可以存储在**片段/** 子目录中:

```
my-app
├── src
│   ├── components
│       ├── fragments
│           ├── Button.tsx
│       ├── Component.tsx
│   ├── constants
│       ├── xConstants.ts
│   ├── navigation
│       ├── PrivateRoute.tsx
│       ├── PublicRoute.tsx
│       ├── Routes.tsx
│   ├── screens
│       ├── HomeScreen.tsx
│   ├── store
│       ├── store.ts
│       ├── rootReducer.ts
│       ├── xFeature
│           ├── actions.ts
│           ├── reducer.ts
│           ├── saga.ts
│   ├── services
│       ├── xService.ts
│   ├── types
│       ├── xType.ts
│   ├── utils
│       ├── xUtils.ts
├── package.json
├── tsconfig.json
```

# 勒娜呢。

以前的结构对我这边的很多项目来说都很棒。我和几个中小型团队一起工作了几个月，效率很高。

但是更大规模的项目呢？花费数年时间和数十(或数百)名开发人员开发更多功能的开发？

我很确定，在某个时候，添加一个特性的时间会成倍增加，开发成本也会成倍增加。这是我开始对一个我讨厌的工具感兴趣的主要原因: *Lerna* 。

 [## 一个用多个包管理 JavaScript 项目的工具。

### 将大型代码库分割成单独的独立版本包对于代码共享非常有用…

lerna.js.org](https://lerna.js.org/) 

## 概观

> 将大型代码库分割成单独的独立版本包对于代码共享非常有用。然而，跨许多存储库进行变更是很麻烦的，并且难以跟踪，跨存储库的测试很快变得复杂。

在实践中，Lerna 帮助您在一个单一的 GIT 存储库中创建和管理一个被分割成多个模块的项目。例如:

*   您有一个依赖于后端应用程序的前端，但在保持同步和维护这两个存储库方面有困难。Lerna 可能是一个很好的解决方案。
*   同样，您可能有一个依赖于多个库的复杂应用程序。与其分别维护应用程序和每个包，不如为它们创建一个单独的存储库，并用 Lerna 管理一切，这样可以节省时间。

根据我的经验，Lerna 是在浪费时间。它应该有助于分离和链接模块，执行所有包的命令(如测试或质量检查)并提供其他实用程序。

我所面临的是时间的流失。事实上，我见过 Lerna 的项目中管道配置很差。这导致当只有一个模块被更新时，启动所有模块的 QA 和/或部署过程，即使那些模块没有受到影响。此外，单一回购结构混乱且难以操作，真是一场噩梦。

这些经历仍然让我得以瞥一眼 Lerna，并理解它试图解决的问题。

# Lerna & React

几个月后，当我询问我的 React 应用程序的文件结构/架构时，Lerna 想到了这个问题。

我对用我的 React 应用程序在 monorepo 中维护我的后端不感兴趣。我也没有使用自定义库。我的目标是，在一个 React 项目中，允许大量开发人员同时处理几个功能，而没有架构的障碍。

随着时间的推移和更多的功能，前面提到的体系结构促使开发人员为每项功能创建嵌套目录:

*   每个目录和子目录都变得很大
*   寻找给定的组件变得非常耗时
*   添加新元素会使情况变得更糟
*   随着时间的推移，生产力会下降

我想到的解决方案是，不要在我的整个应用程序中有一个包，而是为每个功能创建一个包，并创建一个具有入口点角色的包。如何管理那些包？**蕾娜**。

在实践中，我将 Lerna 与[纱线工作空间](https://classic.yarnpkg.com/en/docs/workspaces/)一起使用。一个基本的项目应该是这样的:

```
monorepo
├── packages
│   ├── package1
│   ├── package2
│   ├── package3
├── package.json
├── lerna.json
├── yarn.lock
```

但是我正在开发一个 React 应用程序。我想将每个功能分离到不同的模块中，但我仍然需要一个入口点来:

*   引导 React 应用程序
*   设置导航
*   设置冗余

这就是为什么我的第一步是创建这个“入口点”模块，我称之为核心。你猜怎么着，我以前的架构工作得非常好，所以我将重用它:

```
monorepo
├── packages
│   ├── core
│       ├── public
│       ├── src
│          ├── components
│              ├── AppProvider.tsx
│          ├── navigation
│              ├── PrivateRoute.tsx
│              ├── AppProvider.tsx
│              ├── Routes.tsx
│          ├── store
│              ├── index.ts
│              ├── rootReducer.ts
│              ├── sagas.ts
│          ├── index.tsx
│       ├── package.json
        ├── tsconfig.json
├── package.json
├── tsconfig.json
├── lerna.json
├── yarn.lock
```

这里，核心包是用 create-react-app 生成的。我通常设置我的提供者并调用 *AppProvider* 文件中的 *Routes* 组件。然后这个文件由 index.js 导入并引导。

在 *Routes.tsx* 中，我将从其他模块导入屏幕，并使用我的 *PublicRoute* 和 *PrivateRoute。*

在 **store/** 目录中，索引文件使用 *rootReducer* 和 sagas 文件，以构建一个有效的 Reducer。另一方面， *rootReducer.ts* 从其他模块导入并组合 Reducer，而 *sagas.ts* 对 saga workers 也是如此。

## 模块

我想把我的核心目录和其他功能模块分开。为了尊重这个组织，我在**核心/** 旁边设置了一个**模块/** 目录。

然后，我为每个功能创建另一个子目录，同时仍然使用相同的结构。这些模块使用 index.js 文件来重新导出它们的所有内容，以便于导入。

```
monorepo
├── packages
│   ├── core
│       ├── ....
│   ├── modules
│       ├── xFeature
│          ├── src
│              ├── components
│              ├── store
│              ├── screens
│              ├── services
│              ├── types
│          ├── package.json
│          ├── tsconfig.json
│          ├── index.js
├── package.json
├── tsconfig.json
├── lerna.json
├── yarn.lock
```

## 巩固

随着时间的推移，我在这个结构中加入了一些元素:

首先，一个**普通**模块。我之前讲过一个**片段/** 目录，存放在哪里？**通用**模块。也许你有一些自定义的钩子，在你的应用程序中到处都可以使用。同样适用，将它们存储在**公共**模块中。

由于我正在使用带有[自定义渲染](https://testing-library.com/docs/react-testing-library/setup/)的[测试库](https://testing-library.com/)，我需要定义几个关于测试的函数。将所有内容都存储在 **common/** 目录中会使其过于复杂。相反，我可以在与**内核相同的级别上创建一个**测试**模块。这是一个简化我的测试的好方法，同时仍然将**模块/** 目录用于功能。**

我的单元测试存储在测试文件旁边的 __tests__ 目录中。另一方面，当我编写端到端测试时，我会创建一个不同的目录。在这里，看起来像是一个 **e2e/** 目录，紧挨着**核心/** 和**测试/** 就可以了，不会让我的结构变得更复杂。

最终结果如下所示:

```
monorepo
├── packages
│   ├── core
│       ├── ....
│   ├── e2e
│       ├── ....
│   ├── testing
│       ├── ....
│   ├── modules
│       ├── common
│          ├── ...
│       ├── xFeature
│          ├── ...
├── package.json
├── tsconfig.json
├── lerna.json
├── yarn.lock
```

## 不利方面

从我的经验来看，这种结构对于大型项目非常有效，但是:

*   **Lerna** 和**纱线工作空间**可能很难配置。
*   你(和你的团队)必须学会如何使用 **Lerna** 。
*   开始需要一些时间。
*   对于小型和独立的项目，创建、理解和使用这种结构所需的时间是不值得的。
*   前面提到的大多数结构都可以重新用于 React Native。不幸的是，本机模块和 Lerna 可能很难使用。

## 结论

感谢您的阅读。我希望你已经发现这是有用的和有益的。如果你有任何问题，请在评论中告诉我。谢谢！

[](https://morintd.medium.com/about-me-teddy-morin-9fb1d65fe24e) [## 关于我——泰迪·莫林

### 嗨，我是泰迪，一个反应的爱人🚀。

morintd.medium.com](https://morintd.medium.com/about-me-teddy-morin-9fb1d65fe24e) 

*更多内容看*[***plain English . io***](https://plainenglish.io/)