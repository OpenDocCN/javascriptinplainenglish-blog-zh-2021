# 使用 React 构建博客应用程序—完成项目

> 原文：<https://javascript.plainenglish.io/build-a-blog-app-with-react-finish-the-project-3f4bc4f24ece?source=collection_archive---------0----------------------->

## 第 4 部分:在项目的最后部分，我们将完成所有剩余的组件，并学习如何设置一个本地 JSON 服务器。

![](img/79bcad6a863598efe132994523a7cf77.png)

Photo by [Anete Lūsiņa](https://unsplash.com/@anete_lusina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好！因此，这将是 React 博客应用系列的第四部分，也是最后一部分。在第一部分中，我们讨论了如何开始一个新的 React 项目，并且我们学习了如何建立一个 Git 存储库来跟踪我们的变更。此外，我们还查看了 package.json 文件。

[](/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b) [## 使用 React 构建一个博客应用程序——介绍和设置(第 1 部分)

### 在第一部分中，我们处理项目的基础并设置它。

javascript.plainenglish.io](/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b) 

然后，在第二部分，我们开始构建我们的组件。首先，我们了解了所有组件的概况以及它们应该如何工作。接下来，我们构建了 Home 和 BlogList 组件。

[](/build-a-blog-app-with-react-building-components-part-2-5b079c7da924) [## 使用 React 构建组件构建博客应用程序(第 2 部分)

### 在第二部分中，我们开始构建博客应用程序所需的一些组件。

javascript.plainenglish.io](/build-a-blog-app-with-react-building-components-part-2-5b079c7da924) 

接下来，在第三部分中，我处理了其他重要的组件，比如 Blog detail 组件、Create new blog 组件和 useFetch 定制钩子。

[](/build-a-blog-app-with-react-components-and-hooks-part-3-facc1efe1fb3) [## 用 React 构建一个博客应用——组件和挂钩

### 第 3 部分—我们将在第 3 部分处理 BlogDetail，创建组件，并构建 useFetch 定制钩子。

javascript.plainenglish.io](/build-a-blog-app-with-react-components-and-hooks-part-3-facc1efe1fb3) 

现在，在第四部分，也是最后一部分，我将处理所有剩下的组件，我们将学习如何设置一个本地 JSON 服务器作为获取数据的服务器。

## 导航条组件

这个组件用于在我们的博客网站上显示导航栏。这将是一个简单的导航栏，有两个链接:-

1.  **主页** —点击此按钮，用户将进入主页。
2.  **创建博客** —点击此链接将用户带到新的博客创建页面。

我们在导航栏中还有一个显示我们网站名称的标题。

Navbar Component

## 未找到组件

每当用户导航到不存在的页面时，该组件都会在应用程序中显示 404 错误页面。

这是一个简单的 404 错误页面，有一个显示 404 错误的标题，一段文字说页面没有找到，我们还有一个主页链接。

Not Found Component

## 应用程序组件

该组件将所有其他组件绑定在一起，并使用浏览器路由器链接所有组件。

它导入所有需要的组件，还从 react-router-dom 导入 BrowserRouter、Route 和 Switch。

要了解 React 中浏览器路由器的更多信息，请浏览这个官方文档。

[](https://reactrouter.com/web/api/BrowserRouter) [## React 路由器:React 的声明式路由

### 学习一次，路线无处不在

reactrouter.com](https://reactrouter.com/web/api/BrowserRouter) 

然后我们显示 Navbar 组件，因为它在所有页面上都是通用的。然后我们启动一个开关组件。我们检查不同的路线，并显示对应于该特定路线的组件。

注意事项:-

1.  当路由到 Home 组件时，我们使用一个*精确路径*。因为*路径*匹配以给定 URL 为前缀的任何 URL，但是*精确路径*要求路径完全匹配。所以，我们使用这个路径而不是通常的路径，因为我们不希望所有的页面都路由到主页，因为它只是一个正斜杠，是所有路径的前缀。
2.  我们可以在其他组件中使用任何*路径*或*精确路径*，因为我们没有任何其他组件路径以它作为前缀。
3.  对于所有其他路径(未找到的路径)，我们使用*来捕获上面的任何路由未捕获的任何其他路径(在移动到下面的路由之前，路由首先检查上面的路径)。在这种情况下，我们启动 NotFound 组件。

App component

## Index.css

这是我们为这个应用程序使用的 CSS 文件。我不会解释它，因为它不是一个 CSS 教程。

Index CSS file

## 索引. js

这是索引文件，是我们应用程序的起点。我们不需要更改这个文件中的任何内容，我们会将它保留为默认值。

现在，我们已经完成了所有的组件。我们需要将所有其他文件保留为默认值。

我们想了解如何设置一个本地 JSON 服务器，作为我们的应用程序获取数据的真正服务器。

## json-server

我们将使用一个*[*JSON-server*](https://www.npmjs.com/package/json-server)*来构建我们的假 REST API。要安装 json-server，请键入以下命令:-**

```
**npm install -g json-server**
```

**然后我们将创建一个名为*数据、*的文件夹，然后我们将在*数据*文件夹中创建一个名为 *db.json* 的文件。**

**我们的 db.json 文件是:-**

**db.json**

**现在，要启动服务器，请键入以下命令:-**

```
**npx json-server - watch data/db.json - port 8000**
```

**我们正在定义保存需要查看的数据的位置。我们还定义了一个端口值 8000，用于在不同于 React 的服务器上触发。**

**这里，我们使用了[*npx*](https://docs.npmjs.com/cli/v7/commands/npx)*来运行命令，这允许我们从本地或远程 npm 包运行命令。所以，如果你早一点安装包，我们就不需要用 *npx* 。但是如果你没有安装，我们需要使用 *npx。npx* 首先下载所需的包，如果本地没有，然后运行命令。***

**因此，我们的 json 服务器已经启动并运行，我们可以在不同的端口上启动 React 应用程序，并在浏览器中查看它，以检查一切是否正常。**

**现在，如果你想托管你的 React 应用，Jacob 的这篇文章是一个很好的资源。**

**[](https://medium.com/swlh/the-easiest-way-to-deploy-a-react-app-c7e613035822) [## 部署 React 应用程序的最简单方法

### 你会相信你可以在几分钟内从零开始将你的 React 应用程序部署到互联网上吗？网络生活使之成为可能…

medium.com](https://medium.com/swlh/the-easiest-way-to-deploy-a-react-app-c7e613035822) 

这都是为了这部分。我们已经完成了基本系列。我以后可能会更新这个系列的实际后端，但这对于现在来说已经足够了。

所以，我希望你喜欢阅读这个系列，并学到一些有价值的东西。

写完这篇文章后还有更多文章要读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，以了解 DRF 和 REST APIs 是如何工作的，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](/build-a-simple-todo-app-using-next-js-f88b68761e27) [## 使用 Next.js 构建一个简单的 Todo 应用程序

### 让我们用 Next.js 构建一个简单的 Todo 应用程序，它教你 CRUD 的基本原理(创建、读取、更新和…

javascript.plainenglish.io](/build-a-simple-todo-app-using-next-js-f88b68761e27) [](https://towardsdatascience.com/build-a-simple-todo-app-using-react-a492adc9c8a4) [## 使用 React 构建一个简单的 Todo 应用程序

### 让我们用 React 构建一个简单的 Todo 应用程序，教你 CRUD 的基本原理(创建、读取、更新和…

towardsdatascience.com](https://towardsdatascience.com/build-a-simple-todo-app-using-react-a492adc9c8a4) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)**