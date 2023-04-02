# 用 JSON Server 构建本地 API

> 原文：<https://javascript.plainenglish.io/building-a-local-api-with-json-server-3d1547d81999?source=collection_archive---------11----------------------->

在做一个小的 React 项目时，我做这个项目的唯一目的是测试我新学到的钩子知识，我考虑使用 Rails 作为我项目的后端。我也有尝试新事物的愿望，在四处寻找最适合我的项目目的的数据库后，我遇到了 JSON Server。这是一个理想的适合。

## 什么是 JSON 服务器，我为什么要使用它？

JSON Server 是一个节点模块，它以 JavaScript 对象的形式为您创建完整的模拟 REST API。当你在做一个演示，还没有一个明确的项目方向，或者只是想要一个快速的后端让你处理一些数据时，这是非常方便的。您只需要一个 JSON 文件来存放种子数据，就可以开始了！

## **安装**

为了在您的机器上安装 JSON 服务器(假设您已经安装了 NPM)，请在您的终端中输入以下内容:

```
npm install -g json-server
```

我建议通过检查模块的版本来确认安装:

```
json-server -v
```

然后，您应该在终端输出中看到版本(我的当前版本是 0.16.3)。如果您想查看更多选项或获得帮助，也可以运行以下命令:

```
json-server -help
```

## **使用 JSON 服务器**

现在服务器已经安装好了，我们可以继续在应用程序中使用它了。此时，我已经设置好了我的应用程序(为此我使用了*create-react-app*generator ),并准备好继续使用服务器。接下来，在我的应用程序的根目录中，我运行以下命令来打开我的新 db 文件:

```
nano db.json
```

您现在应该看到一个空白文件，它将存储您的 JSON 数据。创建一个简单的 JSON 对象，例如:

```
{ "items": [ { "description": "candle", "id": 1 }, { "description": "book", "id": 2 } ]}
```

在这里，我们创建了一个对象，它的键为“items ”,值数组的键为“description ”, id 为。现在保存并关闭文件。要从命令行运行此服务器，并且不让它干扰 create-react-app(或任何其他)服务器，您需要指定配置并将其作为脚本添加到您的 package.json 中。Open package.json:

```
nano package.json
```

然后在“脚本”对象中添加以下内容作为第一行:

```
"api": "json-server db.json -p 5555",
```

正如您在上面看到的，我将端口指定为 5555，这样它就可以与 3000(来自 create-react-app)同时运行，而不会有任何冲突。保存并关闭文件，打开一个**新的终端窗口/标签**。在这里，您需要输入以下内容来启动您的 API 服务器:

```
npm run api
```

您现在应该得到一个确认 db.json 已加载的输出，以及类似如下的内容:

```
 Resources
  http://localhost:5555/items

  Home
  http://localhost:5555
```

在使用数据库时，保持该服务器运行。您现在可以在浏览器中打开并查看您的 API 了！干得好！

## **编辑您的数据库**

除了简单地获取和显示数据，您还可以直接从命令行使用 JSON Server 创建、更新和删除数据。例如，要发布新项目，请尝试以下操作:

```
curl -d '{"description":"bag"}' -H 'Content-Type: application/json' -X POST [http://localhost:5555/](http://localhost:3333/list)items
```

您将看到您的数据库已经更新，现在包含您的新项目，也有一个 id 键。

## 结论

您可以使用 JSON Server 做得更好(例如，定义自定义路线)，我希望这篇文章有助于解释入门所需的基础知识。从中获得乐趣，并确保仔细检查您的工作，以防止不必要的更改被保存到您的数据库中！