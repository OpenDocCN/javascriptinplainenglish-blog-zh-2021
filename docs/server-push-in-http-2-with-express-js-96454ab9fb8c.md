# 如何使用 Express 在 HTTP/2 中执行服务器推送

> 原文：<https://javascript.plainenglish.io/server-push-in-http-2-with-express-js-96454ab9fb8c?source=collection_archive---------6----------------------->

既然在 Express 中使用 http2 是可能的，默认情况下服务器推送也是可能的。但是使用服务器推送来获得最佳性能需要更多的努力。

![](img/b3bd22bb11fca2ac278bc89bdc624254.png)

Photo by [Jordan Harrison](https://unsplash.com/@jordanharrison?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这是我上一篇文章的延续，解释了如何使用 **http2-express-bridge** 来支持 HTTP/2 和 Express js 的使用。可以在这里阅读之前的文章[。](https://rahulramesha.medium.com/serving-hello-world-with-http2-and-express-js-4dd0ffe76860)

让我们想象在 HTTP/1.1 中提供一个包含 CSS 和 Javascript 链接的 HTML 页面。

*   浏览器/客户端向服务器请求路径。
*   服务器用一个 HTML 文件响应，然后关闭连接。
*   浏览器读取文件并意识到它需要 CSS 和 Javascript 文件，然后分别请求这些路径。
*   因此，需要建立多个连接来获取加载页面所需的所有文件。

我知道你在想什么——这听起来效率很低，事实也确实如此。有了 HTTP/2 的多路复用，即使避免了多个连接，客户机仍然必须通过 HTML 文件才能意识到它需要来自服务器的其他文件。

使用**服务器推送**，服务器可以决定推送必要的文件以及请求的文件。在一个连接中发送所有内容。使用 **http2-express-bridge** ，将`push()`方法添加到响应对象中。可以按如下方式使用:

```
app.get('/bar', (req, res) => { res.push(['/bar.js', '/foo.js'], staticPath)
    res.send(`
        <!DOCTYPE html>
        <html lang="en">
            <head>
                <meta charset="UTF-8">
                <title>Bar Document</title>
            </head>
            <body>
                This is a bar document.
                <script src="/foo.js"></script>
                <script src="/bar.js"></script>
            </body>
        </html>`);})
```

`push()`方法接受两个参数。

*   第一个参数是单个路径或路径数组。这些路径应该与 HTML 中的路径完全相同。
*   第二个参数是提供文件的静态路径。

`push()`方法被设计成即使它导致错误，它也只是记录错误并发送响应。

仅此而已，它应该能提高你的表现。但也不尽然！

## **呃？为什么不呢？**

这样做的问题是，每次请求路径时，服务器都会推送文件，即使浏览器已经缓存了它们。

这只是问题之一。为了优化服务器推送的性能，必须遵循一些原则。详情请参见[HTTP/2 推送的经验法则](https://docs.google.com/document/d/1K0NykTXBbbbTlv60t5MyJvXjqKGsCVNYHyLEXIxYMv0/edit?usp=sharing)。

我同意在您的服务器上实现这些指导方针似乎是一项艰巨的工作。但值得庆幸的是，谷歌的一名工程师已经创建了一个通用的解决方案包[H2-自动推送](https://www.npmjs.com/package/h2-auto-push)。你可以在这里阅读它是如何工作的以及它的性能结果[(由软件包的创建者编写；强烈推荐去看看)。](https://medium.com/the-node-js-collection/node-js-can-http-2-push-b491894e1bb1)

这个包不能开箱即用，它必须适应正在使用的框架。 [Fastify](https://www.fastify.io/) 已经在[Fastify-自动推送](https://www.npmjs.com/package/fastify-auto-push)中进行了改编。我决定把它改编成 Express，在[**http 2-Express-autopush**](https://www.npmjs.com/package/http2-express-autopush)。

```
npm install http2-express-autopush
```

这个包是一个 express 中间件，在它的基本版本中可以完全像 *express.static* 中间件一样使用。

```
const autopush = require('http2-express-autopush')...app.use(autopush(staticPath))
```

这样，中间件的基本功能就是从路径中提供静态文件。除此之外，它还观察请求的路径，并记录从同一客户端请求的文件。因此，下次它从不同的客户端收到请求时，它会推送记录的路径，并发送一个 cookie。此 cookie 包含已推送文件的信息。因此，它不会在同一个会话中将它们推送到客户端。

有了这个中间件，您不需要特别地按需推送，让中间件决定何时按需推送文件。

中间件有可选的第二个和第三个参数。

*   第二个参数与 *express.static* 中间件中的第二个参数相同。
*   第三个参数是一个对象，其值可用于微调要推送的路径。

默认情况下第三个参数是:

```
{  
    warmupDuration: 500,
    promotionRatio: 0.8,
    demotionRatio: 0.2,
    minimumRequests: 1 
}
```

你可以在这里阅读关于这些参数[的更多信息。](https://www.npmjs.com/package/h2-auto-push#assetcacheconfig)

希望这已经使您具备了使用**服务器推送**和 Express 来获得最佳性能的知识。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)