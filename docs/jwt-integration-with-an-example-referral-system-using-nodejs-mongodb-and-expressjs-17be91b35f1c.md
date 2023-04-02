# 在 10 分钟内将 JWT 集成到您的认证系统中

> 原文：<https://javascript.plainenglish.io/jwt-integration-with-an-example-referral-system-using-nodejs-mongodb-and-expressjs-17be91b35f1c?source=collection_archive---------5----------------------->

## 通过使用 Node.js、MongoDB 和 Express 建立一个查询系统

![](img/9c1cc69bc074de5d350151663c6c9c7e.png)

Photo by [Jefferson Santos](https://unsplash.com/@jefflssantos?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/programming?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

欢迎光临！在这篇文章中，我们将学习如何使用 JSON Web 令牌(JWT)管理用户会话。最后，我们还将构建一个简单的推荐系统来演示 JWT 的工作流程。

如果您已经有了一个用户认证系统，那么您可以参考这篇文章，将 JSON web 令牌安全地集成到您现有的项目中。

不要在介绍上浪费更多的时间，让我们开始吧。

> 这篇文章是我上一篇文章(第二部分)的继续，在那篇文章中，我展示了带有电子邮件验证、忘记密码和重置密码功能的用户注册的实现。如果你想看看第一部分，使用这个[链接](https://pranesh-a-s.medium.com/how-to-build-simple-and-secure-rest-api-for-user-authentication-using-node-js-jwt-and-mongodb-2bdeb3e5427e)。

让我们看看我们的登录 API。

![](img/a40985afed9c40e3a3a30db93ce5bcab.png)

在这里，我们可以看到，一旦用户登录，我们只返回成功标志和一条消息，这不足以创建有效的会话。现在让我们为每次登录创建一个访问令牌(有效期为 1 小时),并将其发送给客户端。

# 什么是 JWT？

> JWT 只是一种会话数据有效负载 JSON 格式，由服务器加密签名。

更详细的[解释](https://jwt.io/introduction/):

JSON Web Token (JWT)是一个开放标准( [RFC 7519](https://tools.ietf.org/html/rfc7519) )，它定义了一种紧凑且独立的方式，以 JSON 对象的形式在各方之间安全地传输信息。该信息可以被验证和信任，因为它是数字签名的。jwt 可以使用秘密(使用 HMAC 算法)或使用 RSA 或 ECDSA 的公钥/私钥对进行签名。

## **生成令牌**

使用以下命令安装“`jsonwebtoken`”模块:

```
npm i jsonwebtoken --save
```

在用户/助手文件夹中，创建一个文件`generateJwt.js`

将你的 JWT 秘密添加到`.env`文件中

```
JWT_SECRET = <SOME_LONG_SECRET_KEY>
```

这个 JWT 秘密将被用作签署有效载荷的密钥。

保存文件并启动服务器。

> **注意**:秘密越长，我们的应用就越安全。因为我们使用的是 HMAC 算法(对称)，所以一个密钥就足够签名了。如果我们使用 RSA，那么我们需要 2 个密钥(私有和公共)。

更新用户模式以存储 accessToken。

```
accessToken: { type: String, default: null }
```

让我们在`user.controller.js file`中导入`generateJwt`函数，并用它来创建一个访问令牌。

是的，我们正在数据库中保存访问令牌。你们中的许多人可能认为使用 JWT 不是正确的方式，因为 JWT 的主要用途是方便**无状态**认证，这意味着我们不需要在服务器中存储信息。因为 JWT 本身包含过期时间、有效载荷、发行者等信息。，但我的目标是使用 JWT 创建一个**安全** API，我是认真的。

> ***注*** *:* JWT 自身并不安全。让它安全的是我们如何在我们的系统中使用它。我不愿意把这篇文章带走，因为这篇文章的目的是展示 JWT 与我们的认证系统的集成。

对于那些仍然对我为什么在 DB 中存储访问令牌感兴趣的人来说，我所做的是`whitelisting`令牌。为了提高底层系统的安全性，我们必须将令牌列入白名单或黑名单。最首选的方法是黑名单，与白名单相比，搜索空间要小得多。

> ***PS*** :当然，我不是安全专家。所以，如果我在安全方面错了，请让我知道。我很乐意学习。

现在让我们从邮差处登录:

![](img/db2852a922ac3e30de32d1694bef71cd.png)

酷！我们得到了 1 小时内有效的访问令牌。我们不会每次都得到相同的令牌。每次都会为每个人生成不同的令牌。

# **JWT 逮到你了**

关于 JSON web 令牌的另一个误解是，令牌是加密的，存储的所有信息都是完全安全的。我们必须明白，我们的有效载荷是“签名”的，而不是“加密”的。

让我们做一些实验。

这是我在响应中收到的访问令牌:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InNhdG9zaGlAZ21haWwuY29tIiwiaWQiOiJjYzkyZWNiYi1lOTlhLTQ4NWItOWFjMy04MTcwMWNkOWU5YmUiLCJpYXQiOjE2MTA3MzkwOTAsImV4cCI6MTYxMDgyNTQ5MH0.WKE_E3WB8s1yCpB1KO63wYtqxd_sjY_DDVldsxbrMqc
```

在浏览器中打开一个新标签，访问[http://calebb.net/](http://calebb.net/)并粘贴令牌。

你会看到这样的东西

![](img/44355af2571a8bd300cbb23579b1df5d.png)

是的，在没有密钥的情况下，通过解码**来检索我们存储在 JWT 中的 JSON 有效载荷是可能的。仅在验证 JWT 是否有效时才需要密钥。因此，我们不应该在 JWT 有效载荷中存储敏感信息，如密码、API 密钥等。**

我再次强调，JWT 本身并不安全。这取决于我们如何使用它。

# **实施简单转诊制度**

为了理解如何实现安全端点，我们将创建一个简单的引用系统。

它是这样工作的:

*   在注册期间为用户生成推荐代码，并将代码保存在数据库中。
*   注册时，从用户处获取推荐代码。
*   检查数据库中是否存在该推荐代码。
*   如果存在，那么存储细节，否则抛出一个错误。

为了生成推荐代码，我们将使用一个简短的唯一 Id 生成器“`nanoid`”。

安装依赖项:`npm i nanoid --save`

我们将使用包含字符 a-z、A-Z 和 0–9 的自定义字符集来生成推荐代码。

另外，将以下字段添加到用户模式中。

```
referralCode: { type: String, unique: true },
referrer: { type: String, default: null }
```

完成所有更改后，我们的用户模型将如下所示:

现在保存文件并重启服务器。

让我们注册并检查是否一切都如预期的那样运行良好。

![](img/82e9ac5c473af89603e9ce75a7b5990d.png)

酷！我们得到了我们的推荐代码`RiNb08qd`。让我们看看我们的 DB 系列。

![](img/cafb15806aa4f560110d47c9b92c0c50.png)

我们可以看到`referralCode`已经被添加到用户集合中。

让我们假设我们已经与我们的一些朋友分享了这个推荐代码。所以他/她在注册时输入我们的推荐代码。

![](img/51f92852fe8dad115b73454441480741.png)![](img/ed413c0683a560e5af3eeba84dc57d00.png)

有用！我们的朋友可以用我们的推荐代码注册。

现在让我们为我们的项目添加更多的功能。比方说，我们需要检索所有使用我们的推荐代码注册的帐户，当我们登录时，它必须显示在我们的仪表板上。

## **流程**

*   成功登录后，将 JWT 存储在客户端(在本地存储中，索引数据库等)。
*   然后用授权头中的访问令牌调用`GET /referred`端点。
*   验证令牌是否有效，通过从 JWT 有效负载中解码用户 id 来找到用户 id。
*   使用用户 id 获取引用代码，然后查找 referrer 字段与`referralCode`匹配的所有集合。

但是我们如何验证头中传递的 JWT 呢？简单来说，我们需要调用存在于`jsonwebtoken`模块中的`verify` API，因为我们使用了`sign` API。让我们继续实现用于验证访问令牌的中间件。

在 middlewares 文件夹中，创建一个名为`validateToken.js`的文件

这是验证 JWT 令牌的一种更安全的方式。我们不只是验证令牌，而是对照我们的白名单(在数据库中)进行检查。

现在，让我们定义控制器来获取所有引用的帐户。

然后，我们必须将端点添加到我们的路由器。在`routes/users.js`文件中，导入`validateToken`中间件，并在新创建的端点中使用它。

```
**const { validateToken } = require(“../middlewares/validateToken”);** const AuthController = require(“../src/users/user.controller”);
router.post(“/signup”, cleanBody, AuthController.Signup);...
...**router.get(“/referred”, validateToken, AuthController.ReferredAccounts);**
```

更新文件后，让我们测试我们的端点。

![](img/2840f48f0a1a40c7f4a89a6f618c6b2f.png)

我们的中间件抛出错误`Access token is missing`。让我们通过传递一个随机令牌作为标头来测试。

![](img/76caa20f4da1d39ef7031f4165b40e92.png)

有用！现在让我们登录以获得一个有效的访问令牌。

![](img/db2852a922ac3e30de32d1694bef71cd.png)

现在让我们在`Authorization header`中传递这个访问令牌作为`Bearer`令牌。

![](img/b9be548ac37b0cc0fc853ad6f78d17f8.png)

嘣！我们得到了所有使用我们的推荐代码注册的账户。因此，使用 JSON Web 令牌，我们可以保护尽可能多的端点，就像我们对 `GET /referred`端点所做的那样。

现在，让我们定义注销用户的控制器和端点。用户注销控制器很简单。我们只需要从数据库中清除访问令牌就行了。

它还是一个受保护的端点，只有拥有有效访问令牌的登录用户才能注销。

在将注销端点添加到我们的`routes/users.js file`之后，它将看起来像这样。

最后，让我们检查注销端点。

![](img/aa6c9cdb9ffc3a342f648afb29128bcd.png)

让我们尝试使用相同的令牌获取引用的帐户。

![](img/f886123691fd7b1253f4c8540a93c425.png)

太好了！它像预期的那样工作。如果检查用户的集合，访问令牌将从用户文档中清除。因此，我们已经成功地(**和安全地**)将 JWT 集成到我们的认证系统中。

你可以在这个 [GitHub 库](https://github.com/PraneshASP/node-authentication-jwt-mongodb)中找到完整的源代码。

## **结论**

在这个现代网络时代，没有什么叫做“这是正确的方法”来实现一个特性。根据需求的不同，它会因系统而异。所以，让我们每天都探索和学习新的东西吧！

如果你对这篇文章有任何疑问，我随时欢迎讨论。

感谢阅读！