# 用 React 构建一个博客应用——组件和挂钩

> 原文：<https://javascript.plainenglish.io/build-a-blog-app-with-react-components-and-hooks-part-3-facc1efe1fb3?source=collection_archive---------5----------------------->

## 第 3 部分—我们将在第 3 部分处理 BlogDetail，创建组件，并构建 useFetch 定制钩子。

![](img/6cf5bf677e71cd52e874b7c821158361.png)

Photo by [Anete Lūsiņa](https://unsplash.com/@anete_lusina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好！所以，这将是 React 博客应用系列的第三部分。在第一部分中，我们讨论了如何开始一个新的 React 项目，并且我们学习了如何建立一个 Git 存储库来跟踪我们的变更。此外，我们还查看了 package.json 文件。

[](/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b) [## 使用 React 构建一个博客应用程序——介绍和设置(第 1 部分)

### 在第一部分中，我们处理项目的基础并设置它。

javascript.plainenglish.io](/build-a-blog-app-with-react-intro-and-set-up-part-1-ddf5c674d25b) 

然后，在第二部分，我们开始构建我们的组件。首先，我们了解了所有组件的概况以及它们应该如何工作。接下来，我们构建了 Home 和 BlogList 组件。

[](/build-a-blog-app-with-react-building-components-part-2-5b079c7da924) [## 使用 React 构建组件构建博客应用程序(第 2 部分)

### 在第二部分中，我们开始构建博客应用程序所需的一些组件。

javascript.plainenglish.io](/build-a-blog-app-with-react-building-components-part-2-5b079c7da924) 

在第三部分中，我将处理其他重要的组件，如 Blog detail 组件、Create new blog 组件和 useFetch 自定义钩子。

然后，我将在本系列的第四部分中包括所有其他组件和本地服务器部分。

如果你想了解更多关于 React 定制钩子的知识，这篇由 Mayank Gupta 撰写的文章是一个很好的资源。

[](https://medium.com/technofunnel/creating-custom-react-hooks-9d4f382359bb) [## 创建自定义 React 挂钩

### 要在 React 中创建自定义挂钩，您只需知道…

medium.com](https://medium.com/technofunnel/creating-custom-react-hooks-9d4f382359bb) 

## 博客详细信息组件

这是我们获取和显示单个博客文章的组件。因此，正如您所记得的，我们使用一个传入网址的链接来调用这个组件。因此，我们在 URL 中包含了一个博客的 id 作为参数。

因此，我们将使用`*getParams()*`钩子提取 id。然后，我们使用我们的 *useFetch* 定制钩子，通过在 useFetch 钩子中传递 id 来获取特定的博客。

我们还使用了一个名为`useHistory()`的钩子，它创建了一个历史堆栈，并从该堆栈中推送或弹出元素。最后，我们将访问的组件或页面存储在历史堆栈中。

然后，我们像在 BlogList 组件中一样显示博文。我们还利用了使用条件操作符的`isPending`和`error`数据来构建更好的用户体验。

我们还有一个删除博客的按钮。我们可以通过点击那个博客来删除它。这个按钮有一个`*handleClick*`功能来处理博客上任何点击。

在`*handleClick*` 函数中，我们获取博客并通过 *DELETE* 方法删除博客。然后，我们将主页 URL 推送到历史堆栈，在博客被删除后将用户重定向到主页。

## 创建组件

这是我们用来在 React 应用程序中创建新博客的组件。它使用了两个钩子:`*useState*` 和`*useHistory*` *。*

然后，我们构建创建功能组件。我们使用`*useState*`钩子来创建和设置不同的字段。例如，我们想要构建一个表单来将博客文章添加到我们的应用程序中。因此，我们有几个字段，我们希望作者在发布博客之前填写。

我们已经将`*title*`*`*body*`*`*author*`*和* `*isPending*`变量声明了。我们还有一个变量`*history*` ，它是从`*useHistory*` *得到的。***

**默认情况下，标题和正文字段保持空白。我们将 author 字段设置为默认名称，因为我们目前将 author 字段设置为选择字段。你可以自由选择自己的方式。理想情况下，它应该是空白的，应该留给作者自己来填充。**

**`isPending`默认设置为假。它表示我们是否在等待添加博客。**

**我们构建了一个带有提交按钮的基本表单，并使用了`setTitle`、`setAuthor`、`setBody`函数在我们填写表单时动态设置变量。**

**我们有一个名为`*handleSubmit*` 的函数来处理我们点击添加博客按钮时要做的事情。**

**只有当 *isPending* 设置为 false 时，我们才会显示*添加博客*按钮。否则，我们知道已经有一个博客添加待定，所以我们显示一条消息，显示*正在添加博客*。**

**在`*handleSubmit*`函数中，我们防止了不刷新页面的默认行为。然后，我们收集所有的数据，并使其成为一个对象。然后我们将`*isPending*`设置为真。然后我们调用 fetch 函数并使用 POST 方法。最后，我们在 fetch 函数中传递 blog 对象。**

**在我们完成之后，我们将`*isPending*` 设置为`false`，并将主页压入历史堆栈。添加博客后，我们将进入主页。**

## **使用提取挂钩**

**在这个组件中，我们构建了 useFetch 定制钩子，它帮助我们从本地 JSON 服务器获取数据。**

**我们将使用 React 中可用的*使用状态*和*使用效果*挂钩。要了解更多关于钩子的知识，这是一个很好的资源**

**[](https://reactjs.org/docs/hooks-overview.html) [## 钩子一瞥-反应

### 钩子是 React 16.8 的新增功能。它们允许您使用状态和其他 React 特性，而无需编写类。钩子…

reactjs.org](https://reactjs.org/docs/hooks-overview.html) 

我们将使用`*useState*` 钩子来设置三个变量:`*data*` *、* `*isPending*`、和`*error*`。我们也有一个二传手给他们三个。默认情况下，我们将`data`设置为空数组。我们保留`isPending` `true`，默认设置`error`为`null`。

因为我们使用本地 JSON 服务器，所以我们可以即时访问我们的数据。所以，我们将无法在主页上看到加载效果。因此，为了看到和体验慢速连接的用户在主页上看到的内容，我们使用了一个`setTimeout`函数，它将获取过程延迟了我们输入的时间。我们不应该在生产中使用它，因为我们希望尽可能快。

所以，在`*useEffect*` 钩子里面，我们有一个中止控制器。接下来，我们有一个超时函数，在这个函数中，当这个钩子被调用时，我们将使用从其他组件接收到的 URL 来获取数据。

在我们从服务器获得响应之后，如果响应不正常，那么我们抛出一个错误。另一方面，如果回答是好的，我们得到数据。

一旦我们得到数据，我们就在我们的`data`变量中设置数据，将`error`设置为`null`并将`isPending`设置为`false`。

然后，我们将一个`catch`函数附加到它上面，以捕捉我们在函数中抛出的任何错误。

如果错误是中止错误，这意味着我们中止了呼叫，它会记录我们中止了对控制台的呼叫。如果我们有任何其他错误，我们将其保存到错误变量，并将`isPending`设置为`false`。

我们在`useEffect`钩子中传递 URL，这意味着无论何时我们改变 URL，都会调用`useEffect`钩子并获取数据。

然后我们从这个函数中返回所有的`data`、`isPending`和`error`作为对象。** 

**这就是这部分的内容。在本系列的下一部分中，我们将通过处理所有剩余的小组件来完成 blog 应用程序，我们还将学习如何设置我们的本地 JSON 服务器，从那里获取所有数据。**

**我希望你喜欢这篇文章，我希望你对这个系列的下一部分感到兴奋，这将结束这个博客项目。**

**该系列的下一部分是:-**

**[](/build-a-blog-app-with-react-finish-the-project-3f4bc4f24ece) [## 使用 React 构建博客应用程序—完成项目

### 第 4 部分:在项目的最后部分，我们将完成所有剩余的组件，并学习如何建立一个本地…

javascript.plainenglish.io](/build-a-blog-app-with-react-finish-the-project-3f4bc4f24ece) 

写完这篇文章后还有更多文章要读:

[](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [## 使用 Django Rest 框架构建博客网站——概述(第 1 部分)

### 让我们使用 Django Rest 框架构建一个简单的博客网站，了解 DRF 和 REST APIs 如何工作，以及我们如何添加…

towardsdatascience.com](https://towardsdatascience.com/build-a-blog-website-using-django-rest-framework-overview-part-1-1f847d53753f) [](/build-a-simple-todo-app-using-next-js-f88b68761e27) [## 使用 Next.js 构建一个简单的 Todo 应用程序

### 让我们用 Next.js 构建一个简单的 Todo 应用程序，它教你 CRUD 的基本原理(创建、读取、更新和…

javascript.plainenglish.io](/build-a-simple-todo-app-using-next-js-f88b68761e27) [](https://towardsdatascience.com/build-a-simple-todo-app-using-react-a492adc9c8a4) [## 使用 React 构建一个简单的 Todo 应用程序

### 让我们用 React 构建一个简单的 Todo 应用程序，教你 CRUD 的基本原理(创建、读取、更新和…

towardsdatascience.com](https://towardsdatascience.com/build-a-simple-todo-app-using-react-a492adc9c8a4) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)**