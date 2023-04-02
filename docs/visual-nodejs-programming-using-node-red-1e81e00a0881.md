# 使用 Node-RED 进行可视化 Node.js 编程

> 原文：<https://javascript.plainenglish.io/visual-nodejs-programming-using-node-red-1e81e00a0881?source=collection_archive---------8----------------------->

![](img/0b4a738a60711d506598537605ca94c3.png)

在本文中，我将向您介绍一个 [Node.js](http://nodejs.org) 模块，它允许您通过在 web 浏览器中使用可视化的拖放式界面来创建和部署服务器端流程。我所指的模块被称为 [Node-RED](http://nodered.org) :一个基于流程的编程工具，它允许你通过将[微服务](https://microservices.io)连接在一起来设计流程(又名流)。

# 在 YouTube 上观看视频

Node-RED 创建于 2013 年，最初旨在将[物联网](https://en.wikipedia.org/wiki/Internet_of_things)可视化地连接在一起，但随着它的成熟，它演变成一种更加强大的东西，足以作为中间件部署在企业生产环境中。Node-RED 背后的强大之处在于它如何在设计界面中隐藏样板代码，允许您快速构建和部署流程和集成。

为了证明这一点，我将比较一个简单的 Node 应用程序和一个 Node-RED 流，这将向您展示可以节省的时间，以及为什么您应该对学习这项技术感到兴奋:

# 简单 Node.js Express 应用程序

下面的代码是一个简单的 [Express](https://expressjs.com) 应用程序，它输出 **Hello World** 。

## server.js

```
const Express = require('express')
const App = Express()
const HTTP = require('http')
const Cron = require('node-cron')
const Functions = require('./functions')// Create Route
App.get('/api/greet', (req, res) => {
   const result = Functions.greet()
   res.send(result)
})// Start Server
const port = 6025HTTP.createServer(App).listen(port, () => {
   console.log('NodeJS App Listening on: ', port) // Schedule CRON Job
   Cron.schedule('*/5 * * * * *', () => {
      Functions.greet()
   })
})
```

## 函数. js

```
const greet = () => {
   const result = 'Hello World'
   console.log(result)
   return result
}exports.greet = greet
```

在 **server.js** 中，我们已经为我们的 Express 服务器、一个调度流程以及一个名为 **/api/greet** 的端点准备了一些逻辑。然后我们有一个 **functions.js** 文件，它导出一个 **greet()** 函数，该函数返回文本 **Hello World** 。 **server.js** 中的 CRON 作业每 5 秒运行一次，每次运行时触发 **greet()** 函数。这个函数也由 **/api/greet** 端点触发。

因此，本练习的要点是我们将使用 3 个事件来触发 **greet()** 函数:

*   通过终端手动
*   通过网络应用编程接口
*   通过时间表

## package.json

```
{
   "name": "node-red-intro-nodejs-app",
   "version": "0.0.1",
   "description": "Node-RED Intro - NodeJS App",
   "main": "server.js",
   "scripts": {
      "manual": "node -e \"require('./functions').greet()\"",
      "endpoint": "curl http://localhost:6025/api/greet"
   },
   "engines": {
      "node": "12.18.4"
   },
   "author": "Agilit-e",
   "license": "MIT",
   "dependencies": {
      "express": "4.17.1",
      "node-cron": "3.0.0"
   }
}
```

*   我们通过在终端或命令提示符下调用 **functions.js** 并执行 **greet()** 函数来手动触发该函数。你可以看到我已经在 **package.json** 中添加了这个作为**手动**脚本，我将通过运行`npm run manual`来触发它。这将写入 **Hello World** 作为对控制台的响应。
*   对于我们的下一个测试，我们启动 Node.js 服务器并通过 HTTP 请求触发 **greet()** 函数。我们的终点将是`http://127.0.01:6025/api/greet`。因为这是一个简单的 **GET** 请求，我们可以在终端中使用 **curl** 命令，或者在浏览器窗口中打开 url。为了便于执行，我将它作为脚本放在 **package.json** 中，我将使用`npm run endpoint`来触发它。您可以看到 **Hello World** 作为响应返回。
*   最后，我们还可以看到，在后台，调度的 **CRON** 作业每 5 秒钟打印一次对控制台的响应。

现在，如果您知道自己在做什么的话，除去设置这个项目的基础所花费的时间，即 **package.json** 、依赖项和 HTTP 服务器…创建 HTTP 端点、 **greet()** 函数和 CRON 作业将花费您几分钟的时间。为了好玩，让我们看看在 Node-RED 中我们可以多快实现这一点:

**注意:**对于 Node-RED 演示，[点击此处](https://youtu.be/ZXzdzJ9ZYKQ?t=162)观看我在 YouTube 上的视频，或者观看上面的嵌入视频(快进到分钟 [2:42](https://youtu.be/ZXzdzJ9ZYKQ?t=162) )。因为我们仍然处于我的 [Node-RED 系列](https://www.youtube.com/playlist?list=PLISqeoHsXJYBriF8VE_CrDvNGURq2c2m6)的开始阶段，这更像是一篇介绍文章，所以很难用文字解释我在 Node-RED 中做了什么。对造成的任何不便表示歉意。

假设您已经观看了视频演示，我相信您喜欢 native NodeJS 和 Node-RED 的有趣比较。在 NodeJS 中需要几分钟才能完成的事情，使用 Node-RED 只需几分钟就能完成。把它扩大到一个更大的项目，你会看到大量的时间节省。

现在，这是我的[启动并运行 Node-RED](https://www.youtube.com/playlist?list=PLISqeoHsXJYBriF8VE_CrDvNGURq2c2m6) 系列的第一篇文章，还有更多文章将关注 Node-RED 的所有领域，从基本到高级功能，再到现实世界的场景。如果你还没有[订阅](https://www.youtube.com/bleedingcode)或[关注](https://medium.com/@johnjardin)我，现在将是一个很好的时机，这样当新内容发布时你会得到通知。

最后，我想为您提供一个参考资料，帮助您了解更多有关 Node-RED 的信息:

你的第一站将是 Node-RED 的网站—[nodered.org](https://nodered.org)。该网站将让您深入了解 Node-RED 是什么，它是如何工作的，并提供适当的端到端文档，介绍如何使用它实现几乎任何您想要的功能。你几乎可以找到任何你需要的关于 Node-RED 的东西，包括在线社区和论坛的链接，这些都可以在主页的底部找到。

最后，我强烈推荐你订阅 YouTube 上的 [Node-RED 频道](https://www.youtube.com/channel/UCQaB8NXBEPod7Ab8PPCLLAA)，该频道由 Node-RED 的创建者管理。它包括许多教程以及现场网络研讨会和视频流。

暂时就这样了。非常感谢您的阅读/观看，敬请期待更多精彩内容。

干杯！

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)