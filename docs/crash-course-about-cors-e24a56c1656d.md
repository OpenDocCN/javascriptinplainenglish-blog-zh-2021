# CORS 速成班

> 原文：<https://javascript.plainenglish.io/crash-course-about-cors-e24a56c1656d?source=collection_archive---------10----------------------->

## 处理和理解 CORS 误差基础的指南。

![](img/8bdaf0684d45d4ae427c24971022254b.png)

Crash course about CORS

*这篇文章献给我亲爱的兄弟* [*奥马尔·科恩*](https://www.linkedin.com/in/omercohenaviv/) *，他一直在努力成为一名更好的开发者。*

```
Access to XMLHttpRequest at 'https://localhost:3000' from origin 'https://localhost:8000' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource
```

上面的错误你看着眼熟吗？

如果您是全栈 web 开发人员，您很可能已经解决了这个错误。有经验的全栈开发人员会意识到他们忘记了添加 CORS 头文件作为中间件，新手必须谷歌一下。

但是这个 CORS 是怎么回事呢？我们为什么需要它？以及理解它将如何使我们成为更好的全栈开发人员。关于它的所有内容，更多内容将在下一篇文章中介绍。敬请期待！

# 这个 CORS 是怎么回事

CORS 主张跨产地资源共享。简而言之，这意味着，当我们的浏览器从域‘A’获得资源(Javascript、HTML、CSS)时，我们有一些关于与域‘B’共享它的规则。

实际上，CORS 是 SOP 政策的延伸，所以为了理解 CORS，我们必须熟悉同源政策。

SOP 是一种网络浏览器安全机制，旨在保护您的私人数据免受恶意网站的侵害。

当浏览器向服务器发送 HTTP 请求时，与其他域相关的任何 cookie(包括身份验证会话 cookie)也会作为请求的一部分发送。现在想象一下，如果这些敏感数据被发送到我们访问的每个网站，会发生什么？这就是 SOP 发挥作用的地方。它检查我们拥有的敏感数据(如 cookies)是否“属于”我们正在访问的当前网站，然后才允许访问这些数据。

对于 DOM 访问(通过 JavaScript)也是如此。根据标准操作程序，如果一个 JavaScript 文件(来自其他来源)试图从一个非 HTML 文件来源的域访问您的 DOM 元素，它将被您的浏览器阻止。

> 假设你不知何故被骗去参观 www.your-bank.bad-site.com。在那个不良网站上，有一个 [iframe](https://www.w3schools.com/html/html_iframe.asp) 加载[*www.your-bank.com*，](http://www.your-bank.com,)在那里你进行合法登录。登录后，在坏网站上的一个简单的 JavaScript 调用可以被用来访问 iframe 中加载的[*【www.your-bank.com】*](http://www.your-bank.com)的 DOM 元素，比如你的账户余额。现在想象一下他们能做什么…

```
frames.bank_frame.document.getElementById("balance").value
```

> 它所做的是访问 iframe 元素(名为 *bank_frame* ，然后在 iframe 的 DOM 中，它访问名为 *balance* 的 HTML 元素并获取其值。当然，这甚至可以扩展到伪造浏览器调用，将您的资金发送到其他地方！如果没有同源策略，这些跨站点请求可能会在您不同意或不知情的情况下执行。

然而，重要的是要知道，SOP 也寻找我们的浏览器上运行的文件的上下文。如果我们有一个从另一个来源(通过 CDN)加载的 JS 文件，浏览器将允许它在我们的浏览器上运行，因为它是由那个 HTML 文件加载的。它与我们的 HTML 文件具有相同的上下文。

顺便说一句，什么被认为是“同源”是有严格规定的。例如，其中一个具有相同的端口。因此，如果我们从 https://www.example.com:8080 的[，](https://www.example.com:8080,)获得一个 HTML 文件，它将不会与 https://www.example.com:8081 的[共享。](https://www.example.com:8081.)这听起来太严格了？这就是 CORS 开始行动的地方。

# 共享世界中的灵活性

到目前为止，我们已经了解了如何限制我们的浏览器共享来自不同来源的资源。但是如果我们真的想要共享资源呢？有没有安全的方法绕过 SOP 的严格机制？

考虑下面这个最常见的例子:我们进入一个网站并从中获取资源——一些 HTML、CSS 和 JS。现在，我们必须向不同的源发出另一个请求，以从 REST API 获取数据。根据 SOP，这是不允许的！请求将被发送，但是我们的浏览器将阻止响应。

CORS 配置主要在服务器端处理。我们基本上必须设置一些标头，这些标头将与来自服务器的响应一起发送。如果响应包含正确的标头，则浏览器不会阻止响应。我只想强调，CORS 和 SOP 政策是浏览器的事情。

例如，如果我们从浏览器向 REST API 发送一个请求，由于某种原因，服务器没有配置为向我们发送正确的头，从而使浏览器阻塞响应，有一种方法可以绕过它！

解决方案是建立一个代理，作为浏览器和 API 之间的“代理”。当代理向该服务器发送请求时，它当然不会阻止来自该服务器的响应(它不是浏览器)。然后，我们可以用正确的头设置代理，将响应发送回浏览器。

# 结论

在本文中，我们学习了 SOP 和 CORS。它们都旨在为网络用户提供安全和隐私机制。它使我们在浏览器中接收的数据(HTML 等)远离恶意攻击者。

重要的是要记住，CORS 是浏览器用户的一种安全机制，但我们是在服务器端设置的。如果来自服务器的响应具有正确的标题，那么我们的浏览器将不会阻止它。

我没有详细说明如何配置这些头，因为这篇文章是关于理解 CORS 一般是如何工作的，以及我们为什么需要它。如果您想了解如何配置 CORS 标头，可以使用以下资源:

*   [MDN 上的 CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)。
*   [好文章自媒体。](https://medium.com/@baphemot/understanding-cors-18ad6b478e2b)
*   [来自 Oauth 的完全指南。](https://auth0.com/blog/cors-tutorial-a-guide-to-cross-origin-resource-sharing/)

*更多内容看* [***说白了就是 io***](https://plainenglish.io) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。*