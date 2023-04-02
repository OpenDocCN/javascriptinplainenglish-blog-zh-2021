# TypeScript:开发环境简介

> 原文：<https://javascript.plainenglish.io/typescript-intro-to-development-environments-d632a85c5e4d?source=collection_archive---------6----------------------->

![](img/862c42dcf0f2b7822d377f2339079005.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这篇文章是我最近写的的一篇介绍 TypeScript 文章的后续。

这里的想法是展示如何从头启动一个 TypeScript 项目，并展示不同的编译和使用选项。

# 先决条件

本质上，要使用 TypeScript，只需要安装 node.js 和 npm 并运行`npm install -g typescript`来启用它。

这将为系统全局安装 TypeScript 的 CLI，但也可以作为您在计算机上启动的任何项目的本地依赖项。

安装完成后，我们现在可以访问调用编译器的`tsc`命令。每当它运行时，它将开始在执行文件夹中寻找一个`tsconfig.json`文件，并继续在所有文件系统中爬行，直到找到一个，或者它将退回到安装时附带的默认文件。

**一般来说，** `**tsconfig.json**` **所在的文件夹被认为是项目的根文件夹，所以总是把它放在实际项目的根中。**

如果你想依赖编译器的默认设置，但是保持一个合适的目录结构，你可以在`tsconfig.json`里面创建一个空的对象并保持一切整洁，就像这样:

```
{}
```

虽然这不是推荐的方式。

该文件如下所示，带有基本配置选项:

现在有很多方法可以编译你的项目，最适合你的方法取决于你正在做的项目和你对编译器本身的控制。

以下是最常见的几种:

# 1.CLI

作为微软提供的官方方式，CLI 随安装一起提供，它提供了一种非常简单的方式来直接在您的终端中运行编译，具有以下选项:

```
# straightforward running through the filesystem, looking for tsconfig.json
tsc# display all configuration options
tsc --all# Emit JS for just the index.ts with the compiler defaultstsc index.ts# Emit JS for any .ts files in the folder src, with the default settingstsc src/*.ts
```

官方[网站](https://www.typescriptlang.org/docs/handbook/compiler-options.html)提供了关于 CLI 的完整文档。

# **2。任务执行人**

像[咕噜](https://gruntjs.com/)或[大口](https://gulpjs.com/)这样的任务运行者在运行你不想浪费时间的平凡、重复的任务时非常有效。我个人经常使用 Gulp，我有一个非常简单的模板，可以在我认为准备好的时候帮助我编译代码，它看起来像这样:

在运行默认的`gulp`命令时，gulp 将通读位于项目根目录下的`tsconfig.json`文件，除了编译之外还为其创建 sourcemaps，并将报告编译的结果，提出在整个过程中可能出现的任何错误。

我写了一篇关于如何设置的详细文章:

[](https://medium.com/@dzhurovivan/typescript-environment-with-webpack-compilation-and-automatic-reload-b4d6d5a60f6f) [## 具有 webpack 编译和自动重新加载的 TypeScript 环境

### 通过这篇文章，我将提供一个非常详细的解释，告诉你如何轻松地建立一个本地开发…

medium.com](https://medium.com/@dzhurovivan/typescript-environment-with-webpack-compilation-and-automatic-reload-b4d6d5a60f6f) 

我还将它上传到了一个 starter 项目中，该项目已经配置了 TypeScript、eslint 和更漂亮的代码样式:

[](https://github.com/idzhurov/ts-starter) [## GitHub-idzhurov/ts-启动器

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/idzhurov/ts-starter) 

# **3。捆扎机**

随着应用程序的增长，复杂性也在增长，这使得简单的编译变得更加困难。这就是捆扎机的用武之地。我们有 [rollup](https://rollupjs.org/guide/en/) 、 [webpack](https://webpack.js.org/) 和 [browserify](https://browserify.org/) ，它们已经存在了一段时间，最近还有 [vite](https://vitejs.dev/) 等等。

除了编译之外，它们还有其他好处，如最大限度地减少代码、html 和 css，将静态资产复制到生产文件夹，使用任务运行器，它们可以实现相当自动化的构建管道，因此 bundler 是从头开始建立大型项目的一个很好的选择。

例如，我已经创建了一个使用 webpack 5 的存储库，使用 HTMLWebpackPlugin 创建一个 index.html 文件，并自动将捆绑的代码添加到 html 文件中:

[](https://github.com/idzhurov/webpack-ts-starter) [## GitHub-idzhurov/web pack-ts-starter

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/idzhurov/webpack-ts-starter) 

# **4。框架**

一个重要的免责声明是，当我们只在我们工作的项目中使用 TypeScript，而不使用 React、Vue 或 Svelte 等现代框架时，通常会使用上述所有选项。Angular 是不可能的，因为它默认使用 TypeScript，你没有任何办法绕过它。

React 和 Vue 甚至在它们的 CLI 中包含了一个选项，所以默认情况下会添加 TypeScript，并带有推荐的编译选项，可以根据您的特定需求进行扩展。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***