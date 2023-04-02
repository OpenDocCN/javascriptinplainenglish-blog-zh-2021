# Next.js 入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-nextjs-6ce019e35a77?source=collection_archive---------17----------------------->

## *“React 生产框架”*

![](img/e1886242366e69dd94f78afa15e27b23.png)

Photo by [Fatos Bytyqi](https://unsplash.com/@fatosi?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/programming?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Next.js 正慢慢成为开发服务器渲染网页的领先库。它最近获得了在 GatsbyJS 中脱颖而出的功能，并且它还可以提供更多的功能。Next.js 有一个很棒的社区，提供了很好的开发者体验。一个最小的 Next 项目也很容易制作，不需要很多技巧。

接下来是基于反应的。这是大多数开发人员目前都很熟悉的东西，在本文中我不会重点介绍 React 的教学。Next.js 项目很容易部署在自己的平台上:Vercel。查看 Next.js 的[官方网站](https://nextjs.org/)了解更多信息。

# 装置

建立 Next.js 项目有两种主要方法。可以使用`create-next-app`，也可以手动安装所有包。我本人是一个使用 NPM 安装所有东西的粉丝，所以我的代码尽可能少，所以我们会这样做。

```
npm init
npm i next react react-dom
```

我们首先在一个新文件夹中初始化 NPM，并安装所有必要的包，开始开发 Next.js 项目。我们需要反应，反应，然后。

安装之后，我们需要更新`package.json`脚本来启动 Next.js 服务器。

```
"scripts": {  
  "dev": "next dev",
  "build": "next build",
  "start": "next start"
}
```

我们将只使用`npm run dev`来启动一个本地开发服务器。`Build`用于部署。

下一步是创建一个`pages`文件夹，我们将在其中放置我们的 React 页面。`index.js`填充被首页。

这是一个在 Next.js 中有效的最小页面。当您运行命令启动服务器时，您可以浏览到`localhost:3000`,将会看到我们刚刚创建的页面。

# 更多页面

一个网站几乎总是由多个页面组成。您可以使用 URL 或链接浏览的页面。在 Next.js 中创建新页面就像创建第一个页面一样简单。用 URL 创建一个合适的结构也很容易。

在`pages`文件夹中，您可以创建子目录或其他 JavaScript 文件。文件夹和文件的名称将直接反映 URL。

一个 JavaScript 页面`pages/admin/dashboard.js`会自动获取 URL `localhost:3000/admin/dashboard`。就像魔法一样！

让我们在`pages`文件夹中创建一个关于页面。包含与我们主页相同的语法。之后，我们将需要添加一个链接到我们的主页，这样我们就可以浏览到关于页面。

它几乎和普通的 HTML 一样简单。我们使用一个带有锚标记的链接组件作为子组件，以符合 SEO 和 HTML 惯例。

# 静态文件和头文件

我们可能想在所有页面中添加 Javascript 文件或样式表，而在每一页中添加这些会很麻烦，所以我们可以使用`_app.js`文件，您需要将该文件添加到`pages`文件夹中。最小的`_app.js`页面如下所示。

您可以在这个组件中添加您的头像和其他全局 HTML。

图像等静态文件应保存在项目根目录下的`public`文件夹中。在这个文件夹中，你可以添加脚本，样式表，图标，甚至配置文件，比如`robots.txt`。

# 结论

Next.js 是一个很好的快速创建 web 应用程序的库。尤其是与 TailwindCSS 搭配使用时，可以快速进行造型。您还可以在[官方文件](https://nextjs.org/docs/getting-started)中了解更多信息。Next.js 将会继续存在，所以学习它不会毫无价值。

谢谢你的阅读，祝你愉快。