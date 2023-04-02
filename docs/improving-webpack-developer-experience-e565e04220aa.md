# 改善 Webpack 开发人员体验

> 原文：<https://javascript.plainenglish.io/improving-webpack-developer-experience-e565e04220aa?source=collection_archive---------11----------------------->

## 使用 Create React App 的 React 开发工具

![](img/81d94bedb9a7fbd8dd73386e5e75dbb8.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我的旅程

我用自己的 Webpack 配置已经很久了。但是对于快速的演示项目，比如那些中型文章，使用定制的构建系统是没有意义的。于是我又开始用 Create React App。我已经忘记很久的所有难以置信的开发人员体验又回来了——比如如果我想要的端口正在使用，允许我使用不同的端口，使用现有的浏览器标签而不是打开新的标签，以及使用新安装的依赖项自动重建。所有这些好的特性让我思考——我能不能在不使用 Create React 应用程序的情况下拥有同样的功能？

# React 开发工具

[React Dev Utils](https://www.npmjs.com/package/react-dev-utils) 是 Create React App 的构建工具库。因为这是一个单独的专用包，所以即使您没有使用 Create React App，也可以使用它们！要安装，运行`npm install --save-dev react-dev-utils`。现在，让我们深入其中一些工具，看看它们如何让你的生活变得更加轻松。

# 选择端口

您是否遇到过您想要的端口被占用的情况？如果您在同一个开发端口上运行多个项目，这个问题会经常出现。你会收到这条信息

```
Error: listen EADDRINUSE: address already in use 127.0.0.1:3000
```

Webpack Dev 服务器将无法启动。要解决这个问题，您必须找到并终止使用您的端口的另一个进程，或者使用不同的端口重新启动 Webpack Dev Server。

React Dev Utils 提供了`WebpackDevServerUtils.choosePort`实用程序来自动检测所需的端口是否正在使用，并选择另一个端口。

```
const { choosePort } = require('react-dev-utils/WebpackDevServerUtils');const desiredPort = parseInt(process.env.PORT, 10) || 3000;const config = async () => {
  const port = await choosePort(host, desiredPort);
  if (!port) {
    process.exit();
  } // Webpack configuration
  return {
    ...
    devServer: {
      port,
    },
  };
};module.exports = config;
```

不要使用对象配置，而是将 Webpack 配置导出为异步函数。如果所需的端口正在使用中，`choosePort`将阻塞并等待用户输入。

```
Something is already running on port 3000.
Would you like to run the app on another port instead?
```

如果用户键入`y`(表示是)，那么实用程序将自动找到下一个可用端口。如果用户键入`n`(代表否)，那么实用程序将返回`null`，过程将退出。现在，您可以优雅地解决端口冲突问题。

# `Open Browser`

在启动 Webpack Dev 服务器之后，您很可能需要打开浏览器到指定的开发 URL。为了自动做到这一点，Webpack Dev 服务器提供了一个`open`标志。但它以一种愚蠢的方式做到了这一点——它总是用指定的主机和端口打开一个新的浏览器选项卡，忽略任何具有相同 URL 的现有浏览器选项卡。这会导致过多的浏览器标签打开到同一个页面，这也有降低多个热重新加载标签的性能的副作用。

对于 Mac 上的 Chrome 用户，React Dev Util 的`openBrowser`实用程序可以智能地使用现有的浏览器标签。

```
const openBrowser = require('react-dev-utils/openBrowser');const host = process.env.HOST || 'localhost';
const port = parseInt(process.env.PORT, 10) || 3000;module.exports = {
  ...
  devServer: {
    onListening: () => {
      openBrowser(`[http://${host}:${port}`](/${host}:${port}`));
    },
    port,
    host,
  },
};
```

利用 Webpack Dev 服务器开始监听指定主机端口上的连接后调用的`onListening`钩子，我们可以调用`openBrowser`实用程序。如果这个 URL 有 Chrome 标签，它会智能地切换到那个标签。如果没有，它会像`open`标志一样打开一个新标签。现在，你将不再有重复和不必要的浏览器标签。

# `WatchMissingNodeModulesPlugin`

Webpack Dev Server 的热重装在检测到代码和依赖关系变化时会自动重建，但也有检测失败的情况。使用未安装的软件包就是其中之一。在这种情况下，Webpack Dev Server 将无法像预期的那样编译，但是在软件包安装后，它仍然无法恢复。要解决这个问题，您需要重新启动 Webpack Dev 服务器。React Dev Util 的`WatchMissingNodeModulesPlugin`解决了这个问题。

```
const WatchMissingNodeModulesPlugin = require('react-dev-utils/WatchMissingNodeModulesPlugin');module.exports = {
  ...
  plugins: [
    new WatchMissingNodeModulesPlugin(path.resolve('node_modules')),
  ],
};
```

`WatchMissingNodeModulesPlugin`将检测缺失的依赖项并观察`node_modules`。如果它们出现，插件将自动触发重建。现在，您将不再需要在使用尚未安装的包后重启 Webpack Dev 服务器。

# 最后的想法

即使您使用自己的 Webpack 配置，Create React App 的构建工具仍然可以改善您的开发人员体验。它提供了工具来解决诸如端口冲突、不必要的浏览器标签和丢失包重建失败等不便。

# 资源

*   [官方 Webpack 文档](https://webpack.js.org/)
*   [官方 Webpack 开发服务器文档](https://webpack.js.org/configuration/dev-server/)
*   [官方反应开发文档](https://www.npmjs.com/package/react-dev-utils)