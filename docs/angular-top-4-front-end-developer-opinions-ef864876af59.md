# angular:4 大前端开发者观点

> 原文：<https://javascript.plainenglish.io/angular-top-4-front-end-developer-opinions-ef864876af59?source=collection_archive---------4----------------------->

## 前端开发人员对 Angular(重写)的主要看法。

![](img/cd728ae71309e1b422bd29b646a5dd78.png)

Photo by [Kindel Media](https://www.pexels.com/@kindelmedia?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/man-vacation-love-people-6774153/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

什么是框架？

嗯，如果你问我，框架类似于木匠的工具箱。它配有一系列工具，让木匠的工作变得轻松。工具包里的一切都是为了让他变得强大和高效。木匠知道他可以用工具箱里的工具完成不同的任务。

就像木匠和他的工具包一样，作为前端开发人员，我们的优势不是只有一个工具包，而是有很多。我们有特权选择 per project，这是一个简化和加速我们开发到生产的工具包。

[React](https://reactjs.org/) 、 [Angular](https://angular.io/) 和 [Vue.js](https://vuejs.org/) 在 [Stack Overflow 2020 开发者调查](https://insights.stackoverflow.com/survey/2020#most-popular-technologies)中被全球 65，000 名开发者评为优秀的 web 框架。

这些框架是我们前端开发人员拥有的三个最顶层的工具包。一个小小的免责声明，包括我自己在内的许多开发人员，将会把 React 看得更像一个库。

根据个人判断，Vue.js 和 React 适合于构建小型到中型的 web 应用程序，团队规模很小——不超过三个人。而 Angular，我相信它在大规模企业应用程序方面做得非常出色，涉及的团队超过了三个人。

在这篇文章中，我分享了一些关于 Angular 的常见开发者观点，并分享了我个人对这些观点的典型回应。

# Angular 有一个陡峭的学习曲线

我完全同意 Angular 有一个陡峭的学习曲线。这种情绪更多地由没有后端编程经验的前端开发人员表达——使用 Java、Go 等语言，这些语言具有类、继承、静态类型等概念。

在学习 Angular 的时候，你也学习了软件开发的原则和模式，这些在其他的 web 框架比如 Vue.js 和 React 中是不必要的。

任何使用 Angular 进行构建的开发人员都必须学习并掌握起码的概念，如[依赖注入](https://angular.io/guide/dependency-injection)、服务和提供者、装饰者、类，以充分利用框架的能力。

## 我的回应

尽管这些概念的学习曲线可能很陡，但它们是通用的编程概念，当开发人员意识到这些概念时，他们就会成为全面发展的开发人员。

了解 Angular 引入的一些有用概念(如依赖注入、服务、装饰器)的开发人员拥有交叉适用的知识。这些知识适用于编程的其他领域，而不仅仅是 web 开发和前端开发。

# Angular 很固执己见

从很多开发人员那里听到这种观点并不少见，尤其是 React 和 Vue.js 开发人员。我经常从这两个阵营中读到 Angular 是刚性的，和它一起工作感觉像是逆潮运动。

是啊！诚然，棱角要求你以特定的方式做事。它规定了您的项目结构和文件命名约定。它也决定了你如何做其他重要的事情。

web 框架的角度迫使您:

1.  使用名为 Typescript 的强类型语言
2.  使用用 [RxJS](https://rxjs.dev/) 库实现的可观察模式。
3.  使用依赖注入和服务来实现模块化和可重用性。

与 React 和 [Vue.js](https://vuejs.org/) 等其他 web 框架相比，这些强制约束和其他基本架构决策让 Angular 感觉很复杂。

## 我的回应

谷歌的 Angular 团队正在寻求建立一个能够扩展业务的框架。Angular 的目标是帮助开发人员构建企业级的解决方案，减少开发人员和团队之间的摩擦。

Angular 是一个为规模设计的框架。企业可以添加和扩展他们的业务解决方案来满足规模，而无需浪费时间重新思考架构设计和决策。

Angular 提高了生产力，因为采用它的企业或明或暗地同意 Angular 的架构设计。这消除或减少了未来开发人员之间关于什么是正确的做事方法的争论和冲突。在使用 Vue.js 和 React 等灵活的库和框架时，其中一些东西经常会出现问题。

让新开发人员加入 Angular 项目会更快更顺利，因为基本的决策和约定已经由框架负责了。新开发人员不必期待任何大的惊喜，因为惯例和偏好是基本的，并且已经由 Angular 决定了。

像 Angular 这样固执己见的框架意味着需要做的决策更少。您的团队可以专注于构建产品，而不是争论诸如

*   样式和命名约定
*   项目和文件结构
*   设计模式的实现，例如(SRP、Decorators、依赖注入、Observable)

一些有争议的问题已经得到了解决，并被纳入了 Angular。可观测量是 [@angular/common/http](https://angular.io/api/common/http) 模块的核心。

模块化和可重用性是依赖注入和服务的首要考虑因素。

# 角度对于原型来说是复杂的

我遇到过前端开发人员，他们抨击 Angular 的原因是它太重了，尤其是对于原型开发和概念验证来说。他们常常沮丧地认为 Angular 需要巨大的投资，但回报却很少。

大多数持这种观点的开发人员都不会忘记提到，与其他框架相比，Angular 中即使是最简单的事情也需要冗长的代码——比如创建组件、指令、服务等等。

Angular 中几乎所有的东西都需要使用类。

## 我的回应

对 Angular 有这种情绪的开发者是完全正确的。如果你只是构建一个简单的一次性应用程序，Angular 确实有点过了。

我会建议你考虑 React 或 Vue.js 或 speed，如果你只是在做原型，而对你正在构建的应用程序没有明确的方向感的话。

团队和项目经理对他们的项目有一个宏伟的愿景和方向，对应用程序的潜在未来规模有一个预期，会持有相反的意见。

对于中小型项目来说，经历 Angular 的复杂性所带来的回报是无法体会和体会的。它更像是从事大型企业应用的团队。

使用 Angular 所面临的挑战必须被认为是一项前期投资，这将使大型项目的后续开发过程更加顺利。

所以我的观点是，如果你的应用是小型到中型的，并且需要更换部件，那么采用 Angular 是一种完全的过度破坏和不值得的做法。

# Angular 主要使用 Typescript

一些前端开发人员对 Typescript 是 Angular 中的主要语言这一事实并不兴奋。

这很大程度上是因为这些开发人员不喜欢 Typescript。

发现很难欣赏 Angular 的开发人员也很难欣赏 Typescript。

这些开发人员不喜欢 Angular，因为他们不喜欢 Typescript。

通常反对打字稿理由包括:

1.  Typescript 是一种静态类型的编程语言
2.  Typescript 冗长
3.  Typescript 需要像 Babel 这样的转换工具将 Typescript 转换成浏览器支持的 Javascript (ES5)
4.  Typescript 要求学习新的语法和结构。
5.  Typescript 降低了开发人员的生产力

## 我的回应

我认为没有一种语言比另一种语言更好。一门语言好不好，是有语境的，受不同因素影响。

Typescript 似乎在没有后端开发经验或经验很少的前端开发人员中名声不佳。像我这样的 Fullstack 开发人员非常欣赏使用 Typescript 的好处。

因此，就这一点而言，我对 Typescript 的看法与这一观点相反，它是编写 Javascript 代码的一大进步。

Typescript 是 Javascript 的超集，包含了 ES5 和 ES6 中的所有特性，并扩展了它们的类型支持和编译时错误检查。

正如我在前面的回答中提到的，如果你正在开发一个简单的应用程序，Angular 可能是一个错误的选择；对于 Typescript 也是如此。

任何从事大型应用程序开发的团队都会体会到使用 Typescript 的好处。这些好处包括:

1.  使用高级类型的健壮且可维护的代码库
2.  使用内置类型和自定义类型的丰富域建模
3.  增加分布式团队在共享源代码上的努力。
4.  自动完成和提高开发速度。

## 最后的想法

Angular 是一个很棒的框架。React 和 Vue.js 同样很棒。但是，使 Angular 变得复杂并且看起来对有 React 和 Vue.js 经验的开发人员没有好处的观点，也是使 Angular 在处理需要规模和大型开发团队的大型企业级应用程序时成为一个好选择的观点。

结论是，如果你正在寻找一个具有这些能力的框架，除了所有的负面意见之外，还要考虑 Angular。

1.  面向大规模和企业级应用的框架。
2.  一个用于分布式团队共享代码库的框架。
3.  一个鼓励代码持久性、可维护性和可重用性的框架。
4.  一个保证稳定增长速度和生产力的框架。

## 你可能也会喜欢这些

[](https://levelup.gitconnected.com/the-6-things-every-good-software-developer-i-know-religiously-does-fd6dd9c2c8f7) [## 我所知道的每一个优秀的软件开发人员都会认真做的 6 件事

### 我认识的每个优秀的软件开发人员都会做这些事情

levelup.gitconnected.com](https://levelup.gitconnected.com/the-6-things-every-good-software-developer-i-know-religiously-does-fd6dd9c2c8f7) [](https://levelup.gitconnected.com/please-refactor-these-blocks-of-code-c7d2b6f2e4ce) [## 请重构这些代码块

### 我知道它们有用，但是请让我们去掉这些代码的味道

levelup.gitconnected.com](https://levelup.gitconnected.com/please-refactor-these-blocks-of-code-c7d2b6f2e4ce) [](https://medium.com/analytics-vidhya/13-git-commands-i-use-daily-14e3ad562068) [## 我每天使用的 13 个 Git 命令

### 您需要知道这些命令

medium.com](https://medium.com/analytics-vidhya/13-git-commands-i-use-daily-14e3ad562068) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)