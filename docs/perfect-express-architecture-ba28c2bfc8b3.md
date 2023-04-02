# 完美快递架构

> 原文：<https://javascript.plainenglish.io/perfect-express-architecture-ba28c2bfc8b3?source=collection_archive---------6----------------------->

Express 的可扩展且易于理解的体系结构。

![](img/1f2e0f141043e8c8709d6c4389365537.png)

Photo by [jose aljovin](https://unsplash.com/@josealjovin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 在后台

同样的故事，一遍又一遍，😁，我目前正在运行一个概念，或者说是一个想法，编写一次，随时随地使用逻辑或代码。到目前为止，其他开发人员已经创建、形成并重用了大量代码库。您可以在下面的链接中找到这些代码库。

```
[**iHateReading Code Repos**](www.ihatereading.in/repos)
```

## 概观

在今天的故事中，我们将创建 Express JS 框架库，并遵循创建可伸缩且易于理解的架构的概念。

在我们开始之前，第一步也是最重要的一步是下载 Express framework 中最常用的包。

```
yarn add express body-parser dotenv nodemon axios
```

*   正文解析器—解析请求正文
*   dotenv —读取 env 文件
*   nodemon —查看实时变化
*   axios —进行 API 调用

## 创建路线

每个端点称为一个路由，每个路由都放在根目录的一个文件夹中。不要在单个 route.js 文件中添加所有端点路由，而是根据它们的逻辑将它们解耦，这是一个很好的做法。

例如，身份验证将具有端点，所有端点(如登录、注册和重置密码)都可以在 routes 文件夹的 authentication.js 中定义。类似地，我们可以为我们的服务器将提供的每项服务创建分段路由。

```
-routes
 -authentication
```

## 创建控制器

控制器是每个路由的方法或回调。它们是从客户端调用每个端点时执行的业务逻辑。例如，假设客户端使用其电子邮件和密码对端点`/login`进行服务器调用，验证用户真实性的整个认证逻辑将只在控制器内部编写。

## 控制器架构

我经常发现将控制器按照它所服务的服务进行命名是一个很好的做法。例如，登录、签名和重置密码方法可以在身份验证控制器中定义。

```
-controllers
 -authentication
   -login.js
   -register.js
   -reset-password.js
```

## 定义模式

嗯，大多数时候你会在 REST API 中使用 ORM 层。因此，无论使用什么数据库，定义模式都是绝对必要的。我总是喜欢用一个完全不同的模式文件夹来定义模式。这使得集成第三方模式定义库(如 mongoose)变得很容易。

类似地，您可以像 controller 和 routes 一样在根目录中创建一个名为`models`的新文件夹。这将包含您将在数据库中创建的每个集合或表记录的所有模式。

```
-models
 -user.js
 -product.js
```

## 环境文件

每次都需要处理 env 文件，所以我建议安装 dotenv npm 模块，以便在节点应用程序中轻松处理 env 文件。

您将需要 env 来定义数据库 URL、应用程序的节点环境、用于部署、开发和生产的服务器端口。所以使用 env 是不可避免的，这是 dotenv 最初安装的。

## 静态文件

对于某些应用程序，您需要处理静态文件，如 HTML、CSS 或图像。Node JS 自带完善的第三方支持，比如 Mustache 等等，可以处理所有静态文件。

放置所有静态文件的传统方法是在根目录的视图目录中。所以最好遵循相同的常规规则来处理静态文件，当然，您可以在将来相应地更改它。

```
view
 -styles.css
 -index.html
```

## 测试目录

编写测试用例总是成为 node js 应用程序的低优先级，但我确实建议编写测试用例，因为它们有助于提供更好的服务，并覆盖人类无法覆盖的边缘情况。

为了编写测试用例，你可以简单地在根目录下创建一个名为`tests`的文件夹，并在其中定义所有的测试用例。同样，这是我在 chai 和 mocha 的文档中读到的传统方法，chai 和 mocha 是 Node JS 应用程序编写测试用例的 npm 模块。

```
-tests
 -userTest.js
```

## 结论

您可以在下面的链接中找到最终的资源库。我没有详细介绍很多故事，因为这只是为了对 perfect express 架构有一个基本的了解，而不是深入细节。

```
[**Click to reach the code repository**](https://github.com/shreyvijayvargiya/iHateReadingLogs/tree/main/TechLogsBackend/ExpressBasicSetup)
```

直到，下一次，有一个美好的一天，人们。

```
For more such stories visit our website - 💻 [**iHateReading**](http://www.ihatereading.in)
```

## 更多阅读

[](https://medium.com/nerd-for-tech/5-reasons-why-vercel-is-the-best-for-application-deployment-92009b17e601) [## Vercel 最适合应用部署的 5 个原因

### 无论是 React project 还是 Gatsby 还是 Next JS 或者 Vue JS 或者 Nuxt JS 或者 Nest JS 或者 Node JS Vercel 都是完美的选择…

medium.com](https://medium.com/nerd-for-tech/5-reasons-why-vercel-is-the-best-for-application-deployment-92009b17e601) [](https://medium.com/geekculture/13-steps-for-perfect-authentication-flow-in-backend-4fad7dce0e0) [## 后端完美认证流程的 13 个步骤

### 我把我的应用服务器当作一个俱乐部聚会，只需 13 个步骤就能开发出完美的认证流程

medium.com](https://medium.com/geekculture/13-steps-for-perfect-authentication-flow-in-backend-4fad7dce0e0) 

*更多内容看* [***说白了. io***](http://plainenglish.io/)