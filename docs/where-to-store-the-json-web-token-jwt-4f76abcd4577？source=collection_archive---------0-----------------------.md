# 应该在哪里存储 JSON Web 令牌(JWT)？

> 原文：<https://javascript.plainenglish.io/where-to-store-the-json-web-token-jwt-4f76abcd4577?source=collection_archive---------0----------------------->

![](img/30c3d0f5679a34b15dcddc6a90150066.png)

Where to Store JWT

我设计和开发 web 应用程序已经超过 7 年了。

这些年来，我见过很多认证机制，有些是 RESTful 的，有些不是。RESTful 服务大多使用 JSON Web 令牌(JWT)作为认证令牌。

每当我实现基于 JWT 的身份验证时，我都会问自己这个问题，“**我们在哪里存储 JWT？”**

编辑:本文只关注浏览器的实现。

让我们来回答这个大问题。

我们有三种在客户端存储数据的选择，每一种都有自己的优缺点。选项包括:

1.  饼干
2.  本地存储
3.  会话存储

## **饼干**

![](img/9b9b3561fdf1dec7d4a25f30a7f3d7f1.png)

如果您在 cookie 上设置了 JWT，浏览器将自动发送令牌以及相同站点请求的 URL。但是它容易受到 CSRF 的攻击。

我们可以通过设置一个带有`SameSite=strict`的 cookie 来保护站点免受`CSRF`的攻击

*编辑 1:*i̶n̶̶g̶e̶n̶e̶r̶a̶l̶̶p̶e̶o̶p̶l̶e̶̶m̶i̶g̶h̶t̶̶t̶h̶i̶n̶k̶,̶̶x̶s̶s̶̶c̶a̶n̶̶b̶e̶̶d̶e̶f̶e̶a̶t̶e̶d̶̶i̶f̶̶w̶e̶̶s̶e̶t̶̶t̶h̶e̶̶h̶t̶t̶p̶o̶n̶l̶y̶̶f̶l̶a̶g̶,̶̶b̶u̶t̶̶i̶t̶̶i̶s̶̶p̶o̶s̶s̶i̶b̶l̶e̶̶t̶o̶̶a̶t̶t̶a̶c̶k̶̶b̶y̶̶u̶s̶i̶n̶g̶̶x̶s̶t̶̶"̶s̶u̶b̶s̶e̶t̶"̶̶(̶k̶i̶n̶d̶a̶)̶̶o̶f̶̶x̶s̶s̶.̶

*编辑 2:* 通过设置`httpOnly`旗，我们可以轻松叛变 XSS。

**优点:**

1.  浏览器将自动向服务器发送令牌。
2.  相同的令牌可用于应用程序实例的多个选项卡。

**反对:**

1.  易受 XSS 攻击。
2.  如果您使用像 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6750) 这样的协议，您需要在报头中附加令牌。

**本地存储**

![](img/1a77232240ac6479b2543d6fa0f592d3.png)

localStorage 不会自动随 URL 一起发送数据。因此，您需要为每个 URL 实现 auth 令牌系统。但最棒的是，这种方法不会受到 CSRF 的攻击。

**优点**

1.  不容易受到 CSRF 的攻击。
2.  相同的令牌可用于应用程序实例的多个选项卡。

**Con**

1.  易受 XSS 攻击。
2.  您需要为发送令牌实现一种机制。

**会话存储**

![](img/69dfd653322d5ca31918521381c30109.png)

会话存储与本地存储非常相似，只是令牌只能访问一个选项卡，一旦选项卡关闭，会话就会被销毁。所以它**对【T4 记得我】这样的功能**没用。但这可用于多重登录功能，如选项卡 A 处于不同的登录状态，而选项卡 B 处于不同的登录状态。

**优点:**

1.  不容易受到 CSRF 的攻击。
2.  易于在一个浏览器中实现多次登录。

**不利:**

1.  易受 XSS 攻击。
2.  一旦选项卡关闭，会话数据就会被销毁。

您可能会注意到，所有 3 种方法都有相同的缺点—“**易受 XSS 攻击”。**是的，所有这些方法都容易受到 XSS 的攻击。请务必关心 XSS，并始终遵循保护 XSS 的[最佳实践](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)。

## **结论**

默认情况下，localStorage 和 SessionStorage 都不受 XSS 保护。

然而，Cookie 提供了一系列安全选项，如`SameSite`、`HttpOnly`等。所以搭配曲奇就好了。

***“用一些安全标志将你的 JWT 存储在 Cookie 中。”***

## 旁注:

如果你使用 Express，[这些包](https://medium.com/hackernoon/express-js-important-npm-packages-related-to-security-2393466e18d5)可能有助于提高你的应用程序安全性。

另外，看看我最近的文章

1.  [深入了解摇树](/deep-dive-into-tree-shaking-ba2e648b8dcb)(如何减少你的包裹大小)
2.  [5 使用效果无限循环模式](/5-useeffect-infinite-loop-patterns-2dc9d45a253f)

我发现这些文章对我有用，也许这些对你也有用。

[](https://scotch.io/bar-talk/why-jwts-suck-as-session-tokens) [## 为什么 jwt 不适合作为会话令牌

### JSON Web 令牌(jwt)现在非常热门。它们在 web 开发中风靡一时:有了这些神奇的东西…

scotch.io](https://scotch.io/bar-talk/why-jwts-suck-as-session-tokens) [](https://auth0.com/docs/security/data-security/token-storage#don-t-store-tokens-in-local-storage) [## 令牌存储

### 保护进行 API 调用的 spa 伴随着他们自己的一系列问题。你需要确保代币和其他…

auth0.com](https://auth0.com/docs/security/data-security/token-storage#don-t-store-tokens-in-local-storage) [](https://stackoverflow.com/questions/44133536/is-it-safe-to-store-a-jwt-in-localstorage-with-reactjs) [## 将 JWT 储存在带有 ReactJS 的本地仓库中安全吗？

### 在大多数现代的单页面应用程序中，我们确实必须将令牌存储在客户端的某个地方(大多数…

stackoverflow.com](https://stackoverflow.com/questions/44133536/is-it-safe-to-store-a-jwt-in-localstorage-with-reactjs) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)