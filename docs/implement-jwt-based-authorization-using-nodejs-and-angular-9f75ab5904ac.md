# 使用 NodeJS 和 Angular 实现基于 JWT 的授权

> 原文：<https://javascript.plainenglish.io/implement-jwt-based-authorization-using-nodejs-and-angular-9f75ab5904ac?source=collection_archive---------8----------------------->

## 如何使用 NodeJS，MySQL 创建 JWT 授权的完整示例，并使用 Angular

![](img/b66ea60350cf5370a1165f01d2d40b68.png)

基于 JWT 的授权主要用于管理用户会话。

# **我们今天面临的用户会话问题是什么？**

为了开发一个 web 应用程序，我们正在使用各种现代前端框架，如 **Angular、React、Vue** 等。它们是独立的框架。它们不依赖于特定的服务器技术。他们将使用 Ajax 请求从服务器获取数据。以前，如果你用 Java、PHP 和 T4 开发 web 应用程序。NET ，HTML 代码混合了相应的服务器端代码(PHP，JSP，Servlet，ASP)。所有代码仅从服务器呈现。因此用户会话在服务器端得到了有效的处理。服务器将处理会话验证和会话到期。

但是现在我们使用无状态 Ajax 请求从服务器获取数据。所以我们必须处理**用户** **会话** **验证**和会话**到期**。我们可以通过使用用户名和密码来验证用户。一旦登录，我们不能要求用户输入用户名和密码来查看每个页面/请求。

您可以考虑使用某个**随机唯一键**，并在每次用户请求到达服务器时验证随机唯一键。但是如果处理大量用户，这种方法会增加服务器的负载，因为每次都要检查数据库中的键。并且不验证随机唯一密钥是否来自授权人员。如果我们没有授权，任何人都可以发送密钥来检查服务器。为了对用户请求进行授权，我们可以使用 JWT。有许多可用的场景。我在这里只解释了一种情况。

# **什么是 JWT？**

JSON Web Token ( **JWT** )作为一个 JSON 对象，用于在各方(客户机和服务器)之间安全地传输信息。

JWT。IO 允许您解码、验证和生成 JWT 令牌。

![](img/ce6b3370fbab1c4dc658ebfb6aae7028.png)

我将简单地解释它是如何工作的。假设用户登录成功后，我们有了一个 user-id。

```
{user_id:'KL00456'}
```

现在，我们可以使用私钥加密用户信息。下面给出了私钥。

```
dvRZbtaVDXu34h0STl9yE4HE4hA3gR
```

私钥的长度由您选择。你可以使用任何长度。这里我使用了 30 个随机字符作为我的私钥。现在，我们可以使用私钥加密用户信息，并将它发送到客户端(浏览器/移动应用程序)。JWT 加密密钥(令牌)如下所示。

```
eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoiS0wwMDQ1NiIsImlhdCI6MTYxMTY1MzY3NCwiZXhwIjoxNjExNjUzNzA0fQ.xCive3xHx2bkHjhJCCULZpLKgJQ9j7yiwyH7nxNt5Q-yJpKTHpWqA3G8PofyLwXLXxOcTPL1lRhe7oJtIre0RQ
```

上述令牌将存储在客户端。当用户访问每个页面时，上述令牌将被发送到服务器。然后，服务器将使用用于生成 JWT 令牌的私钥来验证令牌。如果它是一个有效的令牌，那么我们能够从令牌中解包用户 id，并将相应的数据发送到浏览器。如果它不是一个有效的令牌，那么我们可以很容易地提示用户重新登录。

> 现在你可以问我，有没有可能不解密就从 token 查看数据？。

答案是“**是**”。

是的，我们可以查看 JWT 令牌中的数据。但是，如果不使用私钥，我们就无法验证它。所以验证是重要的一步。现在每个人心里都会产生一个疑问。

> 如果我们不用解密就能看到信息，那么这个 JWT 令牌是如何安全的呢？。

仅为授权目的创建的 JWT 令牌。这是一种新的产品封箱(JWT)。如果密封没有被破坏，我们可以确保没有人打开/修改这个盒子，也没有其他额外的物品插入盒子。我们无法修改令牌信息。如果您修改它，那么它将在验证中失败。因此，这确保了只有服务器可以发布有效的授权令牌，并且只有有效的客户端才能通过与服务器交换该令牌来获取数据。

现在我们将看到如何使用 NodeJS 实现 JWT 令牌。

# **安装 JWT**

互联网上有许多 JWT 图书馆。这里我们将使用 **jsonwebtoken** 包。我将使用 **NodeJS** 展示演示。你可以使用任何其他语言。但是请查看 JWT 官方网站，以获得其他编程语言的正确 JWT 软件包。

如果您不知道如何使用 NodeJS 创建 REST API，请访问下面的链接来学习。

