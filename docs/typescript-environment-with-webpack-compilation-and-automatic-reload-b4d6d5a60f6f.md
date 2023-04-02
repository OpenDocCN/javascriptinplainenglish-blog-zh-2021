# 具有 Webpack 编译和自动重新加载的 TypeScript 环境

> 原文：<https://javascript.plainenglish.io/typescript-environment-with-webpack-compilation-and-automatic-reload-b4d6d5a60f6f?source=collection_archive---------5----------------------->

![](img/3fc8eb675f7b6b8dc049db453234027f.png)

在这篇文章中，我将提供一个非常详细的解释，说明如何轻松地建立一个本地开发环境来编译 TypeScript 和捆绑您的代码，以便在不使用框架的情况下进行生产。干净简单。

这篇文章将会被尽可能详细地解释，所以一个完全的初学者不应该去别处寻找答案。

# 使用

有人可能会问为什么不采用 React、Vue.js 或 Angular 之类的现代框架，答案很简单——你不想要或不需要它们，或者你只是想探索这些框架是如何在非常低的水平上用编译架构启动的。

我通常为互联网创建游戏(我将在另一个教程中展示)，但这里的想法是，如果你不需要，或者特别是如果你有大小限制，你可能不想依赖于框架，所以这是简单明了的重点和实际的语言和构建过程。

# 设置

你需要启动的是 Node.js 或者 npm，当然也可以是任何其他的包管理器。

起点是您的终端:

```
# create a folder
mkdir webpack-ts-starter# navigate to folder
cd webpack-ts-starter# initialize node.js project, skipping npm's interactive tutorial
npm init -y
```

现在您已经有了一个 node.js 项目，您可以使用它轻松地安装项目的依赖项，并在`package.json`文件中跟踪它们。

# 。gitignore

我总是建议尽早添加一个`.gitignore`文件。我是这样创建我的:

```
# create the file through the terminal
touch .gitignore
```

和它的实际内容:

```
# mac os finder hidden file
.DS_Store# the installed npm packages
node_modules# compilation folder if we decide to deploy our package as a library
lib# main project compilation folder
dist# hidden folder that contains local history from the Local History 
# extension
.history
```

这个文件确保所有那些不必要的文件不会上传到 git，所以我们的库将保持干净，只有源文件。

# 属国

先说最主要的，写这篇文章的原因— TypeScript。

`npm install --save-dev typescript`

上面的命令为我们提供了正式的 TypeScript 包和对`tsc`命令的访问，以便手动编译代码。这通常需要一个`tsconfig.json`文件，放在项目的根目录下，否则，TypeScript 将遍历父文件夹，直到找到一个为止，或者它将退回到缺省值，这也不错，但不是完全为我们的特定需求配置的。

因此，创建一个`tsconfig.json`文件并用以下内容填充它:

您已经准备好使用 TypeScript 了。创建这个文件后，你可以在同一个文件夹中运行`tsc`命令，它将编译在`src`下找到的所有内容，并将其导出到`lib`文件夹。

**自动化**

这基本上就是你所需要的，但是随着项目变得越来越大，仅仅使用`tsc`命令是不够的。编译有很多选择，但我个人使用 webpack，下面是你也可以使用的方法:

```
npm install --save-dev webpack webpack-cli
```

这将把 webpack 及其 CLI 添加到项目的开发依赖项中。对于那些不知道的人来说，开发依赖是指那些包，它们只在开发时需要，例如构建管道、链接各种任务运行程序等等，在最终构建的项目中通常不需要。

与`tsconfig.json`类似，webpack 需要一个配置文件来完成编译。在项目的根目录下创建一个`webpack.config.js`文件，并像这样填充它:

在继续之前，让我们再安装几个依赖项:

```
npm install --save-dev ts-loader html-webpack-plugin
```

`ts-loader`实际上是为 webpack 加载 TypeScript 文件，而`html-webpack-plugin`是一个包，它将为构建文件夹创建一个 index.html 文件，并将自动包含编译后的代码作为其源代码。

这是一个非常简单的 webpack 配置，它将从位于`src`文件夹中的 index.ts 文件开始，并将编译和捆绑连接到它的每个文件，跳过未使用的文件(通常称为树抖动)。

在这个阶段，您已经可以访问将编译和捆绑代码的`webpack`命令。我所做的是将它添加到`package.json`中，在`scripts`下，就像这样:

```
"scripts": { "build": "webpack"
}
```

那么运行`npm run build`就会帮你做到。

# 下一关

因此，每次需要更改代码库时运行这个命令可能会有点乏味，所以 webpack 也有一个开发服务器来代替我们进行监视和编译，甚至不要求我们在任何可能的时候重新加载应用程序。这一概念被称为[热模块更换](https://webpack.js.org/guides/hot-module-replacement/)，设置方法如下:

```
npm install --save-dev webpack-dev-server# within package.json, add the script
"serve": "webpack serve"# webpack.config.js
devServer: {
  static: "./dist",
  hot: true
}
```

然后运行`npm run serve`将启动一个本地服务器，并在每次代码更改时自动编译和重新加载。

就是这样，现在你有了一个非常简单的开发环境，可以编译 TypeScript 并使用 HMR。整个项目上传到这里:

[](https://github.com/idzhurov/webpack-ts-starter) [## GitHub-idzhurov/web pack-ts-starter

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/idzhurov/webpack-ts-starter) 

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。*****