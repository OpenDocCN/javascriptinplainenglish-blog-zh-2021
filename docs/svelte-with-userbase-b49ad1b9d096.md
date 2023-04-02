# 与用户群一起使用 Svelte 的好处

> 原文：<https://javascript.plainenglish.io/svelte-with-userbase-b49ad1b9d096?source=collection_archive---------15----------------------->

所有堆栈中最简单的？

![](img/0deb508336463f373495153511069b4b.png)

**简介**

在第一次学习 React 后，我想学习另一个受欢迎的框架来添加到我的简历中，在观看 JavaScript 世界大会后，我决定学习[苗条](https://svelte.dev/)。

在用它工作了大约一个星期后，我必须说它真的很棒。作为一个无框架的框架，或前端编译器，Svelte 比 React 更轻量级，更容易学习。它也有很好的[文档](https://svelte.dev/examples)，并且提供了非常易读的语法，让你可以轻而易举地进入其中。

为了延续简单的主题，我选择尝试构建一个无需构建后端的应用程序。Userbase 提供了一个非常简单的方法来为你的网站添加用户认证，我将向你展示如何做:

**用户群设置**

我们要做的第一件事是创建一个用户基础帐户。一个免费帐户允许你拥有一个拥有 100 名用户的应用程序，这对我来说很好，但你也可以购买一个 90 美元/年的生产计划，该计划提供无限的应用程序和用户以及 [stripe](https://stripe.com/) 集成。创建您的帐户后，只需转到“应用程序”选项卡，创建您的第一个应用程序，并复制应用程序 id。

**纤薄设置**

接下来，我们希望从 Svelte 模板创建一个应用程序，为此，您需要输入以下命令:

```
npx degit sveltejs/template your-app-name
cd your-app-name
npm install
npm run dev // The default port will be 5000
```

在你最喜欢的代码编辑器中打开应用程序，前往 index.html(在公共文件夹中)，添加用户库 [sdk](http://<script type="text/javascript" src="https://sdk.userbase.com/2/userbase.js"></script>) 。如果愿意的话，你也可以把它作为一个[包](https://www.npmjs.com/package/userbase-js)来安装。之后，前往 App.svelte，本教程的其余部分将在那里进行。

**结论**

通常，实现用户认证是一件困难的事情，但是 Userbase 使它变得非常容易。使用 Userbase 和 Svelte 可以显著减少你开始关注应用程序有趣部分所需的时间。感谢阅读！

*更多内容请看*[*plain English . io*](http://plainenglish.io/)