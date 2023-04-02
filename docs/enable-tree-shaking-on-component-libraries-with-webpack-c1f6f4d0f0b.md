# 启用树抖动以使用 Webpack 优化 React 组件库

> 原文：<https://javascript.plainenglish.io/enable-tree-shaking-on-component-libraries-with-webpack-c1f6f4d0f0b?source=collection_archive---------8----------------------->

![](img/491696c0f0b2b98b521fdac455331783.png)

用 React 构建组件库的一个重要部分是确保它们是轻量级的和优化的。

例如，我在应用程序中经常使用 Lodash。我只使用了 Lodash 提供的一小部分功能。当我将我的应用程序捆绑到产品版本中时，我不希望整个 1.14 Mb 的库被拉进来。

树抖动，或“死代码移除”，是一种允许您从库中移除任何未使用的代码的技术。

为了使摇树工作，一些事情需要到位。

1.  目标库需要用 ES5 或更高的语法编写。
2.  目标库需要将它的 package.json 的 sideEffects 设置为 false。
3.  你需要使用支持它的 JavaScript bundler，在我的例子中，是 Webpack。

在本文的其余部分，我将通过一个例子来说明我是如何在为 Monorepo 构建的组件库上实现树抖动的。

我的 Monorepo 有一个叫 components 的包。我所有的定制组件都保存在这里。

我有一个用 ES6 语法编写的过于简单的按钮组件。

我的组件库有自己的 package.json，sideEffects 设置为 false。

将 sideEffects 设置为 false 实质上是我们允许 Webpack 在我们的模块上执行代码分割。

导入我的按钮的应用程序使用 Webpack 进行捆绑。

当我捆绑我的应用程序时，Webpack 会负责删除未使用的代码。

如果我选择不将我的按钮组件导入我的主应用程序，编译我的应用程序并搜索 bundle.js 文件，我将看不到任何对按钮组件的引用。

*更多内容看*[***plain English . io***](http://plainenglish.io/)