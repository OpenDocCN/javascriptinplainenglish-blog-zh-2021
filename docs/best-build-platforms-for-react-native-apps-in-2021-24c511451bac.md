# 2021 年 React 原生应用的最佳构建平台

> 原文：<https://javascript.plainenglish.io/best-build-platforms-for-react-native-apps-in-2021-24c511451bac?source=collection_archive---------6----------------------->

## React 本地应用的最佳 CI/CD 服务对比

![](img/0805b461f44e7441673517c7427d3ec4.png)

市场上有许多可用于 React 原生应用的 CI/CD 平台。然而，每个平台在某些方面都是独特的。一些平台最适合团队，支持协作，而另一些平台很简单，专注于完成工作。因此，选择符合您需求的平台非常重要。

本文将讨论 React 原生项目的 CI/CD 服务提供商，以帮助您选择合适的平台来构建您的应用程序。

# GitHub 操作

[GitHub Actions](https://github.com/features/actions) 是 GitHub 提供的自动化工作流服务。如果你使用 GitHub 进行版本控制，使用 GitHub 操作会更方便，把所有东西都放在一个地方。

> 有了 GitHub Actions，你可以为你的开源 React 原生 Android 或 iOS 应用获得无限的免费运行时间。

此外，您可以每月获得 2000 分钟的免费构建时间，并为私有存储库提供 500 MB 的存储空间。他们还有非常实惠的现收现付定价计划。

## 赞成的意见

*   更好的 Android 和 iOS 构建时间
*   易于复制工作流程
*   最佳定价方案

## 骗局

*   单点登录(SSO)不适用于免费或团队计划

您可以从下面的文章中了解如何使用 GitHub 操作来自动化 React 本机构建。

[](https://blog.usejournal.com/automate-react-native-builds-with-github-actions-af54212d26dc) [## 用 GitHub 动作自动化 React 本机构建

### 自 2019 年起，GitHub 通过其特性 GitHub Actions 原生支持 CI/CD。凭借其简单的 YAML 配置，巨大的…

blog.usejournal.com](https://blog.usejournal.com/automate-react-native-builds-with-github-actions-af54212d26dc) 

# 切尔莱西

有了 [CircleCI](https://circleci.com/circleci-react/) ，你可以开始在 GitHub 或 Bitbucket 中免费构建你的公共 React 原生项目。

> 他们为开源的 macOS 版本提供每月 25，000 英镑(每年 180 美元)的免费积分。

定价的重点是你的构建消耗了多少 CPU。第一个容器是免费的，您可以在其中运行一个构建。如果您想要更多的并行性或更高的吞吐量，您必须升级到付费套餐。他们最便宜的套餐是三个用户每月 15 美元。

## 赞成的意见

*   运行容器中的 SSH 允许更容易的调试

## 骗局

*   私有项目的免费计划不提供 macOS VM

[](https://github.com/CircleCI-Public/circleci-demo-react-native) [## circle ci-Public/circle ci-demo-react-native

### 运行 yarn 来安装 JS 依赖项。运行纱线测试来运行 JS 测试(通过 jest)。运行纱线开始运行应用程序在…

github.com](https://github.com/CircleCI-Public/circleci-demo-react-native) 

# 世博会

[世博会](https://expo.io/)为 universal React 项目提供了一个框架和平台。由于它的简单性、易用性和最短的启动时间，它是最流行的平台之一。直到最近，为了使用他们的构建平台，我们不得不在开发应用程序时使用 Expo 框架。

> 然而，Expo 引入了新的 [EAS 构建和提交](https://blog.expo.io/expo-application-services-eas-build-and-submit-fc1d1476aa2e)服务，允许您构建和提交 React 本地应用程序，而无需使用它们的框架。

他们仍然可以作为预览功能，只能通过付费计划访问，直到他们从预览中毕业。世博会为商业项目提供了一个真正有用的免费计划。但是，您将需要一个付费计划，以避免在高峰时间在云队列中等待 10 或 20 分钟。

## 赞成的意见

*   非常方便构建 React 本地项目
*   跨平台构建
*   慷慨的免费计划

## 骗局

*   在空闲计划的高峰期，在构建队列中等待

[](https://expo.io/) [## 世博会

### 构建一个可在您所有用户的设备上本机运行的项目加入 200，000 多名开发人员，包括通过编辑开始…

世博会](https://expo.io/) 

# Appcircle

[Appcircle](https://appcircle.io/) 为任何从事移动应用的人提供企业级 DevOps，从行业内的初创公司到超大型公司。他们的免费包每月只允许 20 个构建，但是他们提供定制的包供企业使用。

他们的开发者计划对开源项目是免费的，包括每月 200 次构建和 10GB 存储。

> 与其他平台相比，Android 的 React 原生项目构建时间有点长，但 iOS 的构建时间很短。

总的来说，Appcircle 更适合企业使用。

## 赞成的意见

*   为开源项目提供更多存储和构建

## 骗局

*   Android 构建时间相对较长

[](https://appcircle.io/blog/guide-to-automated-mobile-ci-cd-for-react-native-appcircle/) [## 使用 Appcircle 进行 React Native 的自动化移动 CI/CD 指南

### 阅读时间:8 分钟 Appcircle 是一个移动 CI/CD 平台，它提供了一个完全自动化的环境来管理…

appcircle.io](https://appcircle.io/blog/guide-to-automated-mobile-ci-cd-for-react-native-appcircle/) 

# 好朋友

[巴迪](https://buddy.works/)免费计划每月提供 120 条管道运行，其中有一条并行管道。Buddy 是自由职业者的理想选择，因为它提供了许多功能。它允许您以最小的学习曲线来开发和定制您的部署和测试。

> 然而，Buddy iOS 部署尚未到来，但您可以在早期访问中[尝试一下](https://buddy.works/ios)。

他们的 Pro 计划提供 10GB 的高速缓存存储和许多其他功能，每月 75 美元。Android React 原生项目的构建时间相当不错。

## 赞成的意见

*   图形用户界面非常容易使用
*   提供更多功能

## 骗局

*   相对更贵

[](https://buddy.works/docs/quickstart/react-native) [## React Native | Docs | Buddy 的 CI/CD:devo PS 自动化平台

### Buddy 允许您创建交付管道，该管道将在单个……

巴迪. works](https://buddy.works/docs/quickstart/react-native) 

# 信号量 CI

像 GitHub Actions 一样， [Semaphore](https://semaphoreci.com/) 为开源项目提供无限构建。他们还为私人项目提供了一个免费的计划，允许每月用一个并发管道进行 100 次构建。Semaphore 非常适合个人项目、早期 MVP 和类似的少量开发活动。

> 我对他们在 Android 和 iOS React Native 上的构建速度非常着迷。超级快。

不幸的是，免费计划不包括 Android 或 iOS 构建支持。

## 赞成的意见

*   出色的客户支持
*   更好的管道可视化和用户友好界面

## 骗局

*   不支持重新启动单个作业，当前唯一的选择是重新运行整个构建
*   对于多个项目来说，成本可能很高

您可以在下面的 GitHub 资源库中查看为 React 本地应用程序设置信号量 CI/CD 管道的演示。

[](https://github.com/semaphoreci-demos/semaphore-demo-react-native) [## semaphore ci-demos/semaphore-demo-react-native

### 示例应用程序和 CI/CD 管道展示了如何在 Semaphore 2.0 上运行 React 本地项目。使用反应原生…

github.com](https://github.com/semaphoreci-demos/semaphore-demo-react-native) 

# 比特莱斯

[Bitrise](https://www.bitrise.io/) 为公共存储库提供免费的无限构建，添加无限的团队成员，以及构建日志以便于调试。对于组织精英计划，他们提供更快的构建和更多增强的功能。

> Bitrise 也是基于 G2 用户满意度评级的最高评级的持续集成平台。

由于 Bitrise 完全专注于移动，他们与 iOS 合作得很好。Bitrise 最适合开发团队，作为 React 原生项目的一个方便的 CI/CD 平台。

## 赞成的意见

*   开源项目的无限团队成员
*   易用性

## 骗局

*   Android 和 iOS 项目的构建时间非常长(使用标准构建机器)
*   45 分钟构建超时

[](https://www.bitrise.io/why/technologies/react-native-continuous-integration) [## 反应本地持续集成和交付

### 脸书 React Native SDK 内置的移动应用 CI/CD。为移动开发平台构建的 CI/CD:连接、配置…

www.bitrise.io](https://www.bitrise.io/why/technologies/react-native-continuous-integration) 

# 结论

CI/CD 的主要目标是为开发人员节省时间，并保持代码库和最终应用程序的质量。在选择构建平台时，您应该考虑定价、构建时间、缓存存储、vCPU、并发管道等等，以找到满足您需求的完美匹配平台。

本文讨论了 React 本机应用程序的各种 CI/CD 服务提供者的优缺点。我希望它能帮助你找到最适合你的 React 本地应用的平台。

如果你想知道 2021 年要用的十大 React 原生组件库是什么，可以查看下面链接的我的文章。

[](https://blog.bitsrc.io/top-react-native-component-libraries-to-use-in-2021-cce60f81ae08) [## 2021 年将使用的顶级 React 本机组件库

### 2021 年，反应原生图书馆让你的生活更轻松

blog.bitsrc.io](https://blog.bitsrc.io/top-react-native-component-libraries-to-use-in-2021-cce60f81ae08) 

本文到此为止。感谢您的阅读，祝您编码愉快。