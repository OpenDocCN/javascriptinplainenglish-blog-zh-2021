# 如何用 http2 和 Express 制作一个“Hello World”应用程序

> 原文：<https://javascript.plainenglish.io/serving-hello-world-with-http2-and-express-js-4dd0ffe76860?source=collection_archive---------1----------------------->

通过使用[**http 2-Express-bridge**](https://www.npmjs.com/package/http2-express-bridge)**包装器**，最终可以让 Express 与 Node.js' http2 一起工作。****

**![](img/e99ac89051f8976326442275b2d99fb9.png)**

**Photo by [Nubelson Fernandes](https://unsplash.com/@nubelsondev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)**

**几个月前，在万维网上搜索时，我偶然发现了术语 **HTTP/2** 。作为一名好奇的 web 开发人员，我从来没有听说过这个术语——我觉得我应该知道——我很快暂停了对我试图解决的 bug 修复的搜索，并决定进入这个兔子洞。**

**对于外行来说， **HTTP/2** 是对 **HTTP/1.1** 协议的一个重大修订。 **HTTP/2** 规范于 2015 年夏天首次发布。从那以后，大多数主流浏览器都实现了它。 **HTTP/2** 比它的前身有很多主要的优势，无论是请求/响应复用、头压缩、服务器推送等等。甚至有 **HTTP/3** 的草案正在测试中。你可以在这里阅读更多关于**的内容 HTTP/2** [。](https://developers.google.com/web/fundamentals/performance/http2)**

**在感到兴奋的同时，也为没有早点发现而感到沮丧，我决定尝试一下。作为一名 JavaScript 开发人员，我决定用 Express 在 Node.js 中创建一个服务器实例。在搜索了 StackOverflow 之后，这是我整理的代码。**

```
const express = require('express')
const http2 = require('http2')
const { readFileSync } = require('fs')const app = express()

app.get('/express', (req, res) => {
  res.send('Hello World');
})const options = {
  key: readFileSync('<Certificate Key>'),
  cert: readFileSync('<Certificate file>'),
  allowHTTP1: true
}const server = http2.createSecureServer(options, app)
server.listen(3000)
```

**需要一个安全的服务器，因为没有 TLS 加密，没有浏览器支持 **HTTP/2** 。**

**上面的代码看起来很合理，我完全相信代码会工作。但是，当您尝试访问该路径时，迎接您的是:**

```
_http_incoming.js:113
  if (this.socket.readable)
                  ^TypeError: Cannot read property 'readable' of undefined
    at IncomingMessage._read (_http_incoming.js:113:19)
    at IncomingMessage.Readable.read (internal/streams/readable.js:481:10)
    at resume_ (internal/streams/readable.js:968:12)
    at processTicksAndRejections (internal/process/task_queues.js:80:21)
[nodemon] app crashed - waiting for file changes before starting...
```

## **为什么会这样？**

**在内部，Express 有一个核心中间件，在每个请求期间都会被调用。这个中间件用定制的请求/响应对象类型替换从服务器接收的请求/响应对象类型。默认情况下，自定义请求/响应对象继承自`http` 模块。从`http2` 模块得知与服务器不兼容。**

**要解决这个问题，必须改变中间件，以确保适当的请求/响应对象类型被路由到适当的模块。**

**Express 已经为这个修复工作了很长时间，但是 ETA 仍然没有明确的定义。同时，我以 npm 包的形式创建了一个补丁，[**http 2-express-bridge**](https://www.npmjs.com/package/http2-express-bridge)。**

```
npm install http2-express-bridge
```

**代码用法类似于第一个代码片段中的服务器代码。**

```
const express = require('express')
**const http2Express = require('http2-express-bridge')** const http2 = require('http2')
const { readFileSync } = require('fs')// only change required
**const app = http2Express(express)** 
app.get('/express', (req, res) => {
  res.send('Hello World');
})const options = {
  key: readFileSync('<Certificate Key>'),
  cert: readFileSync('<Certificate file>'),
  allowHTTP1: true
}const server = http2.createSecureServer(options, app)
server.listen(3000)
```

**就这样，代码工作了。通过选项中的`allowHTTP1`标志，当客户端不支持 **HTTP/2** 时，它会还原为 **HTTP/1.1** 。**

**你可以在这里查看[包的代码。如上面的代码所示，这个包与 CommonJS 一起工作。它也适用于 ES 模块和 TypeScript。](https://github.com/rahulramesha/http2-express-bridge)**

**快乐复用！**

> ****PS:** 这是故事的前半部分。另一个关注**服务器推送**的部分将在不久的将来发布。**

***更多内容请看*[*plain English . io*](http://plainenglish.io/)**