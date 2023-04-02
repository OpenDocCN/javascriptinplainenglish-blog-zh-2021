# 使用 Express 和 MongoDB Atlas 构建 CRUD 应用程序

> 原文：<https://javascript.plainenglish.io/build-a-crud-application-using-express-and-mongodb-atlas-444f2a7f122b?source=collection_archive---------4----------------------->

![](img/cb1c0d0080e4d95ffaace2669c798038.png)

在本文中，您将学习如何使用 Express 和 MongoDB 构建 CRUD 应用程序。

我会尽可能的简单。为了帮助你节省时间，我决定写这篇文章。让我们看看它是如何工作的！

## 创建一个 MongoDB Atlas 帐户

过程很简单。前往 [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/lp/try2?utm_source=google&utm_campaign=gs_footprint_row_search_core_brand_atlas_desktop&utm_term=mongdb%20atlas&utm_medium=cpc_paid_search&utm_ad=e&utm_ad_campaign_id=12212624584&gclid=CjwKCAjw-e2EBhAhEiwAJI5jg-59YS1MbxYolznxDSKFG-YL8jrSaFPBw5TpFt3s2uu2Axz5FMyULBoCNVoQAvD_BwE) 并创建一个新账户。如果已经完成，您可以登录现有帐户。

创建您的帐户或登录后，在您的控制面板上单击“创建新集群”按钮。

![](img/efcc4925f00d2f733d02bc3fcfdb03bb.png)

MongoDB dashboard

应该会出现一个新页面，询问您创建新集群的详细信息。请注意，如果您已经创建了一个集群，那么第二个集群将会花费您很多钱。如果那是你的第一次，那么它是免费的。继续并点击“创建集群”按钮。

![](img/0aa5ad09b743545af86fb302244e6907.png)

# 创建您的数据库

下一步是创建数据库。为此，您需要创建一个数据库用户。在您的仪表板上，单击“数据库访问”按钮。

![](img/3f57bf1f686b92993b27c5a27ac1dda8.png)

定义一个用户名和密码，然后点击“添加用户”按钮。确保用户对您的数据库有读写权限。

![](img/32a91804e36e361315179d7216bed6ae.png)

# 将您的 IP 地址列入白名单

为了连接到您的本地项目，将您的 IP 地址列入白名单是一个必要的步骤。为此，请单击“网络访问”选项卡。

您可以将您当前的 IP 地址列入白名单，或者允许来自任何地方的访问。在这种情况下，只需选择将您当前的 IP 地址列入白名单。

![](img/35fc96b2ad59bfe403ace4d062f8f983.png)

# 与本地设置的连接

是时候设置与本地项目的连接了。

