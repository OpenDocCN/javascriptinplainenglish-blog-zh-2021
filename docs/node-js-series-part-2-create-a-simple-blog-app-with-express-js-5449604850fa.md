# 用 Node.js 和 Express 创建一个简单的博客应用

> 原文：<https://javascript.plainenglish.io/node-js-series-part-2-create-a-simple-blog-app-with-express-js-5449604850fa?source=collection_archive---------0----------------------->

![](img/d49e65f44cf698c84904bfcd5ed3ec0b.png)

在我的 Node.js 系列的第 1 部分中，我们已经学习了如何使用 Node.js 板载资源构建 web 服务器。最后，我们安装了 Express 模块，并将简单路由配置为响应 http 客户端请求的应用程序端点。在第 2 部分中，我想深入了解一下 Express with you 的最重要的功能。在这篇文章的最后，我将开发一个小的博客应用程序。这个博客应用程序使用 HTTP POST 请求读取数据并将数据写入数据文件，并显示数据以响应 HTTP GET 请求。

使用 npm 包管理器在本地的*应用程序根目录*中安装 Express 模块。

***注意:*** *你已经在你的电脑或者你的服务器上创建了一个目录，你的节点应用的所有文件都存储在这个目录中。这个目录叫做* ***应用根目录*** *。在这个应用程序根目录中，您有一个*。js 文件，其中包含运行您创建的节点服务器的所有代码。这是* ***主应用文件*** *和我们这里例子中的文件****server . js****。*

## *应用根目录*

