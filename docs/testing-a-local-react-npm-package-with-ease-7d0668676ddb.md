# 如何轻松测试本地 React NPM 包

> 原文：<https://javascript.plainenglish.io/testing-a-local-react-npm-package-with-ease-7d0668676ddb?source=collection_archive---------4----------------------->

## 关于何时需要安装本地 npm 软件包而不使用符号链接的教程

![](img/39a3c714abeb8e5421a311085cea40f5.png)

[在我之前的帖子](https://medium.com/geekculture/how-to-test-a-local-react-npm-package-still-on-development-9bed7f199164)中，我尽力解释了一个关于开发本地 npm 包的有趣细节。

你可能知道，我目前正在开发`[redux-chess](https://github.com/chesslablab/redux-chess)`，这是一个基于 Redux 的棋盘，主要用于连接 WebSocket 服务器进行棋步验证、位置评估和许多更酷的功能。

从包本身之外的宿主应用程序中测试包是一个好主意。然而，事实证明`npm install`在安装本地包时会创建一个符号链接，这可能会导致不友好的测试体验。

有关这个不太明显的主题的更多信息，请访问:

*   [npm 安装不应创建符号链接#18503](https://github.com/npm/npm/issues/18503)
*   [Nico js/node-install-local](https://github.com/nicojs/node-install-local)

顺便说一下，我用来测试`redux-chess`的主机应用程序叫做`testing-redux-chess`，可以在[的 GitHub repo](https://github.com/chesslablab/testing-redux-chess) 上下载。

今天，让我详细说明如何在测试应用程序中测试一个有前途的、令人惊奇的本地 npm 包。

在这种情况下，我们依靠`nicojs/node-install-local`来帮助我们摆脱`npm install`将在`./node_modules/redux-chess/node_modules`中自动创建的令人不安的符号链接。

于是，我全球安装了`install-local`。

```
$ npm install -g install-local
```

然后是`redux-chess`——我的 npm 包，记住，它仍在开发中——在我的测试应用程序的主文件夹中:`~/projects/testing-redux-chess`。

```
$ cd ~/projects/testing-redux-chess/
$ install-local --save ../redux-chess
```

`install-local`在`testing-redux-chess/package.json`文件中创建了`localDependencies`键，如下所述。

```
...
"localDependencies": {
    "redux-chess": "../redux-chess"
}
...
```

那时，我在`package.json`文件中写了一些方便的脚本，目的是让我的开发体验更加愉快。

```
...
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "stop": "kill -9 $(lsof -t -i:$npm_config_port)",
    "restart": "kill -9 $(lsof -t -i:$npm_config_port) && react-scripts start",
    "update:local:redux-chess": "rm -rf ./node_modules/redux-chess/dist && cp -r ../redux-chess/dist ./node_modules/redux-chess/dist"
  },
...
```

以下是有助于自动化测试过程的`scripts`:

*   `npm run stop --port=3000`
*   `npm run restart --port=3000`
*   `npm run update:local:redux-chess`

轻松测试`redux-chess`的命令序列最终看起来是这样的。

将代码传输到包的文件夹中。

```
$ npm run publish:npm
```

在测试应用程序中更新包。

```
$ npm run update:local:redux-chess
```

重启测试应用。

```
$ npm run restart --port=3000
```

这些命令可以链接在一起，构建一个运行在`~/projects/testing-redux-chess`文件夹中的命令。

```
$ npm run publish:npm --prefix /home/standard/projects/redux-chess && npm run update:local:redux-chess && npm run restart --port=3000
```

有了这个方案，我能够在浏览器上动态显示我的本地包中的更改，这有助于在进行测试时节省时间和精力。

我猜想在一个完美的世界里，你会希望在不重启 React 应用程序的情况下立即传输包的代码并观察变化，但似乎我们离它只有一步之遥。

这是目前所有的，非常感谢您的阅读。

[](https://medium.com/geekculture/how-to-test-a-local-react-npm-package-still-on-development-9bed7f199164) [## 如何测试仍在开发中的本地 React Npm 包

### 所需的设置并不太复杂，但足够有趣的是，如果没有测试计划，你可能会浪费大量的时间…

medium.com](https://medium.com/geekculture/how-to-test-a-local-react-npm-package-still-on-development-9bed7f199164) 

## 您可能还对以下内容感兴趣:

*   [一个反作用棋盘，棋盘上有几行圈圈和钩子](https://medium.com/geekculture/a-react-chessboard-with-redux-and-hooks-in-few-lines-6009cb724bb)
*   [用 Jest 最简单的方法开发 React 应用](https://programarivm.medium.com/tdding-a-react-app-with-jest-the-easy-way-8ddb64aeaba6)
*   [满心期待测试 React 组件](https://programarivm.medium.com/looking-forward-to-testing-react-components-with-joy-5bb3f86c21d7)
*   [我在 Redux Hooked 应用中的第一次集成测试](https://programarivm.medium.com/my-first-integration-test-in-a-redux-hooked-app-3b189addd46e)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)