我们将使用 [Express](https://expressjs.com/) 创建一个服务器。服务器将帮助我们创建、读取、更新或删除项目。基本上，CRUD 操作。

为此，我创建了一个新的空文件夹，我称之为 blog，因为我们将创建博客文章。打开我的新文件夹，从我的终端使用命令 *npm init -y* 创建一个名为 *server.js* 的文件和一个 *package.json* 文件:

```
npm init -y // to create a package.json file
```

现在我可以安装需要的软件包了

```
npm i express mongoose nodemon dotenv
```

这些软件包如下:

*   设置服务器的步骤
*   m[on 选择](https://www.npmjs.com/package/mongoose)与我的 MongoDB Atlas 数据库以及任何本地数据库进行交互
*   [Nodemon](https://www.npmjs.com/package/nodemon) 在我的应用程序中检测到更改时重启服务器。
*   [dotenv](https://www.npmjs.com/package/dotenv) 创造。我们的 MongoDB 凭证的 env 文件

我的文件夹结构现在是:

```
blog
--node_modules
--app.js 
--package.json
--package-lock.json 
```

在您的 *app.js* 文件中，让我们设置 express 服务器:

```
//app.js const express = require("express");const app = express();app.listen(3000, () => {
  console.log("Listening at port 3000");
});
```

## 与 MongoDB Atlas 的联系

现在我们将应用程序与 MongoDB Atlas 连接起来。为此，我们创建一个名为 *connection.js* 的文件来建立连接。在这个文件中，我们会有这样的代码:

让我们来分解一下:

*   我们需要 dotenv 模块来避免暴露我们的凭证
*   用连接参数定义一个对象。这对于连接到我们的 MongoDB Atlas 服务器非常有用。
*   现在我们有了一个 URI 变量。这保存了您的 MongoDB Atlas 连接 URL。我马上告诉你去哪里拿你的。
*   接下来，我们建立服务器和 MongoDB Atlas 之间的连接。这是通过命令*mongose . connect()*完成的。连接是异步操作。所以我们用一个*来处理。然后()*如果连接建立或*。catch()* 如果他们在我们的连接中有问题。
*   最后，我们使用*模块导出我们的连接对象。*

## 如何获得您的 MongoDB URI:

要得到你的 URI，很简单。在您的仪表板(MongoDB Atlas)中，单击“连接”，然后“连接到应用程序”。

![](img/24f748c84d097761ad02bc5e26da22ef.png)

这应该会弹出来:

![](img/6fa741358f63aa21d8f90efaa72c99cc.png)

您可以在 connection.js 文件中使用 URI，其中<password>是实际 MongoDB 数据库用户密码的占位符。然后，可以在 nodeJS 文件夹中创建一个. env 文件，如下所示:</password>

```
//.env MONGO_USERNAME=your_username
MONGO_PASSWORD=your_password
```

注意你的*。env* (注意点号)文件应该在你的根路径中。到目前为止，您的文件夹结构应该是这样的:

```
blog
--node_modules
--app.js
-- .env
--package.json
--package-lock.json
```

然后我们用*替换用户名和<password>值。env</password>* 值如下:

```
`mongodb+srv://${process.env.MONGO_USERNAME}:${process.env.MONGO_PASSWORD}[@cluster0](http://twitter.com/cluster0).s11qz.mongodb.net/blog?retryWrites=true&w=majority`
```

## 将连接导出到 app.js

设置连接后，可以将其导入 app.js 文件中:

```
const express = require("express");
const connection = require("./connection");
const app = express();app.listen(3000, () => {
  console.log("Listening at port 3000");
});
```

让我们定义一个命令来启动应用程序。在您的 *package.json* 文件中(“脚本”部分)，添加命令“start ”,如下所示:

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon app.js"
  },
```

*package.json* 文件应该是这样的:

现在，通过打开终端并键入命令来运行应用程序:

```
npm start
```

如果一切顺利，您的控制台中应该会出现一条消息，内容如下

```
connected to database
```

这个过程是异步的，所以在您看到它之前，预计需要几秒钟。如果没有建立连接，它将返回一个包含详细信息的错误。

您可以重试该过程，并检查您的用户名和密码是否与您创建的用户的用户名和密码相匹配。如果您忘记了您的凭证，有一个简单的方法可以在“数据库访问”选项卡中更改它们(在 MongoDB Atlas dashboard 中)。

# CRUD 操作

现在我们已经建立了数据库，是时候创建我们的博客文章了。为此，我们创建了一个 Post 模型。这个帖子模型是帮助我们从数据库中创建或阅读博客帖子的蓝图。

在您的根文件夹中，创建一个 *postModel.js* 文件。您的文件夹结构应该如下所示:

```
blog
--node_modules
--.env
--app.js 
--connection.js
--package.json
--package-lock.json
--postModel.js
```

在您的 *postModel.js* 中，有您为 Mongodb 数据库创建新帖子的模型。它应该是这样的:

在这里，我们做了以下事情:

*   创建一个带有标题和内容的模式
*   设置使用此模式的发布模型
*   导出文章，在你的 *app.js* 文件中使用

现在，当您准备创建或更新您的博客帖子时，您可以使用这个帖子模型。

# 创建您的路线

在 *app.js* 文件中，服务器现在正在运行，但是没有路由。为此，我们可以创建路由来创建、读取、更新或删除项目。以下是不同的操作:

## 创建帖子

在进行任何操作之前，我们需要将模型导入到 app.js 文件中。我们还需要设置我们的 express 服务器，以便它可以接收参数并解析它们。下面是 app.js 导入语句的更新版本:

```
//app.js const express = require("express");
const connection = require("./connection");
const postModel = require("./postModel.js");
const app = express();
app.use(express.urlencoded({ extended: true }));
app.use(express.json());..
//rest of the code
```

CRUD 操作的第一部分是创建一个新的职位。为此，我们添加了一条新路线:

```
app.post("/", async (req, res) => {
  const { title, content } = req.body;
  try {
    const newPost = await postModel.create({
      title,
      content,
    });
    res.json(newPost);
  } catch (e) {
    res.status(500).send(e);
  }
});
```

让我们来分解一下:

*   当向我们的服务器发出 post 请求时，它会被解析以检索内容和标题。
*   然后，我们将后期制作包装成一个 try…catch。这允许我们处理异步操作以及任何可能发生的错误。
*   一旦使用 postModel 创建了新的 post，它应该将它作为 JSON 数据返回给客户机。

## 阅读或获取帖子

为了从数据库中获取所有帖子，我们定义了这条路径:

```
app.get("/", async (req, res) => {
  try {
    const posts = await postModel.find();
    res.json(posts);
  } catch (e) {
    console.log(e);
  }
});
```

这是一个异步请求，所以我们使用 try…catch 并将 *async* 关键字添加到回调函数中。这给了你一个数组，其中包含了所有 JSON 格式的博客文章。

我们还定义了从服务器读取或获取一个帖子的路径:

```
app.get("/:id", async (req, res) => {
  const { id } = req.params;
  try {
    const post = await postModel.findById(id);
    res.json(post);
  } catch (e) {
    res.status(500).send(e);
  }
});
```

这将从 params 中获取 id，并根据 id 找到帖子。

## 更新帖子

要更新帖子，您可以在上传和修补请求之间进行选择。在这种情况下，我们使用 PUT 请求:

```
app.put("/:id", async (req, res) => {
  const { id } = req.params;
  const { title, content } = req.body;
  try {
    const post = await postModel.findByIdAndUpdate(id, { title, content });
    res.json(post);
  } catch (e) {
    res.status(500).send(e);
  }
});
```

这段代码从 params 中提取 *id* ，并使用 [*。findByIdandUpdate()*](https://mongoosejs.com/docs/api.html) 方法，在用新标题和内容更新项目之前，通过 id 查找项目。然后，它将数据作为 JSON 发回。

## 删除帖子

最后，删除一篇文章遵循相同的过程，但是我们使用*。删除()*:

```
app.delete("/:id", async (req, res) => {
  const { id } = req.params;
  try {
    const post = await postModel.findById(id);
    await post.remove();
    res.json("deleted");
  } catch (e) {
    res.status(500).send(e);
  }
});
```

整个 app.js 文件现在变成了:

*更多内容请看*[*plain English . io*](http://plainenglish.io/)