# 如何用 Fastify 构建可靠的认证 API

> 原文：<https://javascript.plainenglish.io/how-to-build-a-reliable-authentication-api-with-fastify-c5a24bf8cd41?source=collection_archive---------6----------------------->

## Web 开发|认证

## 使用这个新的 Node.js 框架构建可靠的 Auth API

![](img/5ce1c02ba38324cfd7be8d0758958fea.png)

[Image By Jexo on Unsplash](https://unsplash.com/photos/044AnorPjAU)

在 web 开发中，我一直在与身份验证作斗争。我讨厌构建这些 API，但是现在，[有了 Fastify](https://github.com/fastify/fastify) ，我实际上非常喜欢它。有了这个快速简洁的 JavaScript 框架，我们将构建一个带有 MongoDB 连接的身份验证 API。

# 什么是 Fastify？

Fastify 是 Node.js 的一个高效的 web 框架[，它专注于](https://github.com/fastify/fastify)开发人员的便利。这个框架不仅速度快，而且还附带了一个高级且非常易于使用的插件系统。

# 要求

如果你想开始使用 Fastify，你需要做一些准备:

*   [Node.js](https://nodejs.org/en/)
*   [NPM](https://www.npmjs.com/)
*   NPM 软件包(我们稍后会谈到)

# 入门指南

要初始化节点项目，请在终端中输入以下代码行:

```
> npm init -y
```

这将为您设置一个节点环境。现在，我们将安装 Fastify 所需的软件包/模块:

```
> npm i bcryptjs fastify fastify-auth fastify-plugin jsonwebtoken mongoose nodemon
```

在我们的`package.json`中，我们添加了以下脚本:

我们调用我们的主文件:`server.js`

# 设置 Fastify 服务器

如果你熟悉 node 和 express，也许你知道我们要设置一个 web 服务器，有了 Fastify，这是非常容易的。

这将运行我们的 web 服务器。在你的终端输入`npm run dev`启动服务器。

# 创建用户模型

创建用户模型允许我们创建一个结构来保存用户数据。如果你想了解更多关于[编程模型的知识，请点击这个链接。](https://en.wikipedia.org/wiki/Programming_model#:~:text=A%20programming%20model%20refers%20to,Threads%20library%20and%20Hadoop's%20MapReduce.&text=In%20parallel%20computing%2C%20the%20execution,order%20to%20achieve%20high%20performance)如果你对你应该知道的编程概念感兴趣，我推荐你这篇文章:

[](https://levelup.gitconnected.com/5-critical-coding-concepts-that-will-move-you-from-a-beginner-to-an-intermediate-programmer-c94670a564c8) [## 5 个关键的编码概念将帮助你从初学者成为中级程序员

### 编程不仅仅是“你好，世界”和斐波那契

levelup.gitconnected.com](https://levelup.gitconnected.com/5-critical-coding-concepts-that-will-move-you-from-a-beginner-to-an-intermediate-programmer-c94670a564c8) 

为了创建一个用户模型，我们创建一个名为`models`的新文件夹，并添加一个名为`User.js`的文件:

这为我们的用户数据设置了一个容器。我们还需要验证它是否已经在我们的数据库中，并且我们需要导出模型。这将完成 User.js 类:

# 设置我们的路线

创建我们的路线分为两部分:

*   设置 Fastify 身份验证
*   设置路线

我们需要创建一个新的`routes`文件夹并添加一个`Users.js`文件，然后导入模块和我们的模型。接下来是路由功能和授权设置:

这两种方法验证令牌以及用户名和密码，它还将检查给定的用户名是否已经在数据库中注册。尽管如此，我们将在下一节讨论我们的数据库。

使用以下代码注册路线，创建一个新的`User`对象，并将其存储在我们的 MongoDB 数据库中:

# 建立与 MongoDB 的连接

当我们设置好路由后，您可能会注意到我们在数据库中`.save()`了它，但是连接还没有建立。我们现在就去做。用`index.js`文件创建一个`config`文件夹，输入以下代码:

这将使我们的 API 工作。最后要做的事情是`server.js`必须连接到这 3 个文件。我们使用`dotenv`来获取我们的连接字符串，就像我们使用`dotenv`来获取我们的秘密令牌一样。

# 测试我们的 API

为了测试 API，我使用了一个名为 [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) 的 visual studio 代码扩展。这个插件允许你用你的 HTTP 请求创建一个测试文件。让我们创建一个名为`test.http`的。

我们要调用的第一条路线是`Register`路线:

当我们运行时，您将看到您成功地创建了一个新用户。让我们尝试检索该用户。首先复制您收到的令牌，然后创建一个新请求:

当一切都设置正确后，您将收到您刚刚创建的用户。让我们尝试注销:

如果您想再次登录:

你会得到一个新的令牌。

瞧啊。您已经有了一个有效的身份验证 API。

如果你对更多关于认证的解释感兴趣，看看 David F 的这个精彩故事，他向你解释了如何使用 NextAuth:

[](https://davidfrnks7.medium.com/authenticate-users-with-nextauth-2e7aa6f050a) [## 使用 NextAuth 验证用户

### NextAuth 是 Next.js 应用程序的开源身份验证提供者。它是为无服务器应用程序而构建的，非常…

davidfrnks7.medium.com](https://davidfrnks7.medium.com/authenticate-users-with-nextauth-2e7aa6f050a) 

如果你喜欢我的文章，你可以在这里注册我的免费邮箱。

[](https://bryandijkh.medium.com/membership) [## 通过我的推荐链接加入媒体——布莱恩·迪克伊岑

### 阅读布莱恩·迪克伊岑(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接…

bryandijkh.medium.com](https://bryandijkh.medium.com/membership) 

# 参考资料和来源

*   [https://www.fastify.io/](https://www.fastify.io/)
*   https://www.fastify.io/docs/latest/Getting-Started/
*   【https://github.com/fastify/fastify-jwt 
*   [https://daily.dev/blog/fastify-authentication-strategy](https://daily.dev/blog/fastify-authentication-strategy)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)