我们从 my Node.js 系列的[第 1 部分](https://patrick-rottlaender.medium.com/create-a-simple-web-server-with-node-js-6db13faab0f5)的*应用程序根目录*的目录结构开始。清单 1 显示了*应用程序根目录*。

您进入应用程序根目录并运行 *npm install* 。

```
:$ npm install express --save
```

## 主应用文件

我们的应用程序根目录中的主应用程序文件是 *server.js* 。 *server.js* 文件是*应用主文件*，包含应用的代码。

将 express 模块装入 server.js 文件，如下所示。

```
// server.js....
var express = require('express') 
var app = express()
....
```

这里发生了什么？使用 require()函数从 express 模块导出 express()函数，并引用变量 *express* 。express()函数基本上是 Express 框架中的主要函数，在 [API 参考](https://expressjs.com/de/4x/api.html#express)中有详细描述。express()函数生成一个*应用*或*对象*，存储在变量 *app* 中。应用程序对象也在 [API 参考](https://expressjs.com/de/4x/api.html#app)中有很好的记录，并且具有可以附加到该对象的方法，例如用于*路由 HTTP 请求*和配置*中间件*的方法。在本文中，我们将看到一些代码来理解路由和中间件。

*server.js* 文件的内容如下。

*package.json* 文件包含应用程序或项目的元数据，例如应用程序已经安装了哪些外部模块或依赖项。package-lock.json 文件包含所有已安装依赖项的完整目录树，最后目录 *node_modules* 包含所有已安装的依赖项、外部模块或包。

我们使用 *server.js* 文件中的代码(从上到下)执行以下操作。

1.  装载模块
2.  定义路线
3.  创建服务器
4.  定义服务器正在监听的端口
5.  当所有代码顺利运行时，在控制台上记录一条成功消息

## 快速路由

路由意味着请求的转发。在我们的 *server.j* s 文件的*清单-2* 中，我们在加载 express 模块之后，通过调用 express()函数创建了一个 app 作为 express 类的实例(参见*清单-2* 中的第 8 行)。

现在可以使用以下符号将路由方法附加到此应用程序。

正如您在清单 2 的代码中看到的，我们定义了 2 个路由或应用程序端点(URIs)。将处理所有与定义的 routingPath 匹配的传入请求，并执行 routingHandler 的代码。

1.  **routingMethod:** 路由方法来源于 GET、POST、PUT 或 DELETE 等 HTTP 方法。在我们的例子中，我们将主要处理 get()和 post()方法。路由方法接收两个参数:routingPath 和 routingHandler。
2.  **routingPath:** 从应用程序的根目录“/”开始作为终点的路由路径。简单地说，这就是 http 请求传递给应用程序的路径。如果传递给应用程序的路径符合端点定义，则执行 routingHandler 代码。
3.  **routing handler:**routing handler 基本上是一个带参数的回调函数，处理一些代码并将 http 响应发送回客户端。

*清单-4* 中的符号显示*routing handler 回调接收请求对象(req)和响应对象(res)作为参数。*

res.send()方法只是将一个字符串发送回客户端并关闭请求。

路由处理器还可以接收函数 *next()* 作为参数。

*next()* 函数将处理转发给回调函数中定义的下一个函数。在*清单-7* 中，显示了第一个函数在不关闭请求和不发送响应的情况下将文本记录到控制台。使用 *next()* 调用下一个函数，最后一个函数使用 res.send()方法向客户端发送响应并关闭请求。

您可以将路由处理函数收集到一个数组中，并将该数组作为参数传递给路由方法。

在上面*清单-8* 的例子中，有 3 个路由处理器函数被收集在一个数组中。该数组作为参数传递给路由方法。r1 和 r2 各自执行一条 console.log 指令，然后使用 next()将路由传递给下一个路由处理函数。r3 然后使用 res.send()方法将响应返回给客户端。

## 响应对象

当应用程序将 HTTP 响应发送回客户端时，express 应用程序会创建响应对象。响应对象记录在 Express [API 参考](https://expressjs.com/de/4x/api.html#res)中。响应方法有多种方法，我们在应用中使用的一种方法是 *res.send()* 方法。

*res.send(body)* 方法可以接收 body 作为参数，而 body 可以是

*   一根绳子
*   一个物体
*   阵列
*   缓冲对象

> **注意:**浏览器使用媒体类型或 MIME 类型来确定如何处理来自服务器的 HTTP 响应。因此，服务器在 HTTP 响应头中发送正确的内容类型非常重要。如果配置不正确，浏览器可能会误解 HTTP 响应，应用程序无法正常工作。媒体类型的结构是类型/子类型。类型表示媒体类型的类别，如文本或应用程序，子类型指定数据的类型，如 html 或 json。媒体类型在 HTTP 响应的 content-type 属性中设置。

下面我想展示在 res.send()方法中使用不同参数时不同的 HTTP 响应头。我的重点是内容类型属性，以及它如何使用不同的参数进行更改。

基本上我在这里展示了两种不同的内容类型*文本*和*应用*。

*   *文本内容类型*包含任何种类人类可读的文本数据，例如源代码之类的格式化数据或 html 或 csv 之类的结构化文本数据。大多数情况下，来自我们的服务器应用程序的 HTTP 响应是 text/html。
*   *应用程序内容类型*是不符合任何其他类型定义的任何二进制数据。在大多数情况下，这些数据将以某种方式执行或解释。真实内容类型未知的二进制数据被设置为应用程序/八进制流。

一个名为 *curl* 的程序使响应头在终端中可见。使用 *curl* 我可以在终端中请求一个 HTTP URI，并得到显示在终端中的 HTTP 响应。所以 *curl* 必须安装在你的系统上。你可以在这里找到好的安装说明。

> **注** : curl 是一个与服务器来回传输数据的程序。curl 支持包括 http 在内的一些协议。I 选项在输出中包含 HTTP 响应头。HTTP 响应报头包括 HTTP 版本、内容类型、日期等。

当我们提供 res.send(body)时，其中 **body 是字符串**，该方法将 Content-Type 设置为“text/html”。

我用 *node server.js* 启动服务器，在另一个终端窗口中运行 *curl -i localhost:3000* 并检查输出。

当我们提供 res.send(body)时，其中 **body 是一个对象**，该方法将 Content-Type 设置为“application/json”。

使用 *node server.js* 启动服务器，在另一个终端窗口中运行 *curl -i localhost:3000* 并检查输出。

当我们提供 res.send(body)时，其中 **body 是一个数组**，该方法还将 Content-Type 设置为“application/json”。

使用 *node server.js* 启动服务器，在另一个终端窗口中运行 *curl -i localhost:3000* 并检查输出。

当我们提供 res.send(body)时，其中 **body 是一个缓冲区**，该方法还将内容类型设置为“应用程序/八位字节流”。

用 *node server.js* 启动服务器，在另一个终端窗口中运行 *curl -i localhost:3000* 并检查输出。

## 请求对象

当应用程序从客户端接收到 HTTP 请求时，请求对象由 express 应用程序创建。请求对象记录在 Express [API 参考](https://expressjs.com/de/4x/api.html#req)中。

请求对象具有可以使用的属性。您可以访问请求中提供的各种属性，并且可以在路由处理程序中处理这些数据。

*例如:*可以用 *req.path* 和 *req.method* 访问请求属性 *path* 和 *method* 。因此，当客户端使用 HTTP GET 方法请求时，即路由“/users ”,这些属性就有了可以使用的值。在这种情况下，我使用 HTTP 响应对象中的值。

因此，在服务器终端中使用 *node server.js* 启动服务器，然后在不同的终端中使用*curl-I localhost:3000/users*访问路由。在服务器终端中，您会看到以下输出。

正如您在上面看到的，当您在应用程序中请求/users 端点时，HTTP 响应包含我创建的对象和我从请求对象接收的值。

*例如:*您的数据库中有许多用户，每个用户在您的 web 应用程序中都应该有自己的个人资料页面。要为每个用户提供这样的配置文件页面，您可以为每个用户创建一个端点或一个路由。这意味着您将拥有如此多路由，且每当有新用户加入您的用户群时，您都必须通过编程新的路由来更改您的应用程序。这是没有用的。

这可以通过使用请求参数来避免。请求参数在您的路由中定义如下。

在服务器终端用 *node server.js* 启动服务器，然后在不同的终端用*curl-I localhost:3000/users/Patrick*访问路由。在服务器终端中，您会看到以下输出。

您的每个用户都可以通过 route */users/:name* 访问他们的个人资料页面。

假设您想在没有任何其他参数的情况下访问 route */users* ，您可以预期这是可能的。不幸的是，这在当前的配置中不起作用。

在服务器终端中保持服务器启动，然后在不同的终端中使用*curl-I localhost:3000/users*访问路由。在服务器终端中，您会看到以下输出。

404 HTTP 状态代码告诉您路由*/用户*不存在，没有找到任何东西。

要解决这个问题，您可以在路由定义中的名称后添加一个问号。这告诉 Express 请求参数是可选的，也可以请求路线/用户。

在服务器终端中再次启动服务器，然后在不同的终端中再次使用*curl-I localhost:3000/users*访问路由。

## Express 中间件

中间件仅仅意味着在请求和响应之间执行代码，以便在必要时参数化响应。让我们看一下下面的路由定义，以展示中间件如何在应用程序端点中执行。

在 *server.js* 文件的开头，我们定义了一个由 3 个函数组成的数组。每个函数将一些文本记录到控制台，并转发给下一个函数。阵列是我们在下面的应用端点定义中使用的中间件。在路由*/示例*上 GET 请求后的端点定义中，routingMethod 首先执行函数 r1、r2 和 r3。从 r1 到 r3 执行 Console.log 命令，并使用 next()转发请求。在此之前，不会返回任何响应。请求由 r3 转发给 routingHandler 函数，然后请求被应答。

也可以将模块作为中间件加载，并在处理任何路由的请求时和响应之前始终执行中间件的代码。

我们假设下面的目录结构。

中间件模块如何工作的一个非常好但简单的例子是使用一个简单的控制台记录器。为了演示这一点，我在模块目录中创建了一个 logger.js 文件。

模块目录中的 looger.js 文件包含以下代码。

*logger.js* 文件包含一个简单的函数 logger()，该函数将使用 module.exports 导出。每当请求任何路由时， *req.method* 和 *req.path* 将被记录在终端中，然后处理将通过 next()函数转发。因此，首先将请求传递给应用程序，然后执行 console.log 指令，然后将请求转发给相应的 routingMethod。

这些路由是在我们的主应用程序文件 server.js 中定义的。

在 *server.js* 主应用文件中，我加载模块并将 logger()函数存储到变量 *logger* 中。中间件集成在带有 *app 的代码中，使用*挂载指定的中间件。

之后，我用*节点 server.js* 启动服务器。在另一个终端窗口中，我使用 curl 来调用路由“/”和“/about”。

在服务器运行的第一个终端窗口中，我们看到日志记录对两条路由都有效。对于这两个请求，都执行了 logger 中间件模块的 console.log 命令。

## 使用 Express 创建一个小型博客应用程序

小博客应用程序应该是一个没有任何 HTML 渲染和输入验证的 web 应用程序。它应该简单地展示我们如何利用到目前为止所学的东西。这个博客将博客和用户存储在一个数据文件中。我们将创建路由端点来添加和删除用户和博客，我们将创建包含程序逻辑的模块来操作数据。

> **注意**:你**永远不要**在没有输入验证的情况下在生产中实现应用程序。从安全角度来看，这是绝对不能接受的。我将在我的[媒体](https://patrick-rottlaender.medium.com/)或我的博客 [Digitaldocblog](https://digitaldocblog.com/home?currpage=1) 上的一篇额外的帖子中用 Express 处理主题*输入验证。*

你可以在我的 [GitHub 页面](https://github.com/prottlaender/node-part-2-express-blog-V1)上找到本章讨论的代码。

首先我们创建一个新的应用根目录 *express-blog* 。在这个目录中，我们用 *touch* 命令创建了主应用程序文件 *blog.js* 和一个 *package.json* 文件。

我们在编辑器中打开 package.json 文件，并编辑该文件，如下所示。

我们使用 *npm install* 安装 express，并确保我们将在最新版本中安装 express，但未来安装时不会对该版本进行更新。

然后我们创建一个 data.json 文件和一个模块目录。

现在已经创建了应用程序根目录的结构，我们可以开始开发博客应用程序了。

**第一步**:首先我要在 *blog.js* 主应用文件中写初始代码。该代码加载我们之前安装的 express 模块，并在 localhost 的端口 3000 上启动服务器。此外，已经定义了一个本地路由。

为了创建用户和博客数据，我应该有 2 个不同的模块。一个将创建用户，另一个将创建博客。因此，我在模块目录中创建了两个文件。

第二步:在 data.json 文件中，我将存储用户和博客数据。数据文件当前为空，但将具有以下结构。

有一个 json 数据对象，带有关键字 *users* 和 *blogs* 。这些键都有一个以对象为元素的数组。所以 data.json (users，blogs)中的每个主键都有 I，j 个元素代表某个用户(data.users[i])和某个博客(data.blogs[j])。

我现在将在 *createUsers.js* 和 *createBlogs.js* 文件中编写两个模块 *usersAdd* 和 *blogsAdd* 。这些文件包含最初创建用户或博客记录或将相应的用户或博客记录添加到 *data.json* 文件的函数。

*createUsers.js* 文件包含以下代码。

首先加载 *fs* 模块。这是一个节点内部模块，用于读取文件以及将数据写入文件。然后我们创建 *usersAdd* 函数，该函数将通过*模块导出。*

*usersAdd* 函数使用 fs.readFileSync 读取 data.json 文件，并将接收到的数据存储到 *dataExp* 变量中。如果 *dataExp* 为空，则我们有一个空数据文件，必须首先创建空数据对象，并将其存储到变量 *data* 中。然后，我们用 data.users 在数据对象上创建用户键，并分配一个空数组。

我们从请求体接收姓名、姓氏和电子邮件，并将这些数据存储到新的用户变量中。对于初始用户条目，我们定义 id 100。

> **注意**:在本教程的后面，我们将看到应用程序主文件 blog.js 中的 POST 路由定义/createusers。这个 POST 路由将使用参数 req 和 res 调用 usersAdd，以便我们可以访问 createUsers.js 中的 req.body 对象。我们将在后面看到。

我们用 name、lastname、email、id 这样的关键字创建一个新的 User 对象，并将从请求主体收到的新用户变量赋值给它们。然后，我们将 newUser 对象推入 users 键的数组(在开始时用 data.users = [ ]创建),该数组链接到我们在开始时用 data = { }创建的数据对象。

```
data.users.push(newUser)
```

在此之后，我们有以下 JavaScript 数据对象。

使用 JSON.stringify()我们获取 JavaScript 数据对象，从中创建一个 JSON 字符串，并将该字符串存储到 dataToFile 变量中。使用 fs.writeFile，我们将 json 字符串写入到目前为止为空的 data.json 文件中。

> **注意**:如果使用 JavaScript 开发应用程序，如果要将数据存储在数据库或数据文件中，JavaScript 对象必须转换成字符串。如果您想将数据发送到 API 或 web 服务器，这同样适用。JSON.stringify()函数为我们完成了这项工作。

到目前为止，我们知道了在 data.json 文件完全为空并且第一个 if 条件为 true ( *if(！dataExp)* )。现在让我们看看，如果第一个 if 条件为 false，即 data.json 文件已经有数据，会发生什么，代码会做什么。如果变量 *dataExp* 不为空，就是这种情况。

正如我们已经看到的，我们在数据文件中存储了一个 JSON 字符串。因此，当我们读取文件并将数据存储到变量 *dataExp* 中时，我们在该变量中有 JSON 字符串数据。为了在我们的 JavaScript 代码中处理这些数据，我们必须解析这个 JSON，以便从 JSON 字符串创建一个 JavaScript 对象。这就是我们用 JSON.parse()函数做的事情。

这里我们将 JavaScript 对象存储到变量*数据*中。

```
var data = JSON.parse(dataExp)
```

因为我们的代码被设计为在 data.json 文件中只存储一个数据对象，所以变量 *data* 就是我们的数据对象。因此，当我们有了数据对象后，我们可以询问用户是否已经存在。

因此，我们使用 if 条件来检查键 *data.users* 是否存在。

以防病情*如果(！data.users)* 为真，关键的 data.users 不存在，这意味着**到目前为止没有可用的用户**。此时，我们创建一个 *data.users* 键，并分配一个空数组。在下面的代码中，一个 *newUser* 对象以与上述相同的方式创建，并使用 *data.users.push()* 方法插入到数组中。现在数据对象有了一个额外的键 data.users，这个键有一个作为值的 *newUser* 对象。现在，我们可以将整个数据对象再次转换为字符串，并完全覆盖 data.json 文件。

万一条件 *if(！data.users)* 为假，关键的 data.users 已经存在并且**用户可用**。如果用户存在，单个用户记录自然会有现有的 id。所以我们首先必须创建一个算法来为新用户获取一个新的用户 ID。

我们首先创建一个变量 *newID* 和一个变量 *minID* 。minID 对应于至少必须被分配的 userID，因为它对应于我们的第一个用户数据对象的 userID。 *minID* 必须是第一条用户数据对象记录的 ID 值。因为用户对象存储在一个数组中，所以它必须对应于零位置的用户对象。

```
var minID = data.users[0].id
```

newID 应该比上一次找到的用户对象的 ID 大 100。这就是为什么我们遍历所有用户对象，将值 100 加到找到的最后一个用户对象的 id 值上。最后，我们将最后一个用户对象的 id 值加上 100，并将这个值赋给 *newID* 。

在下面的代码中，再次创建了一个 *newUser* 对象，整个数据对象被转换成一个字符串并存储到 data.json 文件中。

blogsAdd 函数的代码完全按照相同的方案实现。唯一的区别是博客 id 只增长 1。

createBlogs.js 文件包含以下代码。

**第三步**:需要调整 *blog.js* 文件。首先，我们集成了中间件，它允许我们用 urlencoded 有效负载解析传入的 http 请求。

```
app.use(express.urlencoded({ extended: false }))
```

然后必须用 require()函数将这两个模块加载到 *blog.js* 文件中。因此我们需要文件 *createUsers.js* 和 *createBlogs.js* 。

> **注**:我想在这里再解释一下模块的 require()这个话题。createBlogs.js 和 createUsers.js 文件包含 usersAdd 和 blogsAdd 函数，这两个函数都是使用 module.exports 导出的。module.exports 指令意味着，如果使用 require()加载了 createBlogs.js 和 createUsers.js 文件，则可以在应用程序的其他文件中调用这些函数。usersAdd 和 blogsAdd 没有返回值，因此函数本身保存在 blog.js 中的变量 createBlogs 和 createUsers 中。例如，如果在 POST 路由中调用 createUsers(req，res ),则调用 usersAdd 函数，并将 req 和 res 作为参数传递。

正如我们在上面两个模块的代码中看到的，用户或博客对象的初始创建或添加的值通过请求体传递给函数 *usersAdd* 或 *blogsAdd* 。为此，必须在 *blog.js* 文件中创建发布路径 */createusers* 和 */createblogs* 。这些 POST 路由通过 createUsers()或 createBlogs()调用函数 *usersAdd* 或 *blogsAdd* 。

*blog.js* 文件包含以下代码。

现在，我们能够添加博客和用户。

> **注意**:在这个应用程序中，我们没有用户界面来输入用户变量，如姓名、电子邮件或博客变量，如标题、作者和日期。使用此应用程序，您不能在表单中输入数据，然后使用 HTTP POST 将数据传输到应用程序 routes /createusers 或/createblogs。这就是邮递员出现的地方。使用 [Postman](https://www.postman.com/) 您可以通过在 HTTP POST 请求的 HTTP 主体中手工输入这些数据来模拟一个表单。邮递员检查 POST 请求是否成功。在这一点上，我不想谈论邮递员。所以请。查看 [Postman 网站](https://www.postman.com/)上的文档。

但是仍然没有办法从 *data.json* 文件中删除数据。我们现在想通过如何删除用户的例子来说明这一点。

应该完全接管此功能的模块是 usersRemove()函数，我将把它写入文件 r *emoveUsers.js 中。*为此，我们首先在模块目录中创建一个空文件 r *emoveUsers.js* 。

*removeUsers.js* 文件包含以下代码。

我们首先再次加载 node fs 模块，然后定义函数 usersRemove()，然后在代码末尾使用 module.exports 导出该函数。函数 usersRemove()接收 req 和 res 作为参数，读取 *data.json* 文件，并将读取的数据解析为由变量 *data* 表示的 JavaScript 对象。

为了向您展示数据对象，我只需运行如下脚本。

当您检查您的控制台时，您可以看到我们将文件中的所有 json-data 保存在变量 data 中。我们看到一个可以在我们的代码中使用的 JavaScript 对象。

在代码中，我们从 req.body 中获取 userID，并将其存储到变量 delUserID 中。req.body 中的值是一个字符串。当我们在 json 数据文件中将 userIDs 作为数字操作时，我们必须将字符串转换成数字。这是用“- 0”完成的。这里我们减去数值零，告诉 JavaScript delUserID 是一个数字而不是一个字符串。

然后我们必须找到需要删除的用户对象。用户对象是 data.users 数组中的元素。因此，我们必须找到 req.body 中的 userID 与 data.users 数组中的 userID 相匹配的用户对象，因为这个 userID 标识了应该删除的用户对象，因此应该从 data.users 数组中删除。

当来自 rep.body 的 userID 等于 data.users 数组中用户对象的 userID 时，回调函数 elementFound 返回 true。

data.users.findIndex()方法返回在 data.users 数组中找到的第一个用户对象的索引，其中来自 rep.body 的 userID 等于用户对象的 userID。

data.users.splice(index，1)在索引位置删除 1 个用户对象。由于 findIndex()方法之前返回了我们要删除的用户对象的确切位置，这里的 splice()方法最终删除了用户对象。

由博客对象和用户对象组成的完整数据对象现在减少了一个用户对象。缩减的数据对象作为一个整体转换成一个字符串，并使用 fs.writeFile()方法再次写入 data.json 文件。

blogsRemove()函数的工作方式与上面解释的 usersRemove()函数相同。因此，模块目录中的文件 removeBlogs.js 如下所示。

在上面两个 removeUsers.js 和 removeBlogs.js 模块的代码中，要删除的用户或博客对象的值通过请求体传递给 usersRemove()或 blogsRemove()函数。为此，必须在 *blog.js* 文件中创建 POST routes /removeusers 和/removeblogs。这些发布路由调用模块 removeUsers.js 和 removeBlogs.js 中定义的函数 usersRemove()或 blogsRemove()。这些模块也必须用 require()函数加载到 *blog.js* 文件中。

blog.js 文件现在包含以下代码。

**第四步**:我们的应用程序目前可以创建用户和博客，也可以删除博客和用户。到目前为止还不错。现在应该添加另一个功能，即博客的显示。这将通过这样一种方式实现，即一个路由的 GET 请求根据请求中提供的请求参数向服务器发回不同的响应。

这是什么意思？

例如:我们的数据文件中有各种博客，它们都是为特定日期创建的。我们希望看到所有的博客，也希望看到某年或某月的博客，或者是在特定日期创建的博客。

您希望通过此途径访问所有博客。

而你想在 2020 年用这个途径访问所有的博客。

诸如此类。

我们可以使用请求参数更优雅地做到这一点。我们在 blog.js 文件中创建了以下 GET route。

问号表示参数年、月和日是可选的，也可以在请求时省略。

我们已经定义了一个路由，它应该根据请求参数给出不同的响应。这就是为什么我们首先必须评估路由定义中的请求参数，然后定义应该如何回答不同查询的条件。

稍后我将回到完整的主应用程序文件 blog.js。

我们的目标是显示博客文章。根据路线，我们希望显示(1)所有博客或(2)一年的所有博客或(3)一年零一个月的所有博客或(4)特定日期的所有博客帖子。

为了从我们的 *data.json* 文件中收集所请求的数据，我们基本上需要 4 个新函数来执行这些查询。因此，我在模块目录中创建了一个新的*查询模块*。这个 *queryModule* 包含所有这 4 个查询函数，它们都将在我们的应用程序中可用。 *queryModule* 文件中的代码符号与前面的模块略有不同。

原因是，我们以前在模块目录中有一个模块文件，该文件中只有一个函数。模块文件导出值是函数本身。

在我们的主应用程序文件中，我们用 require 函数加载 previousModule，并将值作为函数存储到变量 previousModule 中。然后我们可以用 previousModule()直接调用主应用程序文件中的函数。

现在，我们示例中的 queryModule 应该查询博客，我们需要不同的函数。所以这个文件是不同的。在这个文件中，我们收集了 4 个函数，但是我们没有将它们作为函数导出。相反，我们使用 module.exports 来导出一个有 4 个键的对象。这些键中的每一个都只有一个值，这个值就是各自的功能。

在我们的主应用程序文件中，我们用 require 函数加载 queryModule，并将导出的对象存储到变量 *queryModule* 中。我们现在可以通过 *object.key* 符号从主应用程序文件中调用函数。

当我们在 modules 目录中查看新的 *queryBlogs.js* 文件时，您会看到该文件中有一个包含 4 个不同键的对象，这些键包含以下函数()作为值。

*   queryAllBlogs
*   queryBlogsYear
*   queryBlogsYearMonth
*   queryBlogsYearMonthDay

与前面的模块还有一个重要的区别。 *queryBlogs.js* 中的那些函数每个都返回值。这个值是查询结果，稍后可以在我们的主应用程序文件 *blog.js* 中使用，以向最终用户显示请求的数据。基本上，这个值是一个博客文章的数组，当某个路由被请求时，应该显示这些博客文章。

因此 *queryBlogs.js* 文件如下所示。我将详细解释*查询日志*和*查询日志年份*。另外两个功能 *queryBlogsYearMonth* 和 *queryBlogsYearMonthDay* 示意性相同。

我们的数据作为字符串存储在一个 *data.json* 文件中。我们应用程序中与数据相关的每个操作都要求我们能够访问 JavaScript 数据对象。因此，如果我们想要搜索或选择数据，以便在应用程序中只显示其中的一部分，例如，只显示某一年的所有博客文章，仍然需要事先从数据文件中读取全部数据。在拥有大量数据的大型项目中，这种基于文件的方法并不合适。然后，您应该使用数据库。

> **注意**:对于大量的数据，使用 MongoDB 这样的数据库是有意义的，因为我们可以直接在数据库中搜索特定的值，而没有必要从数据库中检索所有的数据。我将在以后的另一篇文章中向您展示 MongoDB 的用法。为了简单起见，在本文中让我们坚持使用基于文件的方法。

*queryAllBlogs* 函数是我们显示博客的其他查询的基础。这个函数首先定义一个空数组 *allBlogs* 。然后，如上所述，使用 *fs.readFileSync* 从数据文件中完全读取数据，并使用 *JSON.parse* 将其转换为 JavaScript 对象。现在，我们可以访问带有*数据的博客帖子。然而，这并不完全正确。正如我们在上面已经看到的， *data.blogs* 是数据对象中的一个键，这个键有一个数组作为值。严格地说，这个数组包含的元素是博客文章。*

在任何情况下，通过 for 循环，我们使用 data.blogs[i]遍历数组的所有元素，以便可以从数据文件中读取每个单独的博客数据记录，并使用 *allBlogs.push()* 方法将其作为*数据集*对象附加到首先定义的 *allBlogs* 数组。函数 *queryAllBlogs()* 然后将 *allBlogs* 返回给调用者。*所有博客*包含所有*数据集*对象。allBlogs 数组如下所示。

函数 *queryBlogsYear* 将 *allBlogs* 数组作为参数(与模块中定义的任何其他函数 queryBlogs*一样)。这是因为我们希望在 *queryBlogsYear* 函数中选择其中的所有数据，因此所有的博客文章都必须在该函数范围内可用。

> **注意:**只看 queryBlogs.js 文件，不明白 queryBlogs*函数中的 allBlogs array as 参数是从哪里来的。要访问所有博客中的数据，必须首先执行返回所有博客的 queryAllBlogs 函数。这发生在 routingMethod 的应用程序主文件 blog.js 中。请。见下文。

首先，我们创建空数组 yearBlogs。该数组将在函数代码的末尾包含所有应该由 queryBlogsYear 函数稍后返回的数据。

然后我们使用 for 循环遍历 allBlogs 数组。

在 for 循环中，我们首先用 *allblogs[i]读取 blog date 的值。日期*并将该值存储在变量 *blogDate* 中。在数据文件中，日期以 ISO 8601 日期格式(YYYY-mm-dd)保存。强烈建议总是以这种格式保存日期，因为 ISO 8601 是 JavaScript 首选的日期格式，因此对日期的所有其他操作都更容易。为了在 JavaScript 中很好地处理日期字符串 yyyy-mm-dd，必须首先使用 *Date.parse()* 将这个字符串 date 转换成一个数字。然后使用 *new Date()* 方法将该数字转换成一个日期对象。

> **注** : Date.parse()接收 ISO 8601 格式的日期字符串 yyyy-mm-dd，并返回一个表示 UTC 1970 年 1 月 1 日 00:00:00 之间的毫秒数。这个数字是唯一的，是使用 new date()方法创建 Date 对象所必需的。使用这个日期对象，我们可以访问给定日期对象的年、月或日。

在我的代码*中，Date.parse()* 作为参数直接传递给 *new Date()* 方法，这样就可以从返回的数字中直接生成所需的日期对象。日期对象存储在变量 *parsedBlogDate* 中。

因为 *parsedBlogDate* 表示一个对象，所以*parsedBlogDate . getfullyear()*方法让我们能够访问日期所对应的年份。年份存储在*变量 parsedBlogDateYear* 中。

> **注意**:我使用 parsedBlogDate.getMonth()从 Date 对象中检索月份。此方法为一月返回 0，为十二月返回 11。因此，有必要添加“+1”来获得通常的值 1 表示一月，12 表示十二月。我们将使用 parsedBlogDate.getDate()检索一个月中的第一天为 1，每个月的最后一天为 max 31。

然后我们在 if 循环中比较请求中传递的年份(year = req.params.year，变量 year 在 blog.js 中定义)和所有博客文章的年份。我们只生成请求的年份与博客文章的年份相匹配的数据集。以这种方式创建的数组 *yearBlogs* 然后作为返回值返回给调用者。

我现在将回到主应用程序文件 *blog.js* 和具体的路由定义，在这里我们评估请求参数并提供不同的响应。通过这个路由，我们根据请求参数发送以下响应。

*   所有博客帖子— res.send(所有博客)
*   给定年份的博客帖子— res.send(blogsYear)
*   给定年份和月份的博客帖子— res.send(blogsYearMonth)
*   给定日期的博客帖子— res.send(blogsYearMonthDay)

我们已经定义了一个路由，它根据请求参数给出不同的响应。当请求 url == /blog 时，我们希望看到所有博客，当请求 url == /blog/2019 时，我们看到所有博客，即给定年份 2019 的博客，等等。

首先，我们用 require()函数加载 *queryBlogs* 模块，并将对象保存在变量 *queryBlogs* 中(记住模块 queryBlogs 返回一个函数对象)。

在路由定义中，我们获取与请求一起传递的请求参数，并将它们保存在变量 url、year、month 和 day 中。然后我们用*queryBlogs . queryAllBlogs()*访问 queryBlogs 模块中定义的 *queryAllBlogs()* 函数。这个函数返回所有的博客文章，这些博客文章存储在 *allBlogs* 数组中。

然后，我们创建 if 和 else if 条件来定义应用程序中路由定义的响应行为。

在请求的 url 等于 */blog* 的情况下，如果条件为真，则首先为**。当 allBlogs 数组为空时，下面的 if 条件为 true。然后，响应是 no post found*RES . send(' no post found ')*。当这个 if 条件为 false 时，已经在 *allBlogs* 数组中找到了博客文章。在这种情况下，来自 *allBlogs* 数组的所有数据将通过 *res.send(allBlogs)* 发送回调用者。**

如果请求的网址等于*/博客/年份*(即/博客/2019)，则条件为真，则**为先。当 else if 条件为真时，我们调用 queryBlogs 模块中的 queryBlogsYear()函数，并将 allBlogs 数组作为参数传递。我们使用*query blogs . query blogs year(all blogs)*调用函数，并将返回值存储在数组变量 *blogsYear* 中。**

如果 *blogsYear* 数组为空，下面的 If 条件为真。这意味着在*所有博客*中没有找到请求年份的博客帖子。那么响应是今年没有找到帖子*RES . send(‘今年没有找到帖子’)*。当 if 条件为 false 时，已经找到请求年份的博客文章，并且 blogsYear 数组不为空。然后来自 *blogsYear* 数组的所有这些数据将被用 *res.send(blogsYear)* 发送回调用者。

当请求的网址等于*/博客/年/月*(即/博客/2019/04)时，条件为真则**秒。当 else if 条件为真时，我们调用 queryBlogs 模块中的 *queryBlogsYearMonth()* 函数，并将 *allBlogs* 数组作为参数传递。我们使用*queryblogs . queryblogsyearmonth(all blogs)*调用函数，并将返回值存储在数组变量 *blogsYearMonth* 中。**

如果 blogsYearMonth 数组为空，则下面的 If 条件为真。这意味着在*所有博客*中没有找到请求年份和月份的博客帖子。那么响应是今年和本月没有找到帖子*RES . send(‘今年和本月没有找到帖子’)*。当这个 if 条件为 false 时，已经为所请求的年份和月份找到了博客文章，并且 *blogsYearMonth* 数组不为空。然后，blogsYearMonth 数组中的所有这些数据将通过*RES . send(blogsYearMonth)*发送回调用者。

在请求的 url 等于*/博客/年/月/日*(即/博客/2019/04/10)的情况下，如果条件为真，则**为第三个否则。当 else if 条件为真时，我们调用 queryBlogs 模块中的 queryBlogsYearMonthDay()函数，并将 allBlogs 数组作为参数传递。我们使用*queryblogs . queryblogsyearmontday(all blogs)*调用函数，并将返回值存储在数组变量*blogsyearmontday*中。**

如果 blogsYearMonthDay 数组为空，则下面的 If 条件为真。这意味着在*所有博客*中没有找到请求日期的博客帖子。那么响应是没有找到今年和年月日的帖子*RES . send(‘没有找到今年和年月日的帖子’)*。当 if 条件为 false 时，已找到请求日期的博客文章，并且 blogsYearMonth 数组不为空。然后来自 *blogsYearMonthDay* 数组的所有这些数据将通过*RES . send(blogsYearMonthDay)*发送回调用者。

如果所有 **if 和 else if 条件**为假，则请求的 url 与任何已定义的请求参数(/blog/:year？/:月？/:日？).则**否则响应**为 *res.status(404)。发送('未找到')*。

## 总结与展望

在 Node.js 系列的第 2 部分中，我解释了 express 的一些非常重要的细节，以及如何在 web 应用程序开发中使用 Express。基于我们在[第 1 部分](https://digitaldocblog.com/webserver/nodejs-series-part-1-create-a-simple-web-server-with-nodejs/)中已经了解的关于 Express 的知识，我们详细地查看了 Express 路由，以及如何相对容易地在 Express 中使用中间件。利用我们学到的知识，我们构建了一个简单的博客 web 应用程序，并应用了这些知识。

这个博客应用程序有一个文件中的所有数据，没有 HTML 前端。Express 非常适合使用像 MongoDB 这样的数据库，也适合使用 HTML 模板来呈现内容。在我的 Node.js 系列的下一篇[第 3 部分](https://digitaldocblog.com/webserver/nodejs-series-part-3-the-simple-express-blog-app-with-mongodb/)中，我将向您展示如何使用 MongoDB 数据库而不是数据文件。然后，我们将继续开发博客应用程序，并在博客应用程序上实现一个 HTML 前端。

## 进一步阅读

[](https://bit.cloud/blog/how-to-build-a-composable-blog-l1jkl9f4) [## 如何建立一个可组合的博客

### 从头开始创建一个博客需要很多。有许多移动的部件组合在一起形成一个…

比特云](https://bit.cloud/blog/how-to-build-a-composable-blog-l1jkl9f4) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****