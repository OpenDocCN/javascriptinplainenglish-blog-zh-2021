# 如何用 Node.js 和 Express 设置简单的 API

> 原文：<https://javascript.plainenglish.io/how-to-set-up-a-simple-api-with-node-js-and-express-1d7c13afc7cc?source=collection_archive---------4----------------------->

## 想学习一个新的后端，但不知道从哪里开始？按照步骤建立一个基本的 Node.js/Express API(包括路由和处理请求/响应)！

![](img/6476f7527a54f5e4668037b5dd0ff6f4.png)

Photo by [Matt Lee](https://unsplash.com/@mattlee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 目录

1.  [简介](#a851)
2.  [早步骤](#ae58)
3.  [基本设置](#9b84)
4.  [增加路线](#2215)
    [加成！外部抓取](#7a9f)
5.  [结论](#b80f)
6.  [想要更多？查看其他资源！](#1d0d)

# 简介**💪**

最近，我集中精力复习基础知识，深化我在训练营中学到的知识，以便学习新的东西。然而，这次我决定休息一下，挑战自己，学习一些新的东西与大家分享！今天我们将学习建立一个简单的 Node.js/Express API 的基础知识。

如果你懂 JavaScript，不管是因为你已经用普通 JavaScript 还是 React 构建了你的前端，那么我推荐你用 Node.js 探索一个后端，并学习 Express 作为后端框架。虽然我不会详细介绍 Express 是什么，但如果你想了解更多，请查看 Tomislav Capan 的这篇文章或这段视频:

现在，让我们来看看如何设置一个基本的 Node.js/Express API！在你离开之前，如果你是一个视觉型的人，想看看成品是什么样子，请注意，在任何时候你都可以参考[结论](#b80f)。

# 早期步骤**🐣**

开始之前，我们需要先做三件事:

1.  通过运行以下命令，确保安装了 node。

```
node --version
npm —-version
```

如果没有，请在此导航[并下载最稳定的版本。您也可以下载最新版本，但要注意它可能包含一些将来可能会被删除的错误和功能。](https://nodejs.org/en/download/)

2.在您的本地计算机上创建一个新的项目目录(文件夹)。

```
mkdir <new-project-name>
```

3.进入那个文件夹

```
cd <new-project-name>
```

# **基本设置🏃‍♀️**

现在，您已经安装了 node 和 npm，并创建了存放该项目的地方，我们可以开始了！

1.  在项目文件夹中，在终端中使用以下命令将其初始化为节点项目。

```
npm init
```

接下来，终端将提示您希望如何初始化它(例如，您可以将入口点从 **index.js** 更改为 **app.js** )，否则您可以继续单击 enter 键。这将在项目的根目录下生成一个 package.json 文件，其中包含关于您的项目的信息。

另外，如果您添加了`-y`标志，您也可以跳过提示符，让它创建一个默认的 package.json 文件！

2.将快速模块作为依赖项安装到:

```
npm install express --save
```

然后您会看到, **node_modules** 文件夹是用 express 需要的所有东西创建的。

**有趣的事实**: `—-save`标志确保将其保存为 package.json 中的一个依赖项

3.接下来，你还需要安装 nodemon，这样我们就不需要每次做出改变时都重启应用程序。因为我们只在开发时需要它，所以添加 `—-save-dev`标志将其定义为开发依赖:

```
npm install --save-dev nodemon
```

4.在代码编辑器中打开项目，并导航到 **package.json** 。通过添加以下行来更改脚本:

```
“start”: “node index.js”,
“dev”: “nodemon index.js”
```

这两行让我们更容易运行我们的应用程序！我们现在可以使用`npm start`来启动我们的应用程序，否则使用`npm run dev`在开发模式下运行我们的服务器。但是，如果您将入口点更改为 **app.js** ，而不是 **index.js** ，请使用 **app.js** (例如:“start”:“node app . js”)。

5.创建一个新文件 **index.js** (或 **app.js** )

6.在 index.js 的顶部添加以下内容:

```
const express = require('express');
const app = express();
```

我们正在导入 express，这是一个用于创建 express 应用程序并将其存储在 app 变量中的函数。

7.设置您将使用的端口:

```
const port = 8080
```

8.向我们设置的端口添加一个侦听器:

```
app.listen(port, () => {
   console.log(`Server running on port: ${port}`);
});
```

# **添加进路🚀**

要添加路由，在项目目录中创建一个单独的 routes 文件夹，并在其中为您的路由创建一个新文件(例如:**)。/routes/index.js** 或**。/routes/users.js** )。

1.  在**的顶端。/routes/users.js** :

```
const express = require('express');
const app = express();
```

2.在**的底部。/routes/users.js** :

```
module.exports = router
```

3.回到**。/index.js** 并将应用程序与此文件连接，用于具有以下内容的路线:

```
app.use('/', require('./routes/user'));
```

或者，您可以将路线保存到一个变量中，并将其传入:

```
const userRoutes = require(‘./routes/user’);
app.use(userRoutes);
```

4.如果您将接收数据，为了方便地访问发送的数据，您需要使用 express 的 json-parser。另一方面，要处理 CORS 问题以允许请求，您将需要`npm install cors`。这两个重要的步骤加在一起，您将需要添加下面几行到**。/index.js** :

```
const cors = require('cors');
app.use(express.json());
app.use(cors());
```

5.在**中创建一个获取和发布路径。/routes/users.js** :

```
// note: the following routes won't work since we don't have a database for our users, but the syntax is the same!router.get('/users', (request, response) => {
   response.send(‘users’);
});router.post(‘/user/create’, (request, response) => {
   const {name} = request.body;
   if (name) {
      users.push({name});
      res.json({ok: true, users});
   }
});
```

## **奖金！外部获取🐶**

如果您想要获取外部 url 或 API，您将需要首先需要 http 或 https 节点模块。两者之间的唯一区别是 HTTPS 请求是加密的。也就是说，确保你知道你将在两者之间提出哪个要求！在相应路线文件的顶部:

```
const http = require('http')
const https = require('https')
```

然后在同一个文件中使用它:

```
https.get(“https://thisisaurl.com”, res => {
   let data = '' res.on('data', chunk => {
      data += chunk
   }) res.on('end', () => {
      response.send(data)
   })
 }).on('error', error => {
   response.send("Error:", error.message)
 })
```

# **结论🎉**

祝贺你坚持到最后；现在您能够创建一个基本的 Node.js/Express API 了！虽然我们没有介绍数据库，但是如果您喜欢这个并且对 Express 感兴趣，您可以完全扩展到 MERN 堆栈并学习 MongoDB。那是下次的事了，现在庆祝你创建了一个 Node.js/Express 后端！

Celebratory trophy and confetti!

如果您想比较并看看上面的完整文件应该是什么样子:

非常感谢你阅读❤️，我希望这能帮助你开始一个新的项目，你可以继续参考它！提醒一下，下面是一般的命令和安装步骤:

```
// commands
npm init
npm start
npm run dev// installation
npm install express --save
npm install --save-dev nodemon
npm install cors
```

如果你喜欢读这篇文章，看看我的其他文章吧！一个很好的起点是“[获取请求和控制器动作:将前端连接到后端](https://medium.com/p/733a87ffe757)”、“[测试和 Jest 单元测试初学者指南](https://medium.com/p/250d04e61117)”或“[所有关于渲染:客户端和服务器](https://medium.com/p/efc94b117460)”。

# **想要更多？查看其他资源！**💾

## 用 Node/Express 创建简单的 REST API

📖[https://medium . com/@ onejohi/building-a-simple-rest-API-with-nodejs-and-express-da 6273 ed 7 ca 9](https://medium.com/@onejohi/building-a-simple-rest-api-with-nodejs-and-express-da6273ed7ca9)
📖[https://fullstackopen.com/en/part3/node_js_and_express](https://fullstackopen.com/en/part3/node_js_and_express#receiving-data)

## CORS 和 JSON 解析器

📖[https://stack overflow . com/questions/57824556/cannot-fetch-between-express-and-react-apps-due-to-CORS](https://stackoverflow.com/questions/57824556/cannot-fetch-between-express-and-react-apps-due-to-cors)
📖[https://medium . com/@ mmajdanski/express-body-parser-and-why-may-not-need-it-335803 CD 048 c](https://medium.com/@mmajdanski/express-body-parser-and-why-may-not-need-it-335803cd048c)

## 你可以发出不同的回应

📖[https://blog . fullstacktraining . com/RES-JSON-vs-RES-send-vs-RES-end-in-express/](https://blog.fullstacktraining.com/res-json-vs-res-send-vs-res-end-in-express/)
📖[https://www . tutorialspoint . com/difference-between-RES-send-and-RES-JSON-in-express-js](https://www.tutorialspoint.com/difference-between-res-send-and-res-json-in-express-js)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)