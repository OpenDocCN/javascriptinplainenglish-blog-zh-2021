# 基于 Cookie 的 JWT 认证

> 原文：<https://javascript.plainenglish.io/nest-js-cookie-based-jwt-authentication-615be1f907a9?source=collection_archive---------10----------------------->

![](img/07d7f25f8be8b4f4d98980f3d1397eae.png)

我们开始使用 Nest.js 作为我们的 Node + TypeScript 服务开发的主要框架，主要是因为它具有内置的配置，并且可以随时使用与 TypeScript 集成在一起的项目结构。最重要的是，它包含了构建和林挺脚本，这是很难从零开始，它只是开箱即用。

在[https://blockpulsar.com](https://blockpulsar.com/)我们一直专注于灵活的服务开发方式，这样每项服务都将是独立的原子，以获得更好的可扩展性和易于维护性。这就是为什么从一开始我们就实现了基于 JWT 令牌的身份验证，这样我们就可以嵌入关于个人 HTTP 请求的最常用信息，而其他服务可以使用我们的 JWT 密钥提取这些信息。这听起来像是一种非常标准的做事方式，但我仍然想指出我们这样做的方式，以及当我们将所有内容移入 Cookies 而不是保存在本地存储中时，结构变得多么简单，这样我们的 UI 现在就不会通过`Authorization`头发送它。一切都是通过浏览器 cookie 执行所有对 API 的请求来实现的，顺便说一下，这比本地存储更安全。

# 为 Nest.js 设置 Passport JWT

Nest.js 由所谓的原子模块组成，这些原子模块通过可注入类原则连接到主应用程序模块。嗯，这只是一种奇特的说法，有一个主模块调用所有其他模块来初始化它们，共享相同的上下文，并为 Express.js 设置中间件，这是实际的 HTTP 处理程序。理解这一点很重要，最终 Express.js 是处理请求的人，Nest.js 只是一个包装器，这意味着所有的 Express.js 库都可以与 Nest.js 一起使用，包括 Passport.js 和`passport-jwt`库，这是我们这里的基础。

作为认证的核心入口点，我们有一个名为`auth`的模块，如下所示

```
// Auth Module
import { PassportModule } from '@nestjs/passport';
import { JwtModule } from '@nestjs/jwt';
import { JwtStrategy } from './jwt.strategy';
import { AuthService } from './auth.service';@Module({
  imports: [
    ...
    PassportModule.register({
      session: false,
    }),
    JwtModule.register({
      secret: AppConfig().jwtSecret,
      signOptions: { expiresIn: '7d' },
    }),
    ...
  ],
  providers: [
    ...
    AuthService,
    JwtStrategy
    ...
  ],
  controllers: [AuthController],
})
export class AuthModule {}
```

这是一个初始化结构，其中我们有来自`@nestjs/passportlibrary`的主 PassportModule，它制作所有的中间件附件和核心 passport.js 逻辑，类似于我们用`passport.use`函数对 Express.js 所做的，它只是变得更像这里的类型脚本。

`JwtStrategy`另一方面，我们为 Nest.js 添加了一个定制的可注入策略，它实际解析 JWT 并注册认证用户来请求上下文，类似于所有其他 passport.js 策略，但作为一个 Nest.js 模块来保留可注入模块的概念。

```
// JwtStrategy for handling Passport JWTimport { ExtractJwt, Strategy } from 'passport-jwt';
import { PassportStrategy } from '@nestjs/passport';
import { Injectable } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor(private readonly configService: ConfigService) {
    super({
      jwtFromRequest: ExtractJwt.fromExtractors([
        ExtractJwt.fromAuthHeaderAsBearerToken(),
      ]),
      ignoreExpiration: false,
      secretOrKey: <providing secrets from configService here>,
    });
  }async validate(payload: any) {
    // validating payload here
		if (<user is authenticated>) {
			return <user data here>
		}// return 401 Unauthorized error
    return null;
  }
}
```

这是 Nest.js 的基本 JWT 策略，但它是为了让 JWT 令牌来自`Authorization: Bearer`头，这对于大多数应用程序来说是可以的，特别是如果你有多个客户端使用移动应用程序，但对我们来说，拥有基于 cookie 的授权也更灵活，这意味着我们只是通过 Cookie 传递令牌，而不期望有授权头。这就给我们带来了像这样的自定义 JWT 提取器函数

```
// JwtStrategy for handling Passport JWT...
...
import { Request as RequestType } from 'express';@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor(private readonly configService: ConfigService) {
    super({
      jwtFromRequest: ExtractJwt.fromExtractors([
        JwtStrategy.extractJWT,
        ExtractJwt.fromAuthHeaderAsBearerToken(),
      ]),
      ignoreExpiration: false,
      secretOrKey: <providing secrets from configService here>,
    });
  }private static extractJWT(req: RequestType): string | null {
    if (
      req.cookies &&
      'token' in req.cookies &&
      req.cookies.user_token.length > 0
    ) {
      return req.cookies.token;
    }
    return null;
  }
  ...
  ...
}
```

你可以看到我们有一个由`JwtStrategy.extractJWT`和`ExtractJwt.fromAuthHeaderAsBearerToken()` JWT 令牌提取器组成的数组，这意味着它也支持拥有一个授权头，因为`ExtractJwt.fromExtractors`的工作方式是检查所有的处理程序，并从第一个成功执行的处理程序中提取 JWT 令牌。

其余的逻辑与常规的 JWT Passport 策略相同，我们只需检查用户权限和`JwtStrategy.validate`函数中的令牌有效性，如果成功或者我们想要抛出`401 Unauthorized`错误，则返回`User | null`。请注意，validate 函数是从 Passport 模块内部调用的，每个 Nest.js Passport 策略实现都必须有那个`validate`函数，类似于我们以前对 Express.js 使用的`done`回调。

# 多域和基于 Cookie 的 JWT 令牌

如果您有像我们这样的多域结构，基于 Cookie 的身份验证系统有时会很有挑战性。例如，我们的主要 web 应用程序托管在[https://app.blockpulsar.com](https://app.blockpulsar.com/)下，API 在这里[https://api.blockpulsar.com](https://api.blockpulsar.com/)下，最初，还不清楚如何使 cookie 设置/获取过程灵活，以便以后使用，特别是如果我们知道一些浏览器不支持通配符基于域的访问。很快我们就发现，我们只需要修正一些严格的规则，比如

*   UI React 应用程序不应该读取委托给 API 的 Cookies，它只需要发送一个 API 请求并获取所需的信息，如用户身份验证状态或用户数据
*   为了让注销 API 完全控制它的 cookie，UI 必须发送一个 API 请求来删除 cookie，以便让用户从浏览器中注销

这有助于将事情安排到位，因此现在只有我们的 API 负责读写与身份验证相关的 cookies，UI 只与 API 进行通信，否则，它可能会变得非常混乱。通常，当您进行双向读写访问时，很容易出现过时的数据甚至损坏的数据，这是因为可能出错的情况越来越多。

# 从 API 端注销用户，而不是从 UI

修正了让唯一的 API 负责管理认证 cookie 的规则，这就很容易理解，即使注销 UI 也不应该通过删除 cookie 来接触 Cookie，这显然是可以做到的，但是因为 API 总是希望有一个即将到来的 Cookie，所以它也必须验证是时候删除认证 Cookie 了。

注销用户的端点非常简单，如下所示

```
@Get('signout')
async logout(@Res({ passthrough: true }) res: ResponseType) {
  // Some internal checks
  ...
  ...
  res.cookie('token', '', { expires: new Date() });
  ...
}
```

它删除了`token` cookie，并认为用户被分配出去了。这非常简单，但是它也有助于跟踪用户何时退出，或者 cookie 何时过期。正如你所想象的，它拥有强大的分析能力，比如平均用户会话时间等。

# 结论

由于这种直观的结构和可读的代码库，Nest.js 帮助我们更容易、更快地完成工作。拥有原子模块的方式我们已经能够支持许多认证类型，而不像在 Nest.js 之前那样使 Passport.js 回调复杂化。

因为我们的用户界面只是发送一个简单的 Axios 请求，而没有考虑添加自定义标题或决定如何注入用户凭据，所以 JWT + Cookie 对我们来说工作得更好，浏览器只是将 Cookie 发送到相关的 https://blockpulsar.com 域名，如果用户通过身份验证，它就准备好了。否则它只会拒绝有`401 Unauthorized`错误的东西，UI 会轻松处理。

当然，如果你有一个移动应用程序，你的项目的结构会有所不同，因为你没有 Cookie，所以你仍然需要通过标准的授权头发送 JWT 令牌，但即使这样，这个 JwtStrategy Nest.js 可注入类也能顺利地处理事情。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)