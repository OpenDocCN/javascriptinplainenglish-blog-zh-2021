# 如何用 Node.js，Express，MongoDB 制作 REST API

> 原文：<https://javascript.plainenglish.io/how-to-make-rest-api-with-node-js-express-and-mongodb-dfce5e70e830?source=collection_archive---------6----------------------->

# 第一部分。服务器连接设置

在这篇文章中，您将了解什么是 REST API，并学习如何使用 MongoDB Atlas 在 Node.js 中为 API 设置连接。

![](img/dc10744fee934062798e2a529ee7a32e.png)

By: umang

## 首先，什么是 Restful API？

REST(**RE**presentational**S**tate**T**transfer)是一种架构风格或模式，它定义了开发 web 应用程序的约束集。Restful APIs 是一种以更简单的方式访问数据或服务的方式。

当向端点发出请求时，它将资源状态的表示传输到端点，并以下列格式之一返回响应: ***JSON(最常用)*、HTML、PHP、Xlt 或简单文本。**

## **什么使得 API 是 Restful 的？**

*   它不应该在服务器上存储客户端的信息。
*   通过 http 管理请求的客户机-服务器体系结构。

![](img/7461e5a716c55b0166e8a82a50e108e0.png)

[https://www.altexsoft.com/blog/rest-api-design/](https://www.altexsoft.com/blog/rest-api-design/)

# **启动前的要求**

*   您首选的 [**IDE**](https://www.codecademy.com/articles/what-is-an-ide) (VSCode、Atom 等)
*   Node.js 已安装(通过在终端中键入 ***node -v*** 进行检查)
*   PC 上的 MongoDB 或者 [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) (设置你的账号，做一个集群)，后者优先。
*   API 测试工具，如 [Postman](https://www.postman.com/) 或[这些替代品](https://rapidapi.com/blog/best-api-testing-tools/)中的任何一个。

首先，我们将初始化 Node.js 项目。要进行初始化，请为项目创建一个新文件夹，并在 VSCode 中打开该文件夹，然后在终端中键入以下命令:

```
npm init (and follow the process)
or
npm init --yes (put this flag to make project with default setting)
```

![](img/b9cd968364af5aec11caf41b27eb0942.png)

现在您将能够在文件夹中看到 **package.json** 文件。转到该文件并更改几行代码:

```
1\. "main": "server.js",2\. "scripts": { "start": "nodemon server.js" }
```

现在转到终端，通过编写以下代码安装一些依赖项:

```
npm install express nodemon cors body-parser mongoose dotenv
```

所有的依赖项都是必要的，我会在我们前进的时候告诉他们的用法。 ***nodemon*** 会在代码更改后自动重启你的服务器。

1.  制造。我们将从这里获取我们的密钥、密码和端口号，这样其他人就不能访问它(不要在 GitHub 上推送这个文件)。在。环境文件:

```
PORT = 5000
```

2.现在，在同一个目录下创建一个 **server.js** 文件，并编写下面的代码来创建我们的服务器:

```
const http = require('http')
const app = require('./app')
const port = process.env.PORT || 3000
const server = http.createServer(app)
server.listen(port)
```

3.使 **app.js** 在同一个目录下。在这里，我们将定义 API 的基本路径，并连接到我们的 MongoDB 数据库。您可以将该文件视为 API 文件的主要入口。现在开始编写该文件中的代码:

```
const express = require('express')
const app = express()
const cors = require('cors')
const bodyParser = require('body-parser')  
const mongoose = require('mongoose')
require('dotenv/config')
```

> 注意: **Body-parser** 是一个*中间件*用于解析即将到来的请求**的主体，dotenv** 用于获取 env 变量， **cors** 也是一个用于启用 cors 的中间件， **mongoose** 是 mongodb 和 nodejs 的对象数据建模库。它管理数据之间的关系，提供模式验证，并用于在代码中的对象和 MongoDB 中这些对象的表示之间进行转换… [🔗](https://www.freecodecamp.org/news/introduction-to-mongoose-for-mongodb-d2a7aa593c57/)

现在，要连接 MongoDB，请转到您的 MongoDB Atlas 集群，获取数据库连接代码并将其粘贴到 **dotenv** 文件中，如下所示:

```
DB_CONNECTION = mongodb+srv://**Yourname**:[**password**@cluster0.pi2rv.mongodb.net](mailto:1234@cluster0.pi2rv.mongodb.net)/**dbname**?retryWrites=true&w=majorityNote: Replace all the bold word respectively:
your username (**umang**)
password (**1234**)
Database name (**Shop**)
```

![](img/624ee008417ee8772cb8941d3cfcfdd6.png)

现在，转到 app.js，编写与数据库连接的代码，并完成连接设置。

```
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));# Defining all the http header and the request options
app.use((req, res, next) => {
res.header('Access-Control-Allow-Origin', '*');
res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept, Authorization');
if (req.method === 'OPTIONS') {
     res.header('Access-Control-Allow-Methods', 'PUT, POST, GET,   PATCH, DELETE')
return res.status(200).json({})
}
next();
});mongoose.connect(
          process.env.DB_CONNECTION, 
         {useNewUrlParser: true, useUnifiedTopology: true },
         () => {
             console.log('connected to database')
         })
mongoose.Promise = global.Promiseapp.use((req, res, next) => {
   res.status(200).json({message: "It works"});
})
```

现在我们的设置已经完成，转到 vscode 中的终端并键入

```
nodemon server.js 
// it will run a server and database connection will be made
```

> 通过进入 [http://localhost:5000](http://localhost:5000) 进行测试。它应该会回复“它工作了”。

## 万岁！您已经在 Node.js、Express 和 MongoDB 中完成了 REST API 的基本连接设置。

被一个错误卡住了？没问题！留下评论，我一定会努力解决。否则，在 25umangagarwal@gmail.com 给我发邮件或者在 [*LinkedIn*](https://www.linkedin.com/in/umang-agrawal07/) 上联系我。

# 第二部分。为/get 请求创建 API 端点

[](https://25umangagarwal.medium.com/making-api-endpoints-for-rest-api-in-nodejs-ec688c18aaa) [## 在 NodeJS 中为 REST-API 创建 API 端点。

### 第 2 部分—创建 API 端点来发布或检索数据。

25umangagarwal.medium.com](https://25umangagarwal.medium.com/making-api-endpoints-for-rest-api-in-nodejs-ec688c18aaa) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)