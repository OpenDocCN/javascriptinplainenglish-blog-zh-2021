# 如何使用 JWT 和 Node.js 创建认证系统

> 原文：<https://javascript.plainenglish.io/authentication-systems-using-jwt-and-node-js-9c3cc14aaf82?source=collection_archive---------0----------------------->

![](img/146eb493a995c643777945fab862c066.png)

## 本教程简介

在本教程中，您将了解如何在 Node.js 中使用 JSON Web 令牌(JWT)来验证用户身份。如果你对 JWT 不熟悉，你可以点击这里的链接——这用许多有趣的例子解释了 JWT 的一切。

在本教程中，我们将使用 Node.js 为注册、登录和注销创建 API。首先，让我们回忆一下 JWT 的基础知识。

JW 令牌由 3 部分组成:

## 1.页眉

报头包括用于生成令牌的算法类型。看起来是这样的:

```
{
 “alg”: “HS256”,
 “typ”: “JWT”
}
```

## 2.**有效载荷**

有效负载就是用户数据。

```
{
 “id”:”920021",
 “name”: “Krishna”
}
```

## 3.**签名**

签名是由服务器生成的密钥。

这三个部分组合起来就形成了一个 JW 令牌，看起来有点像这样:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjkyMDAyMSIsIm5hbWUiOiJLcmlzaG5hIn0.tvORZ0xRXmRhVB_sYnckoEN8HYe-q4YUlZJ-ZNaWBiM
```

首先，要完成本教程，我们需要以下内容:

1.  **Postman:** 用作 API 客户端来创建或测试 API。
2.  **npm** :您的系统中必须安装节点程序包管理器(npm)。
3.  **Node.js:** Node.js 是用来构建可伸缩应用的平台。

现在，让我们创建一个 Node.js 项目。

创建 Node.js 项目的第一步是生成一个 **package.json** 文件。使用以下命令:

```
npm init
```

现在您需要安装所需的依赖项:

```
npm install express
npm install jsonwebtoken
npm install nodemon 
```

创建一个 **index.js** 文件，它是项目的主文件。检查您的项目结构是否如下图所示:

![](img/a7596eb4c7ea69cbd887ac473cf9751a.png)

现在，打开 **index.js** 文件，使用下面的代码导入所有的包或依赖项:

```
const express = require('express');const app = express();const jwt = require('jsonwebtoken');
```

让我们测试这个项目。创建一个简单的 GET API，检查是否一切都按预期运行。使用下面的代码:

```
app.get('/api/testing', (req,res) => {res.send('Hello Developer!')})app.listen(9999,() => console.log('Server is Up and Running'));
```

现在，要测试这个 API，您需要使用以下命令运行项目:

```
nodemon
```

打开 Postman 并添加以下 URL:

[http://localhost:9999/API/测试](http://localhost:9999/api/testing)

> 注意:验证你是否向邮递员发出了 GET 请求。

你的成功回应应该是这样的:

*开发者您好！*

现在，让我们为注册创建一个 API。

1.  注册 API 从客户端获取用户名和密码凭证。
2.  此外，它还为该数据或有效载荷生成一个 JW 令牌。这里，我们将为这个特定的用户 id 创建一个令牌。然后，这个令牌被发送回客户端。

## *注册 API*

```
app.post('/api/signup' , (req,res) => {const id  = req.body.id;const username = req.body.username;const password = req.body.password; jwt.sign(id , 'secret_key' , (err,token) => {if(err){res.status(400).send({msg : 'Error'})}else{res.send({msg:'success' , token: token})}})})
```

> **注意:**在这里，我们不打算将数据保存到数据库中，因为我们希望更专注于理解 JWT 概念。

一旦运行了这段代码，Postman 的响应将如下所示:

**响应**

```
{"msg": "success","token":"eyJhbGciOiJIUzI1NiJ9.MQ.gaKRuIIRNvXiTlyNPE1Kp3SpAQfhrI3r9MrSB1YdMz8"}
```

响应返回一个带有 JW 令牌的成功消息，该令牌经过加密，还带有报头、数据(id)和签名。现在，这个令牌将帮助用户发出对受保护路由的每个请求。

现在，让我们继续登录 API。

在我们创建登录 API 之前，我们需要创建一个**中间件**函数来验证从客户端发送到服务器端的令牌。

> **注意:**中间件函数是可以访问请求对象、响应对象以及应用程序的请求-响应周期中的下一个函数的函数。

```
function verifyToken(req, res, next) {const authHeader = req.headers["authorization"];const token = authHeader && authHeader.split(" ")[1];if (token == null) return res.sendStatus(403);jwt.verify(token, "secret_key", (err, user) => {if (err) return res.sendStatus(404);req.user = user;next();});}
```

这个中间件功能将帮助我们验证在每个受保护的路由请求上从客户端传递到服务器端的令牌。我们可以在我们的 API 中使用这个中间件，只需将它作为一个参数添加到 API 端点和回调函数之间。

## 登录 API

```
app.post('/api/login' , verifyToken , (req,res) => {res.send('You are Authorized!')})
```

发送响应的技巧如下。如果你向邮递员请求这个 API，它肯定会给出一个错误——*403 未授权*。这就是我们在 API 中使用中间件的原因。现在，要使用这个受保护的路由，您必须在 Postman 中设置头。

> **注意:**要设置标题，请转到标题选项，添加一个值为“无记名<令牌>的密钥“授权”。查看下图。

![](img/9fa5a936b2e04d06301f0884dbc2d41d.png)

单击左边的框，检查并发送登录请求。它应该用*回应“你被授权了。”*

## 注销 API

现在，我们必须创建注销 API。

为了创建注销 API，我们必须首先检查请求是否有效，然后对请求做出响应。这里，重要的一步是注销用户，在后台，我们必须从标题中删除 JWT 令牌。但是不幸的是，我们没有任何这样的选项来删除头中的 JWT 令牌。因此，我们将用一个将在 1 秒后过期的空字符串替换 JWT 令牌。其代码如下所示:

```
app.put("/api/logout", authToken, function (req, res) {const authHeader = req.headers["authorization"];jwt.sign(authHeader, "", { expiresIn: 1 } , (logout, err) => {if (logout) {res.send({msg : 'You have been Logged Out' });} else {res.send({msg:'Error'});}});});
```

只有当您通过添加带有报头的 JW 令牌来发送请求时，此 API 才会起作用，其响应如下:

```
{"msg": "You have been Logged Out"}
```

在这里，我们已经成功地建立了一个授权系统，我希望你们都知道 JWT 是如何运作的。谢谢你，祝你愉快！