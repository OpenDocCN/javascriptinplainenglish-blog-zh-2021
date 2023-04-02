# CORS:简短而甜蜜的解释

> 原文：<https://javascript.plainenglish.io/cors-a-short-and-sweet-explanation-517443c367a6?source=collection_archive---------10----------------------->

如果你是一名网络开发人员，你可能遇到过 CORS，如果你遇到过 CORS，那很可能不是一次愉快的经历。
在本文中，您可以找到关于什么是 CORS 及其使用案例的简短解释。

![](img/a99f33dd5b077062c9b2d1c9cea95348.png)

Photo by [Usman Yousaf](https://unsplash.com/@usmanyousaf?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# CORS？那是什么？

跨源资源共享或 CORS 是 HTTP 的一项功能，它使得限制允许哪些源向 web 服务器发出请求变得容易。

假设我们有一个托管在`api.example.com`的 API。我们希望保护我们的 API，并确保没有其他应用程序可以访问我们的敏感 API 并执行可能的恶意(自动)请求。
我们需要指定只有`*.example.com`域被允许发出请求。这就是 CORS 的救星，具体的设置方式取决于你使用的语言和库，但是由于 CORS 是一种随处使用的技术，你可以在网上的某个地方找到一个详细记录的页面！

一旦你建立了它，它将是成功或失败的。相信我，你很快就会知道是哪一个。如果你把事情搞砸了，你可以在这篇文章的底部找到一个小建议来帮助你解决问题。

# CORS 飞行前

幕后还有一件很酷的事情，叫做 CORS 预检，它本质上是检查什么是允许的。想要发出请求的应用程序首先会调用服务器并询问“我可以做什么？”。

您的服务器将返回指定 URL 允许的每个方法以及可能给出的头。如果这些与需要发生的请求相匹配，我们就可以安全地发送实际的请求。

***side note****:CORS 错误，本质上是服务器在让你的应用知道它不被允许执行任何动作！*

这种预检是一种非常酷的技术，因为它可以让一切都变得更快。它遵循 fail-fast 原则，如果我们已经知道这个请求会失败，例如，因为 HTTP POST 是不允许的，那么我们为什么还要费心发送整个主体呢？

如果您正在查看服务器的日志，这些预检请求将作为 HTTP 选项请求弹出！

# 我怎么搞砸了？

不要误会我的意思，CORS 是一种神奇的技术，一旦你让它工作，它可以帮你省去很多麻烦。不过，把它弄得恰到好处真的很难。CORS 错误总是需要在服务器端修复！同样，这取决于你选择的语言，但是在 Node.js 中，我们要做的是安装和`app.use` cors。

```
import cors from "cors";app.use(cors({
  origin: ['http://localhost:8080'],
}));
```

这是你能做的最基本的设置之一。不要担心 99%的时间，这是所有你需要的设置。您需要知道的是，在那个名为`origin`的数组中指定的所有 URL 都将被允许发出请求。
如果你得到一个 CORS 错误，你可能正试图从一个不在这个数组中的 URL 请求！所有你需要做的就是指定正确和完整的域名，你就可以开始了！:D

祝你有创意的一天！💜

*更多内容尽在*[***plain English . io***](http://plainenglish.io)