[](https://medium.com/javascript-in-plain-english/create-rest-api-using-nodejs-and-mysql-from-scratch-d1844601e21) [## 从头开始使用 NodeJS 和 MySQL 创建 REST API

### 从头开始使用 MySQL 的 CRUD 示例

medium.com](https://medium.com/javascript-in-plain-english/create-rest-api-using-nodejs-and-mysql-from-scratch-d1844601e21) 

在 nodejs 项目中使用下面的命令安装 **jsonwebtoken** 。

```
npm install jsonwebtoken
```

# **加密 JWT**

现在，我们将了解如何在服务器端使用 JWT 加密数据。

**第 1 行:**首先导入 jsonwebtoken 包。
**第 2 行:**定义你的私钥。
**第 3 行:**从 JWT 调用 sign()函数生成令牌。它需要三个参数。
**第一个参数** = >用户信息作为 JSON 对象。
**第二个参数** = >私钥。
**第三个参数** = >加密和定义令牌过期时间的算法。

将上述代码保存在名为 **jwt-encrypt.js.** 的文件中，并使用下面的命令执行该文件。

```
node jwt-encrypt.js
```

上面的命令将输出一个加密的 JWT 令牌。

# **解密 JWT**

在上面的例子中，JWT 令牌是在服务器端生成的，并将被发送到客户端。现在，我们将验证生成的令牌。

**第 1 行:**导入 jwt 包。
**第 2 行:**用于生成 JWT 令牌的相同私钥。
**第 3 行:**JWT 令牌来自客户端。
**第 4 行:**从 JWT 调用 verify()函数，传递上述数据。如果它是一个有效的令牌，它将向用户提供信息。否则它将抛出一个异常。如果抛出异常，那么它就不是有效的令牌。

将上述代码保存在名为 **jwt-decrypt.js.** 的文件中，并使用下面的命令执行该文件。

```
node jwt-decrypt.js
```

如果是有效的令牌，上面的命令将输出用户信息，如下所示。

```
{ user_id: 'KL00456', iat: 1611724265, exp: 1611724395 }
```

# **登录示例**

到目前为止，我们已经看到了如何生成令牌并使用 JWT 验证令牌。现在我们将使用带有 **Angular** 的登录示例来看看如何实时实现这个 JWT 授权。下面列出了我们要做的步骤。

1.  在 MySQL 中创建一个表并存储用户名和密码。
2.  创建一个 NodeJS API 来验证用户名和密码，并生成 JWT 令牌。
3.  创建一个 NodeJS API 来验证 JWT 令牌。
4.  在 Angular 中创建一个登录页面，调用 NodeJS 认证 API。
5.  成功登录后，转到主页，将 JWT 令牌发送到服务器进行验证。如果验证成功，则显示主页，否则显示登录页面

# **在 MySQL 中创建表格**

使用下面的命令创建一个表。

使用下面的命令在表中保存用户名和密码。

> 注意:不要将纯文本存储为密码。始终加密密码并保存。举个例子，我用它作为纯文本。

# **验证登录并创建 JWT 令牌 API**

在 server.js 文件中使用下面的代码。

**第 32 行& 34:** 捕捉用户名和密码并使用。

**第 33 行:**检查数据库中的用户名和密码。

**第 42 行:**使用用户 id 生成令牌。

# **验证 JWT 令牌 API:**

第 3 行:从客户端接收令牌。

**第 7 行:**使用私钥验证令牌。

**第 13 行:**将授权状态传递给客户端。

# **带角度的实现**

## **创建登录页面**

创建一个名为 login 的组件，并将下面的代码粘贴到 HTML 文件中，以创建一个登录页面。将登录设为路由中的默认页面。

使用 login.ts 文件中的按钮 click 事件将用户名和密码传递给服务器 api。

成功登录后，接收令牌并将其保存在本地存储中，然后转到主页。

现在，在 home.component.ts 文件中，将令牌传递给服务器进行验证。您可以使用 Angular 中的 AuthGuard 来实现这一点。然而，为了简单起见，我将它与 ngOnInit()函数一起使用。

**完整源代码:**

```
[https://github.com/bharathirajatut/angular-examples/tree/master/jwt-implementation](https://github.com/bharathirajatut/angular-examples/tree/master/jwt-implementation)
```

# **总结**

在本教程中，您学习了如何使用 NodeJS 从头开始实现 JWT 授权。并使用 Angular 框架创建了一个简单的登录和注销示例。身份验证和授权是任何应用程序的一个非常重要的部分。许多初学者在开发应用程序时未能实现授权。开发人员需要更加关注安全性。为什么？因为今天我们使用应用程序完成大部分活动。应用简化了我们的工作和生活方式。它在很多方面帮助了我们。然而，我们必须意识到应用程序的安全缺陷。

这是 JWT 从无到有的完整实现。然而，我们需要做一些修改，使其更符合行业标准。我会在另一篇文章中写下缺失的部分，以及如何让它变得更好。

敬请关注更多文章。

**感谢您的阅读。**

JWT 令牌包链接

[](https://github.com/auth0/node-jsonwebtoken) [## auth0/node-jsonwebtoken

### JSON Web 令牌的实现。这是针对 draft-IETF-oauth-JSON-we B- token-08 开发的…

github.com](https://github.com/auth0/node-jsonwebtoken)