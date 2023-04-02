# React 快速刷新—新的 React 热重装器

> 原文：<https://javascript.plainenglish.io/react-fast-refresh-the-new-react-hot-reloader-652c6645548c?source=collection_archive---------0----------------------->

## 使用 React 快速刷新的全面指南

![](img/c814797e0ba805dfaa9f8aabd600c61a.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我的旅程

在为一篇中型文章构建基于 Create React 应用程序的演示时，我注意到一些意想不到的事情——当我编辑源代码时，我的应用程序会更新，但我的状态会保持不变。我期待着我的状态被重置，就像我在其他项目中工作过无数次一样。我很困惑，认为我的应用程序实际上没有正确热重装。但是随着我的深入研究，我发现这是一个令人兴奋的新特性。

# 快速刷新反应

我体验的这一新功能是反应快速刷新。它是 React 热重装的最新迭代。编辑 React 组件时，React 快速刷新将有效地只更新和重新渲染该组件。这导致热重装时间明显加快。此外，React 快速刷新将在重新渲染期间保留组件状态，因此您无需再次手动创建相同的场景。这些“快速”和无痛的重新渲染创造了卓越的开发人员体验，使变化和结果之间的反馈循环明显更有效。

# 创建 React 应用

从 4.x 开始，Create React App 默认启用 React 快速刷新。如果您的项目是基于 Create React App 构建的，您需要做的就是升级。

# 自定义网络包

如果您的项目使用自定义 Webpack 配置而不是 Create React App，启用 React 快速刷新仍然非常简单。首先，安装`react-refresh`和`[@pmmmwh/react-refresh-webpack-plu](http://twitter.com/pmmmwh/react-refresh-webpack-plu)gin`库。`react-refresh`包含支持 React Fast Refresh 的热重装所需的基本工具，`react-refresh-webpack-plugin`是启用`react-refresh`所需的 Webpack 插件。

然后，将`react-refresh/babel` Babel 插件添加到 Babel 配置文件中

```
// babel.config.jsmodule.exports = function babel(api) {
  const BABEL_ENV = api.env();
  const presets = [...];
  const plugins = [...];
  if (BABEL_ENV === 'development') {
    plugins.push('react-refresh/babel');
  }
  return {
    presets,
    plugins,
  };
};
```

并将`react-refresh-webpack-plugin`插件添加到 Webpack 配置文件中。

```
// webpack.config.jsconst ReactRefreshWebpackPlugin = require('[@pmmmwh/react-refresh-webpack-plu](http://twitter.com/pmmmwh/react-refresh-webpack-plu)gin');module.exports = {
  ...
  plugins: [
    new ReactRefreshWebpackPlugin(),
  ],
};
```

或者，您可以直接在 Webpack 配置中指定 babel 插件，而不是 Babel 配置文件。

```
// webpack.config.jsconst ReactRefreshWebpackPlugin = require('[@pmmmwh/react-refresh-webpack-plu](http://twitter.com/pmmmwh/react-refresh-webpack-plu)gin');module.exports = {
  ...
  plugins: [
    new ReactRefreshWebpackPlugin(),
  ],
  module: {
    rules: [
      {
        test: /\.[jt]sx?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        options: {
          plugins: ['react-refresh/babel'],
        },
      },
    ],
  },
};
```

就是这样，现在您应该拥有 React 为您的项目提供的最新、最棒的热重装程序了！

# 使残废

状态的保存是很好的，但是有时候你可能不想保存状态。React 快速刷新用`// @refresh reset`注释支持这一点。如果一个组件被编辑，并且这个注释存在于文件中的某个地方，那么 React 快速刷新将强制重新装载该组件，这将重置该组件的状态。

如果你发现自己不断地添加这个评论或者面对下面讨论的[的一些限制，你可能想要采取激烈的方法，不要使用 React Fast Refresh all。Create React App 提供了`FAST_REFRESH`标志来禁用它，并使用旧的热重装程序。这可以通过运行`FAST_REFRESH=false npm start`或将`FAST_REFRESH=false`添加到`.env`文件中来完成。如果您正在使用自己的定制 Webpack，只需删除上面](#d493)提到的[中的配置更改。](#a961)

# 限制

不幸的是，React 快速刷新确实有一些限制。如果 React 快速刷新不能确定更新哪些 React 组件，它将做安全的事情，并回退到进行完全重新加载。如果使用未命名/匿名和非 PascalCased React 组件，就会出现这种情况，因为 React 快速刷新无法静态确定代码是否与 React 相关。

如果您编辑最终导致 root 的文件，即使文件中的某些代码与 React 相关，也会发生完全重新加载。React 快速刷新不能保证与 React 无关的内容可以热重新加载，因此它认为不能。

此外，React Fast Refresh 的状态保持对类组件不起作用——它只对函数组件和钩子起作用。以前的热重载迭代对类组件有效，但是以一种不安全的方式，可能导致不正确的意外行为。React 快速刷新侧重于安全，所以它目前不支持类组件。

# 预发行

在撰写本文时，`react-refresh`和`[@pmmmwh/react-refresh-webpack-plu](http://twitter.com/pmmmwh/react-refresh-webpack-plu)gin` 都是 v1 之前的版本，所以可能会有问题。话虽如此，脸书团队对这些库有足够的信心，在 Create React App 4.x 中默认启用它。对我来说，仅此一点就足以开始在我的项目中使用它。

# 最后的想法

了解了 React Fast Refresh 之后，我将它集成到了我所有的项目中。通过仅在必要时智能热重装和维护应用程序状态，它使开发效率大大提高。现在，我可以更快地在 UI 中反映我的更改，并且它会自动处于与以前相同的状态。虽然有一些限制，但我没有遇到任何根本性的问题，更糟糕的是，它的行为与上一代热重装程序完全一样。React 快速刷新绝对是现有 React 热重装的优秀继承者。

# 资源

*   [官方反应刷新文档](https://www.npmjs.com/package/react-refresh)
*   [官方 React 刷新 Webpack 插件文档](https://www.npmjs.com/package/@pmmmwh/react-refresh-webpack-plugin/v/latest)

## 进一步阅读

[](/5-tips-to-scale-up-your-react-apps-8fb68319062e) [## 扩展 React 应用的 5 个技巧

### 1.将 Bit 用于可组合设计 2。设计令牌 3。网络请求的定制钩子 4。客户端与服务器状态 5。一个…

javascript.plainenglish.io](/5-tips-to-scale-up-your-react-apps-8fb68319062e) 

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*