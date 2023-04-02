# JSON Web 令牌简化了身份验证

> 原文：<https://javascript.plainenglish.io/authentication-simplified-with-json-web-tokens-25880e91c0?source=collection_archive---------17----------------------->

## 保护您的 web 应用程序的快速而简单的方法

![](img/2f66fa6a257edcf043fbc3912e495216.png)

Photo by [Tima Miroshnichenko](https://www.pexels.com/@tima-miroshnichenko?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/man-people-woman-water-6266301/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

JSON web 令牌(JWT)是向任何 web 服务添加身份验证和授权的一种快速而简单的方法。

虽然身份验证和授权听起来相似，但它们是两个根本不同的东西。

认证是确认用户是他们声称的那个人的过程。用户名和密码、face ID 和一次性密码都是身份验证的例子。

另一方面，授权限制了允许用户做什么的范围。与普通用户相比，授予管理员额外的访问权限就是授权的一个例子。

假设您使用用户名和密码登录到 Medium。如果成功，灵媒已经通过**认证**你就是你声称的那个人。然后你可以去更改你的个人资料设置，因为这是你自己的账户，你被**授权**这么做。

# 什么是 JWT

JSON web 令牌，或简称为 JWT，是一种安全表示[声明的简洁方法](https://tools.ietf.org/html/rfc7519)。从本质上来说，这是一种双方交换信息的安全方式，也就是**数字签名**。

JWT 由三部分组成。报头、有效载荷和签名验证。

报头数据标识用于生成签名的算法和令牌类型。

有效载荷是您希望交换的 JSON 编码数据。

最重要的是签名，它是通过加密哈希函数运行您的头、有效负载和秘密的组合来进行数字签名的。

![](img/d08db3c71b94e03fcfb62987366c1385.png)

JWT Info — From [Jwt.io](https://jwt.io/)

# 任何人都可以破译 JWT

不相信我？来吧，把下面的 JWT 复制到[这个网站](https://jwt.io/)。

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.o52bYlRaL9DW_IphDyb26eK9ZM4z9o8y-Ne-A7SzroI
```

但这不安全，我什么都看得到！

没那么快。

虽然你可以很容易地解码任何 JWT(这是故意的)，创造一个假的几乎是不可能的。

# 数字签名

这背后的神奇之处在于用于创建数字签名的 [**单向**散列函数](http://www.aspencrypt.com/crypto101_hash.html)。

创建 JWT 时，您可以通过哈希函数运行标头、有效负载和密钥，对其进行数字签名。

如果你想知道加密散列函数是如何工作的，那么读一下[。简而言之，它是一种对给定的输入产生相同输出的方式，以这种方式无法确定原始输入。](http://www.aspencrypt.com/crypto101_hash.html)

例如，当对 JWT 的数字签名进行编码时，下面的内容将通过一个单向散列函数来产生一个唯一的结果。

```
hash(header.payload.**my-super-secret-key)** =>F2QT4fwpMeJf36POk6yJV_ad
```

如您所见，报头和有效载荷很容易被解码。秘钥是保证 JWT 安全的关键。如果其他人发现了你的秘密密钥的价值，那么他们将能够**绕过你的授权**。

> JWT 只有在签名时使用的密钥与发行时使用的密钥相同时，才具有有效的签名。

# 要求

JWT 的有效载荷应该包含用户的[声明](https://tools.ietf.org/html/rfc7519#section-4)。这些声明代表了关于用户和其他附加数据的各种声明。

如何选择命名这些不同的主张取决于你。然而，在[官方文件](https://tools.ietf.org/html/rfc7519#section-4)中列出了指导方针。

对于这个例子，我选择对我的令牌进行如下声明。

```
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

*   sub——subject 的缩写，在本例中是用户的 ID。
*   用户名。
*   无论用户是否是管理员。

当决定你希望做出哪些声明时，请记住，JWT 可以很容易地被解码以暴露这些信息。所以，不要在令牌内编码任何敏感数据**。**

# 确认

假设提供的 JWT 是有效的，那么为了验证令牌的真实性，需要检查签名。

如前所述，JWT 的数字签名是通过将报头和有效载荷数据以及您的密钥传递给单向哈希函数来创建的。

```
hashFunction("base64EncodedHeader.base64EncodedPayload.secret")
```

您可以通过自己计算该签名并将其与令牌提供的签名进行比较来确定令牌是否有效。

# 传动装置ˌ[机]变速器

当向受保护的资源提交请求时，您应该使用[承载模式](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization)将 JWT 嵌入到 HTTP 请求的授权头中。

```
Authorization: Bearer <YOUR-JWT-HERE>
```

# 我应该用 JWT 的吗

与[会话](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)相比，JWT 会话的设置和管理要简单得多。在大多数情况下，您可以安装下面的模块之一，只需几行代码就可以启动并运行。

*   快速且易于设置。
*   服务器上没有状态的持久性，所有都封装在 JWT 声明中。
*   可伸缩性不是问题，因为客户端存储 JWT。

也就是说，他们也有一些弱点。

*   您的密钥被泄露的风险。
*   带宽，JWT 的大小明显大于会话 cookie。
*   撤销令牌可能比使会话无效更复杂。

JSON web 令牌是否适合您的应用程序将取决于您的特定需求。但是，它们是开始一些简单、安全和可扩展的身份验证的好方法！

如果你喜欢这篇文章，并且愿意支持我成为一名作家，考虑注册[成为一名媒体成员](https://adam-galtrey.medium.com/membership)。每月只需 5 美元，你就可以无限制地阅读 Medium 上的所有文章。如果你[用我的链接](https://adam-galtrey.medium.com/membership)注册，我也会赚一小笔佣金。

# JWT 图书馆

*   【JavaScript 的 JWT
*   [Python 的 JWT](https://pyjwt.readthedocs.io/en/stable/)
*   [面向 Java 的 JWT](https://github.com/auth0/java-jwt)
*   [JWT 为 C#](https://docs.microsoft.com/en-us/dotnet/api/system.identitymodel.tokens.jwt.jwtsecuritytokenhandler?view=azure-dotnet)
*   [JWT 围棋](https://github.com/dgrijalva/jwt-go)