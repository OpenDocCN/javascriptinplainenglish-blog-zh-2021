# 使用 React 构建博客应用程序—介绍和设置

> 原文：<https://javascript.plainenglish.io/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b?source=collection_archive---------1----------------------->

## 第 1 部分:在第一部分中，我们处理项目的基础并设置它。

![](img/9e19a4a774d9039b8eb81bdbd3f74a15.png)

Photo by [Anete Lūsiņa](https://unsplash.com/@anete_lusina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好！学习的最好方法是通过实践。因此，让我们使用 React 构建一个简单的博客应用程序来了解事情是如何工作的。我们不会制作一个功能丰富、设计酷的博客网站。相反，这很简单——服务于学习的目的。

这将是一个简单的博客网站，功能很少，使你能学得更好。

我们将在这个博客中加入的特色是:-

1.  从本地 JSON 服务器获取博客并以列表形式显示博客。
2.  获取个人博客的详细信息并显示出来。
3.  添加新博客。
4.  删除博客。

这将是纯粹的反应，我们不会为这个博客网站使用任何后端服务器。因此，我们所做的更改，即我们删除或添加的博客，将在页面刷新后重置。所以，它不会在任何服务器上保存任何数据。

这一系列文章目前是针对初学者的，所以我们将详细介绍所有的内容，这样您就可以了解事情是如何工作的，并且能够实现更多的功能。

在本系列教程的初始阶段，我们将只使用 React，不使用后端或云来存储任何数据。一旦我们刷新页面，一切都会重置。

但是，稍后，我计划给这个 React 项目添加一个后端，使它成为全栈的。我们将使用 Express、Node.js 和 MongoDB 来构建这个应用程序的后端，然后连接前端和后端。

此外，如果该系列文章获得了良好的反响，我会在该系列的更多部分中添加更多的功能，包括身份验证和其他一些功能，使其更加实用。但是我们把这些东西留到以后，可能会添加也可能不会添加。

所以，现在让我们把重点放在初始阶段，它主要是针对初学者的。

## 那么，什么是反应呢？

React 是一个基于 Javascript 的库，用于构建网站的前端。React 是开发人员构建任何网站前端的最受欢迎的选择。

Eric Elliott 对 React 的介绍是一篇很棒的文章，适合任何刚接触 React 的人，以及想了解它是如何工作的，它为什么受欢迎以及如何开始使用它的人。

[](https://medium.com/javascript-scene/the-missing-introduction-to-react-62837cb2fd76) [## 反应过来的缺失介绍

### 为什么 React 是世界顶级 UI 框架

medium.com](https://medium.com/javascript-scene/the-missing-introduction-to-react-62837cb2fd76) 

另外，我想把这本[巨著](https://medium.com/pragmatic-programmers/table-of-contents-8c3f2d6f16ab) *和[实用程序员](https://medium.com/pragmatic-programmers)的真实*联系起来。这是一本学习 React 的好书，在 Medium 上有售。

因此，让我们从在我们的机器上安装节点包管理器(npm)开始。你可以到 [npm 网站](https://www.npmjs.com/get-npm)去做。

安装 npm 之后，让我们转到我们想要的目录来构建我们的项目。

我们将使用 *create-react-app* 来构建 react 项目。为此，我们可以在终端上键入以下命令:

```
npx create-react-app react-blog
```

这里，npx 是与 npm 捆绑在一起的包运行工具。因此，上面的代码行在名为 *react-blog 的文件夹中创建了一个新的 React 项目。*

它还将创建一个基本的 React 程序。我们看到其中有一个 package.json 文件。此外，我们还有节点模块、一个名为 src 的文件夹和一个公共文件夹。

我们的大部分工作将在 src 文件夹中完成。这是我们的 package.json 文件。

在 package.json 文件中，我们发现 React 需要许多依赖项才能工作。Create React App 已经为我们安装了这些。我们也有各种脚本来执行项目中的各种功能。

例如，运行命令`npm start`将为我们启动开发服务器，并在浏览器中打开我们的 React 应用程序。

当我们运行该命令时，我们会看到 React 网站，它是用 Create React 应用程序预先构建的。我们将删除所有这些预先建立的内容，然后开始建立我们自己的博客网站。

我们还将为我们的项目建立一个 Github 存储库，我们将在每次更改后保持更新，以跟踪更改，并在出现问题时恢复到以前的状态。在从事任何项目时，这都是一个很好的实践。

因此，让我们在 Github 上构建一个新的存储库，并将其命名为 *react-blog。*然后，我们在项目文件夹中初始化一个新的 Git Repo。

```
git init
```

然后，我们使用以下命令将它与 Github 存储库链接起来

```
gir remote add origin your-repo
```

然后，我们将现有文件添加到前面初始化的 git repo 中。我们可以通过以下方式做到这一点

```
git add -A
```

然后，我们通过以下方式提交 Git 存储库

```
git commit -m "First commit"
```

最后，我们可以通过编写以下代码将所有本地 Git 存储库推送到 Github 存储库

```
git push origin master
```

我们已经准备好开始建设这个项目。因此，我们必须重复这三个步骤— `git add`、`git commit`和`git push`，在我们做出每个重大变更后更新我们的存储库。

这是第一部分。我们将从下一部分开始构建我们的博客项目，并详细讨论所有必要的内容。

我希望你喜欢这个新系列开始。我希望你对这个新系列感到兴奋，我很想听到你的反馈。

以下部分是:-

[](/build-a-blog-app-with-react-building-components-part-2-5b079c7da924) [## 使用 React 构建组件构建博客应用程序(第 2 部分)

### 在第二部分中，我们开始构建博客应用程序所需的一些组件。

javascript.plainenglish.io](/build-a-blog-app-with-react-building-components-part-2-5b079c7da924) [](/build-a-blog-app-with-react-components-and-hooks-part-3-facc1efe1fb3) [## 用 React 构建一个博客应用——组件和挂钩

### 第 3 部分—我们将在第 3 部分处理 BlogDetail，创建组件，并构建 useFetch 定制钩子。

javascript.plainenglish.io](/build-a-blog-app-with-react-components-and-hooks-part-3-facc1efe1fb3) [](/build-a-blog-app-with-react-finish-the-project-3f4bc4f24ece) [## 使用 React 构建博客应用程序—完成项目

### 第 4 部分:在项目的最后部分，我们将完成所有剩余的组件，并学习如何建立一个本地…

javascript.plainenglish.io](/build-a-blog-app-with-react-finish-the-project-3f4bc4f24ece) 

看完这篇文章后还有更多文章要读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，了解 DRF 和 REST APIs 如何工作，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](https://towardsdatascience.com/build-a-rest-api-with-node-express-and-mongodb-937ff95f23a5) [## 用 Node，Express 和 MongoDB 构建一个 REST API

### 让我们使用 Node、Express 和 MongoDB 构建一个遵循 CRUD 原则的 REST API，并使用 Postman 测试它。

towardsdatascience.com](https://towardsdatascience.com/build-a-rest-api-with-node-express-and-mongodb-937ff95f23a5) [](/build-a-simple-todo-app-using-next-js-f88b68761e27) [## 使用 Next.js 构建一个简单的 Todo 应用程序

### 让我们用 Next.js 构建一个简单的 Todo 应用程序，它教你 CRUD 的基本原理(创建、读取、更新和…

javascript.plainenglish.io](/build-a-simple-todo-app-using-next-js-f88b68761e27) 

## 进一步阅读

[](https://bit.cloud/blog/how-to-build-a-composable-blog-l1jkl9f4) [## 如何建立一个可组合的博客

### 从头开始创建一个博客需要很多。有许多移动的部件组合在一起形成一个…

比特云](https://bit.cloud/blog/how-to-build-a-composable-blog-l1jkl9f4) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****