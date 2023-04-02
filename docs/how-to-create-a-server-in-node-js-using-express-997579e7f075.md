# 如何使用 Express 在 Node.js 中创建服务器

> 原文：<https://javascript.plainenglish.io/how-to-create-a-server-in-node-js-using-express-997579e7f075?source=collection_archive---------17----------------------->

## 在 Express 中构建第一台服务器所需的一切

![](img/1f619e77982e507eadcf6b1110a404e7.png)

Photo by [Florian Krumm](https://unsplash.com/@floriankrumm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我第一次开始学习 Node.js 和 express 时，我感到非常害怕，因为我看到的所有教程都让我构建大中型应用程序。在本教程中，我们将保持简单，构建一个发送“Hello World！”的基本服务器当服务器启动时。

# 项目设置

在我们开始 Node.js 开发人员的旅程之前。我们必须首先做一些初始项目设置

为此，我们需要做的就是在我们的项目中初始化 npm，并将 express 安装到我们的应用程序中。这方面的代码如下所示:

*注:* `*npm init*` *后面的* `*-y*` *允许我们跳过填写****package . JSON****直接进入编码*

之后在你的目录下创建一个名为***server . js****的新文件。*这是我们服务器的所有代码将去的地方。

# 向我们的项目添加 express

现在，我们必须通过 npm 来表达添加安装，我们必须在我们的项目中实际需要它。

在您的 **server.js** 文件中需要 express 模块并将其存储在一个名为 express 的变量中。

我们将有另一个变量来保存我们的服务器在本地运行时运行的端口。这个变量最初将被称为端口

在此之后，我们将创建另一个名为 app 的变量，并使其引用 express()。这个应用程序变量本质上是我们服务器的顶层，它将是我们添加路由并最终启动服务器的方式

这方面的代码如下所示:

# 启动我们的 Express 服务器

现在我们已经设置了样板代码，是时候实际启动我们的服务器了。

这是通过调用我们的 app 变量上的`.listen()`函数并传入我们的 port 变量来完成的。

`.listen()`函数也可以采用可选的第二个函数，在这种情况下，它将是一个箭头函数，记录“服务器在端口上启动”,后跟当前端口号。

这方面的代码如下所示:

# 向我们的服务器添加路由

如果您键入*节点****server . js***并导航到 [http://localhost:5000/](http://localhost:5000/) ，您会看到一个错误。这不是因为我们在编码中犯了错误，而是因为我们在服务器中遗漏了一些关键功能。*路线*

路由是 Node.js 处理来自不同 URL 的不同请求的方式。作为开发人员，我们负责处理每个路由的请求和响应。

在这种情况下，我们通过使用`app.get()`函数并传入我们想要处理的路线来实现。在这种情况下，我们正在处理的路线是我们用`“/”`指定的默认路线。

确保在将`express()`分配给 app 之后，在`app.listen()`之前添加这段代码

之后，我们将第二个参数，一个箭头函数，传递给`.get()`方法来处理请求和响应。

请求和响应是另一篇文章的主题，但你需要知道的是，当我们的服务器启动时，将使用 Node.js(缩写为 res)的响应部分来发送字符串`“Hello World!”`。

这方面的代码如下所示。

*注意:* `*app.get()*` *只是我们可以用来与我们的服务器进行交互的许多方法之一，其他方法还包括* `*.delete()*` `*.post()*` *和* `*.put()*` *，它们被称为* ***HTTP 请求*** *。*

## 完整代码

# 结论

感谢您阅读完我的文章**‘如何使用 Express 在 Node.js 中创建服务器’。我希望你知道如何使用 express 在 Node.js 中创建一个基本的 web 服务器。享受你剩下的一天吧！**

*更多内容请看*[***plain English . io***](http://plainenglish.io)