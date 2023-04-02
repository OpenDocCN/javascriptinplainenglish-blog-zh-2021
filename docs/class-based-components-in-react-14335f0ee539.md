# React 中基于类的组件

> 原文：<https://javascript.plainenglish.io/class-based-components-in-react-14335f0ee539?source=collection_archive---------17----------------------->

![](img/4299ad78306ad437bf4b33c7bb370db9.png)

Photo by [Alex Zarco](https://www.pexels.com/@alex-zarco-1513461?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/grayscale-photography-of-high-rise-buildings-3331837/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

所以您想使用更面向对象的编程(OOP)方法来构建 React 组件？好吧，那就别再找了。

今天我们将创建一个基本的状态对象，然后在我们的 return 语句中使用状态对象的 props，我们将把它呈现给用户。在 React 中有几种不同的方式来构建组件。我个人使用最多的两个是函数式的和基于类的，我在 React 和 Vue 中都是如此。我们整个组件文件的代码如下

让我们来分析一下这里发生了什么。首先，我们在第 1 行导入 React。这使我们能够访问 react 提供的所有内容。接下来，我们将通过扩展 React.Component 来设置我们的类组件。这给了我们访问道具的权限，并且 [React 文档](https://reactjs.org/docs/components-and-props.html)推荐—

> ***类组件应该总是用道具*** 调用基础构造函数

因为 es6 类如果是子类就得调用 super。如果我们不将 props 传递给 super()和 console.log，将不会输出任何内容。但是，通过将它传入 super()并进行日志记录，我们将获得我们所期望的任何道具。

接下来，我们设置我们的状态对象。它可以包含您想要的任何内容，但是对于这个例子，我传递了一些关于我自己的信息。我们正在做的最后一件事是返回一个`<h1>`并抛出一个字符串。在正常情况下，我最有可能将它放入一个枚举中并返回该枚举，但是对于这个例子，我认为我应该保持简单。

![](img/cf7ead490b84cc06b9cc9161af5dc5fc.png)

EZPZ

虽然这是一个非常简单的例子，但是你可以用基于类的组件做很多很酷的事情。

我希望这篇文章是令人愉快的。如果你有任何反馈，发表评论，让我知道我可以改进的地方。如果你想看看我的其他帖子，可以在这里找到。我写的都是前端特有的东西，所以我有关于 [Fetch API](https://avetwhocodes.com/fetching-data-from-an-api-with-the-fetch-api-in-react-5dbe0abcfb41) 、 [React](/level-up-your-react-skills-with-the-use-of-composition-766a41f544c9) 、 [TypeScript](https://jgrice01.medium.com/typescript-understanding-the-basics-a2264759cd2d) 、[SASS](https://medium.com/codex/writing-better-sass-with-dynamic-class-generators-e486a0413d0d)&[electronic](https://jgrice01.medium.com/want-to-build-desktop-apps-using-js-say-hello-to-electron-4f862c3b4e38)的文章。感谢您的阅读，祝您愉快！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)