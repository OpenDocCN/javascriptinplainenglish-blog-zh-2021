# Node.js 应用程序的 10 个最佳实践

> 原文：<https://javascript.plainenglish.io/10-best-practices-for-node-js-apps-5c8d1ee33a02?source=collection_archive---------4----------------------->

## 基于我自己经验的 Node.js 最佳实践

![](img/8db8e9d89b63aa3394c1b0a2cf737ed7.png)

Credit: [https://en.wikipedia.org/wiki/Node.js](https://en.wikipedia.org/wiki/Node.js)

在本文中，我总结了 Node.js 应用程序的 10 个技巧。这篇文章是基于我自己的经验，并不声称是完整的。

# 1.安装 npm 模块(正确)

在某些项目中，必须始终安装某个版本的 npm 模块。然而，通常 npm 模块只是用命令`npm install ... --save`而不是`npm install ... --save --save-exact`安装。

命令`npm install ... --save`导致 npm 模块...在 package.json 前接收一个版本号`^`。如果其他人为项目安装了这个 npm 模块，他可能会收到一个与最初安装的版本不同的版本。

然而，`npm install ... --save --save-exact`命令会将 package.json 中的版本设置为当前版本。

# 2.应用程序监控非常重要

Node.js 应用程序在服务器上作为单独的进程运行。例如，如果这个过程由于编程错误而崩溃，你应该是第一个知道的人，而不是你的访问者。

Node.js 应用程序有许多监控工具，可以确保在出现错误时，通过电子邮件或其他方式发送相应的消息。在这里，每个人都必须找到他们应用所需的监控软件。对于 Node.js 应用程序，我更喜欢 monit，因为它已经包含在大多数服务器中。然而，与 monit 提供的工具相比，其他工具提供了更广泛的监控选项。

# 3.始终使用 Node.js 的最新 LTS 版本

我总是建议使用 Node.js 的最新 LTS(长期支持)版本，一方面是为了获得稳定性，另一方面是为了不失去最新的特性。在撰写本文时，当前版本是 node . js 15 . 11 . 0。

# 4.总是使用 npm init 启动新的 Node.js 项目

`npm init`命令在当前目录下创建一个有效的空 package.json 文件。package.json 文件对每个项目都很重要，因为 npm 模块及其版本就存储在这里。

如果你使用不同的 Node.js 版本，想在它们之间来回切换，我推荐使用 [nvm](https://github.com/creationix/nvm) (节点版本管理器)。

# 5.总是用小写字母写文件名

不要创建这样的文件名:“MyFile.js”原因很简单。Node.js 可用于各种平台(Windows、OSX、Linux)。例如，命令`var MyFile = require('MyFile');`可以在 Windows 开发系统上工作，但是在 Linux 生产服务器上会导致“找不到文件”。原因是有些操作系统，比如 Windows，不区分“MyFile.js”和“myfile.js”。然而，其他操作系统，如 Linux，却可以。

因此，Node.js 项目中文件名的连字符符号被证明是实用的。对于上面的例子，这应该是“my-file.js”。

# 6.不要通过 Node.js 传递静态文件。

静态文件，如图像或类似文件，不应通过 Node.js，而应通过 web 服务器交付。理想情况下，Node.js 应用程序不直接在端口 80 上运行，而是通过不同的端口和 web 服务器(我推荐 Nginx)将请求转发给 Node.js 进程。

因为 web 服务器可以比 Node.js 应用程序更有效地交付静态文件，所以静态文件应该直接通过 web 服务器在单独的目录中交付。这意味着 Node.js 应用程序有更多的资源可用于处理动态请求。

# 7.避免同步功能

例如，Node.js 总是为文件操作提供同步和异步版本的命令。例如，当用命令`fs.readFileSync(path[, options])`读取一个文件时，会阻塞整个进程，直到文件被完全读取，`fs.readFile(path[, options], callback)`程序继续执行该命令。一旦文件被读取，回调函数就会被调用。在大量使用的应用程序中，许多同步函数调用会降低性能。因此，应该避免使用同步函数调用。

因为 Node.js 是单线程的，所以建议使用异步函数，比如读取文件或数据库。特殊的 npm 模块可以控制最终的回调层次结构。

# 8.正确设置 NODE_ENV 变量

这个`NODE_ENV`是一个环境变量，由于 Express 框架，它变得特别流行。NODE_ENV 变量定义 Node.js / Express 应用程序运行的环境(开发或生产)。

例如，该变量可以由`export NODE_ENV=production`在 Linux & OSX 下设置，或者由`set NODE_ENV=production`在 Windows 下设置。通过将环境变量设置为 production，Express 会被提示将视图模板保存在内存中，而不是从硬盘中重新加载它们并生成不太详细的错误消息。因此，express 应用程序被调整为具有更高的应用程序性能。

# 9.删除 console.log 语句

Node.js 应用程序中的每一点都可以生成输出`console.log();`。这对于开发系统来说是一个优势，因为开发人员可以在代码的不同点查看单个对象的状态。

但是，如果这些 console.log 语句被遗忘并进入生产系统，它们会消耗大量不必要的 CPU 时间并浪费宝贵的资源，尤其是在输出很大的情况下。console.log 命令还会阻塞整个进程，因为它是同步执行的。因此，在生产系统中使用之前，应该删除所有 console.log 指令，例如 Gulp 或类似指令。

# 10.通过自动测试检查代码

最后，Node.js 应用程序的客户端 JavaScript 代码应该始终受到测试的保护。Node.js 有大量不同的测试框架。

# 结论

我希望这些简单的技巧可以帮助您实现 Node.js 的最佳实践。

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)