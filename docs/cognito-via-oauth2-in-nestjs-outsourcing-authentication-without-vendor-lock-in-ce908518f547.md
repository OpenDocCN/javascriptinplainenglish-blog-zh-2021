# 在 NestJS 中通过 OAuth2 的 Cognito:无供应商锁定的外包认证

> 原文：<https://javascript.plainenglish.io/cognito-via-oauth2-in-nestjs-outsourcing-authentication-without-vendor-lock-in-ce908518f547?source=collection_archive---------0----------------------->

认证是复杂的，如果能外包就太好了。但我也想避免被锁在里面。我可以鱼与熊掌兼得吗？

![](img/2da4b1cec34db3182213e6c3025f42c4.png)

TLDR；是啊！在[nestjs-starter repo](https://github.com/thisismydesign/nestjs-starter)中，我通过 OAuth2 使用 Cognito 及其托管 UI，同时将所有用户数据保存在我的应用程序中。所以大部分认证的复杂性被外包给一个现成的解决方案(价格[可能是最低的](https://aws.amazon.com/cognito/pricing/)，我可以随时替换这个策略，例如通过[直接实现社交登录](https://csaba-apagyi.medium.com/oauth2-in-nestjs-for-social-login-google-facebook-twitter-etc-8b405d570fd2)。

通过这种方式，我可以以集成一个 OAuth2 提供商为代价，获得许多身份验证策略(密码、谷歌、脸书等)。

[Setup Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-app-integration.html) :创建用户池，App 客户端，配置托管 UI。将配置添加到`.env`文件中。

然后我们将使用`passport-oauth2`，一个通用的 OAuth2 策略来与 Cognito 集成。

需要记住的唯一技巧是，在这个通用策略中，`id_token`没有暴露给`validate`方法，因此我们需要进行一个额外的调用。

这是基本的认知整合！要使这成为一个完整的身份验证流程，还需要两个步骤:

*   在重定向端点中发布 JWT 令牌，以便我们可以在应用程序中处理用户会话。你可以在我的[oauth 2 in NestJS for social log in](https://csaba-apagyi.medium.com/oauth2-in-nestjs-for-social-login-google-facebook-twitter-etc-8b405d570fd2)文章中看到如何做。
*   在`validate`回调中查找或存储用户数据。我在 [nestjs-starter](https://github.com/thisismydesign/nestjs-starter) repo 中使用一个带有 TypeORM 存储库的数据库。你也可以从[官方文件](https://docs.nestjs.com/techniques/database)中了解更多。

最后，这是一种外包身份验证复杂性的方法，而不会被提供商锁定！你会在回购协议([https://github.com/thisismydesign/nestjs-starter](https://github.com/thisismydesign/nestjs-starter))中发现更多很酷的功能。我还写过一个结合 Next.js 和 NestJS 的 [MVC 设置，以及](https://csaba-apagyi.medium.com/nestjs-react-next-js-in-one-mvc-repo-for-rapid-prototyping-faed42a194ca)[用 Apollo](https://csaba-apagyi.medium.com/automagically-typed-graphql-queries-and-results-with-apollo-3731bad989aa) 自动键入 GraphQL 查询和结果。

*更多内容参见* [*简明英语. io*](http://plainenglish.io/)