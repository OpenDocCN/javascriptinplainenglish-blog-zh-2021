# 使用 React 构建组件构建博客应用程序(第 2 部分)

> 原文：<https://javascript.plainenglish.io/build-a-blog-app-with-react-building-components-part-2-5b079c7da924?source=collection_archive---------1----------------------->

## 在第二部分中，我们构建了博客应用程序所需的一些组件。

![](img/2242075a181ead38f71a5a980e737cc4.png)

Photo by [Anete Lūsiņa](https://unsplash.com/@anete_lusina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好！所以，这将是我已经开始的新 React 博客应用系列的第二部分。在第一部分中，我们讨论了如何开始一个新的 React 项目，并且我们学习了如何建立一个 Git 存储库来跟踪我们的变更。此外，我们还查看了 package.json 文件。

所以，还没有读第一部分的人，请先读第一部分，然后继续读这一部分

[](/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b) [## 使用 React 构建一个博客应用程序——介绍和设置(第 1 部分)

### 在第一部分中，我们处理项目的基础并设置它。

javascript.plainenglish.io](/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b) 

在第二部分，我们将开始实际的构建过程。我们现在将开始构建组件。我们所有的工作都将放在 *src* 文件夹中。

在构建项目时，我们将遵循模块化的方法，将所有不同的任务分成不同的文件，以避免混乱。

我们将使用*浏览器*来帮助我们为我们网站的不同部分建立不同的网页，并在 *App.js* 文件中链接它们。

要详细了解路由在 React 中是如何工作的，我推荐你看看 Edmond Atto 的这篇精彩文章。

[](https://medium.com/the-andela-way/understanding-the-fundamentals-of-routing-in-react-b29f806b157e) [## 了解 React 中路由的基础知识

### 本书第五章；vumbula React——与 John Kagga 合著

medium.com](https://medium.com/the-andela-way/understanding-the-fundamentals-of-routing-in-react-b29f806b157e) 

因此，我们将拥有各种组件，我们将在本文和后续文章中逐一构建这些组件。

因此，让我们快速浏览一下我们将要构建的所有文件，以及每个文件的用途

1.  **App.js** —它是我们 App 的主要组成部分。它使用 BrowserRouter 链接我们所有不同的页面，并给它们路径和组件来加载该页面。
2.  **Home.js** —是我们博客网站的主页，以列表形式展示所有博客。它不包含以列表格式显示博客的逻辑，但是它调用 BlogList 组件并将博客传递给该组件以显示博客。home 组件使用我们稍后将创建的 useFetch 自定义挂钩来获取博客。
3.  **BlogList.js** —它从 Home 组件接收博客并显示它们。
4.  **BlogDetails.js —** 它是获取单个博客并将其显示在单独页面上的组件。
5.  **Create.js** —您可以在这里创建新博客，并将其添加到以前的博客列表中。
6.  **Navbar.js** —这是将在每个页面上显示导航栏的 Navbar 组件。
7.  **NotFound.js** —这是当用户登陆到一个不存在的页面时，我们要加载的页面。这将是一个 404 错误页面。
8.  **index.js** —它是加载我们的 App.js 文件的默认文件。
9.  **useFetch.js** —这是我们将创建的自定义钩子，用于从我们将要创建的本地 JSON 服务器获取数据。
10.  index.css —这是保存我们所有样式的 css 文件。我们不会关注这一部分，因为它不是一个 CSS 教程。

我现在开始一个接一个地构建组件。那么，我们开始吧。

## 家用部件

它是显示我们博客网站主页的组件。我们将在 home 组件文件中导入 BlogList 组件和 useFetch 定制钩子。

我们将在本系列的后面创建 BlogList 组件和 useFetch 挂钩。

现在，我们假设它们存在，并且我们将在 Home 组件中使用这些组件。此外，如前所述，我们知道我们导入的两个组件的用途。

我们使用 useFetch 定制钩子并传入本地 JSON 数据库的 URL。我们会收到三种类型的数据——博客、未决事件和错误。

1.  **blogs** —它保存了本地 JSON 数据库中所有的博客。
2.  **isPending** —这有助于我们了解当前是否正在获取数据，以及我们是否需要等待一段时间才能完全获取和显示数据。
3.  **错误** —这包含我们从本地 JSON 服务器获取数据时可能遇到的任何错误。

然后，我们使用条件显示格式来显示我们需要以一种更加用户友好的格式智能显示的内容。

我们只在有错误时才显示错误。每当我们有任何错误时，它就会启动，然后显示该错误。

接下来，我们检查 isPending。如果这是真的，我们会显示一条加载消息，让用户知道博客当前正在被加载。

最后，我们将博客和标题传递给 BlogList 组件，该组件在列表中显示博客。

Home Component

## 博客组件

接下来，我们想讨论博客组件。我们在 Home 组件中调用了 BlogList 组件，并通过该组件传入了要显示的博客和标题。

在这里，我们首先从`react-router-dom`导入*链接*。Link 可以帮助我们将任何一段文字或图片链接到一个 URL。它的工作方式类似于锚标记，但是它使用本地保存的数据，而不是再次调用服务器；因此，它不需要刷新页面，有助于我们的应用程序成为单页面应用程序。

然后，我们从主页组件接收博客和标题。然后我们开始我们的 JSX，在其中我们显示标题，然后遍历博客。我们映射*博客，将*作为一个单独的*博客，*然后使用博客的 id 作为映射的关键字。然后我们显示博客的标题和作者的名字。

我们将这两条信息放在一个链接中，该链接链接到我们将完整显示单个博客的页面。

BlogList Component

所以，这将是所有的第二部分。我们将在下一部分讨论 BlogDetails 和 Create components，以及 useFetch 定制钩子。

我希望你喜欢这部分，我会很快写下下面的部分。我希望你感到兴奋，并能够学到一些好的东西。

以下部分是:-

[](/build-a-blog-app-with-react-components-and-hooks-part-3-facc1efe1fb3) [## 用 React 构建一个博客应用——组件和挂钩

### 第 3 部分—我们将在第 3 部分处理 BlogDetail，创建组件，并构建 useFetch 定制钩子。

javascript.plainenglish.io](/build-a-blog-app-with-react-components-and-hooks-part-3-facc1efe1fb3) [](/build-a-blog-app-with-react-finish-the-project-3f4bc4f24ece) [## 使用 React 构建博客应用程序—完成项目

### 第 4 部分:在项目的最后部分，我们将完成所有剩余的组件，并学习如何建立一个本地…

javascript.plainenglish.io](/build-a-blog-app-with-react-finish-the-project-3f4bc4f24ece) 

看完这篇文章后还有更多文章要读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，以了解 DRF 和 REST APIs 是如何工作的，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](https://towardsdatascience.com/build-a-rest-api-with-node-express-and-mongodb-937ff95f23a5) [## 用 Node，Express 和 MongoDB 构建一个 REST API

### 让我们使用 Node、Express 和 MongoDB 构建一个遵循 CRUD 原则的 REST API，并使用 Postman 测试它。

towardsdatascience.com](https://towardsdatascience.com/build-a-rest-api-with-node-express-and-mongodb-937ff95f23a5) [](/build-a-simple-todo-app-using-next-js-f88b68761e27) [## 使用 Next.js 构建一个简单的 Todo 应用程序

### 让我们用 Next.js 构建一个简单的 Todo 应用程序，它教你 CRUD 的基本原理(创建、读取、更新和…

javascript.plainenglish.io](/build-a-simple-todo-app-using-next-js-f88b68761e27) 

感谢阅读！