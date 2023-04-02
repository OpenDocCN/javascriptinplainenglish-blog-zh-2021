# 用于社交登录(谷歌、脸书、推特等)的 NestJS 中的 OAuth2

> 原文：<https://javascript.plainenglish.io/oauth2-in-nestjs-for-social-login-google-facebook-twitter-etc-8b405d570fd2?source=collection_archive---------0----------------------->

关于 NestJS 的例子少得惊人。自 2018 年以来有一个[开放问题](https://github.com/nestjs/docs.nestjs.com/issues/75)要求它们，但回复( [1](https://github.com/nestjs/docs.nestjs.com/issues/75#issuecomment-436275866) 、 [2](https://github.com/nestjs/docs.nestjs.com/issues/75#issuecomment-437791849) )和其他地方的资源( [1](https://dev.to/imichaelowolabi/how-to-implement-login-with-google-in-nest-js-2aoa) 、 [2](https://stackoverflow.com/questions/67237523/oauth2-flow-in-full-stack-nestjs-application) )仅提供了部分/不完整的概述。

![](img/e6dd9e4aabd09f3d4d454f2d5d5b582f.png)

这里我将展示一个全栈认证流程，包括获取社交令牌后的认证请求，对于 GraphQL 也是可选的。您可以在 [nestjs-starter repo](https://github.com/thisismydesign/nestjs-starter) 中查看一个工作示例。

解决方案概述:

*   1，使用`@nestjs/passport`和`passport-google-auth`实现 Google auth(其他提供者很相似)。
*   2、一旦重定向回应用程序，就颁发一个 JWT 令牌，这样应用程序就可以管理用户的会话。
*   3、用 JWT 策略保护 REST 和 GraphQL 端点。

第一步。此处的[归功于 Google Oauth 策略的实施，并展示了如何通过截图在 Google 中创建 Oauth 应用程序。代码应该如下所示:](https://dev.to/imichaelowolabi/how-to-implement-login-with-google-in-nest-js-2aoa)

你现在可以使用`@UseGuards(GoogleOauthGuard)`。你会注意到，每个受保护的路线重定向到谷歌认证。我们接下来会解决这个问题。

第二步。现在应用程序知道了用户，我们可以在应用程序中处理用户的会话。我们将颁发一个 JWT 令牌，并使用相应的保护措施来保护经过认证的路由。这在[正式文件](https://docs.nestjs.com/security/authentication)中有解释。

我们需要在服务器和客户端之间传输这个令牌。一个安全易用的选择是通过一个 SameSite HttpOnly Cookie。代码应该如下所示:

修改 OAuth 控制器以颁发 JWT 令牌:

第三步。我们现在可以使用`@UseGuards(JwtAuthGuard)`来保护经过认证的路由。[文档](https://docs.nestjs.com/security/authentication#graphql)中显示的图形 QL 开箱即用！

最后，我们用 NestJS 实现了端到端的社会认证。你会在回购协议中发现更多很酷的功能([https://github.com/thisismydesign/nestjs-starter](https://github.com/thisismydesign/nestjs-starter))。我还写过一个结合 Next.js 和 NestJS 、以及[自动键入 GraphQL 查询和结果与 Apollo](https://csaba-apagyi.medium.com/automagically-typed-graphql-queries-and-results-with-apollo-3731bad989aa) 的 [MVC 设置。](https://csaba-apagyi.medium.com/nestjs-react-next-js-in-one-mvc-repo-for-rapid-prototyping-faed42a194ca)

*更多内容参见* [*浅显易懂*](http://plainenglish.io/)