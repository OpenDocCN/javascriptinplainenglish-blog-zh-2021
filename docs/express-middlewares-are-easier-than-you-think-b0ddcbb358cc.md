# 快递中间件比你想象的要简单

> 原文：<https://javascript.plainenglish.io/express-middlewares-are-easier-than-you-think-b0ddcbb358cc?source=collection_archive---------9----------------------->

![](img/37db20c08b393de14860c6b4bf3a7552.png)

在我从上一个 [***博客***](https://js.plainenglish.io/javascript-promises-easier-than-you-can-imagine-cfb18b1f35bc) 中得到正面反馈后，我决定开始另一个博客，在那里我将一个复杂的概念分解，并将其同化为人类大脑熟悉的东西。毕竟，这就是我的工作，让不同背景的[***RBK***](https://medium.com/u/9a3929b3623?source=post_page-----b0ddcbb358cc--------------------------------)学生成为全栈开发者。

今天，我们来看看中间件。当处理从客户端到服务器端的请求时，它们被广泛使用。它们只是一些函数，将请求作为一个参数，对其进行一些处理，然后将其传递给下一个中间件。相信我，这听起来很简单。然而，为了让这个概念在你的头脑中持续存在，我要给你一个具体的例子。

# 汽车制造中的中间件

[特斯拉和 SpaceX 的创始人埃隆马斯克](https://en.wikipedia.org/wiki/Elon_Musk)，地球上最富有的个人智人，将他的汽车制造公司特斯拉的生产线描述为 [***生产地狱***](https://observer.com/2019/02/elon-musk-tesla-production-hell-podcast-interview/) 。这是任何汽车制造商面临的最大挑战。这让我很好的想起了服务器端开发:一个非常 ***关键的******微妙的*** 和 ***不可见的***web 开发的一部分。

我认为如果 Elon Musk 有一个 web 开发机构，他也会对服务器端的请求处理说同样的话。如果你仔细看看，你会发现这是一样的。

服务器接收请求，处理它，并产生响应。汽车制造商收到原材料，用它们做东西，然后送回最终产品。汽车制造商有不同的机器执行不同的任务。服务器也是如此。它有独立的中间件，每个中间件执行一个独特的任务。

有时候，你不需要把汽车作为一个整体来生产。相反，你只想生产轮胎。那样的话，你会**用**一台或两台机器代替。服务器也是一样，你可以为每个单独的请求插入任意多的中间件。

# **使用现有的中间件**

现在让我们看看中间件最简单的例子。为此，我创建了这个 server.js 文件，并在其中导入了 express 和 body-parser。 [Express](https://expressjs.com/) 是 NodeJS 最流行的 web 框架。它允许我们跳过许多样板代码，转而关注我们的业务逻辑。Express for Node 就像 jQuery for vanilla JavaScript。

在这个例子中，我们将使用 Body-parser，它是一个中间件，允许我们访问我们正在处理的请求的主体。首先，我们需要通过运行以下命令从 npm 注册表本地安装它:

```
npm i body-parser
```

然后，我们需要通过 require 导入它，就像我们在第 5 行中做的那样。现在，我们将使用这台机器来处理所有传入的请求。在第 12 行，我们调用了内置方法 use，并为它提供了主体解析器中间件。现在，任何传入的请求都将通过这台机器，因此我们可以访问所有传入请求的主体。

# 创建我们自己的中间件

让我们创建我们的第一个中间件。我们先从一些小而非常有用的东西开始: ***Loggify。*** 该中间件将把任何即将到来的请求(获取、发布、删除、上传、..)以及它将在哪个港口到达。正如我们前面所说的，中间件只是一个函数，它有三个主要参数:

*   正在处理的请求，或者我们正在处理的材料
*   如果我们要发送回响应或最终产品，我们可以使用的响应对象
*   一旦我们的中间件完成了它的工作，并准备好将请求(材料)传递给下一个中间件(机器)，我们可以调用的下一个方法

正如您所看到的，这个函数 loggify 会在第 2 行将请求方法和 URL 记录到控制台。一旦完成，它将把请求传递给生产线上的下一台机器。现在，让我们使用我们的机器。

这是我们在上一节中拥有的同一个文件。除了，现在，我们从第 5 行导出的单独文件中导入了中间件 loggify。与我们在 app.use()中使用 body-parse 的方式相同，我们使用 loggify 函数作为参数再次调用它。现在，任何传入的请求都将通过 loggify 机器，该机器将通知我们，例如，在端点 */users 上有一个传入的 *Get* 请求。*

当然，我们可以为特定的路径使用中间件。为此，我们只需要以这种方式向 app.use()传递一个额外的参数:

```
app.use('/users', loggify)
```

# 结论

中间件是我们希望为 web 服务器上即将到来的请求调用的函数。但是不用为每个请求处理程序重写它们，我们只需定义它们，并在 Express 的 app.use()方法中使用它们。你可以在类似[](https://yarnpkg.com/)*或 [***npm***](https://www.npmjs.com/) 的注册表中找到其他开发者已经编写的数千个，你可以自由地导入和使用。*

*当我第一次接触中间件时，我花了很长时间去理解它们是什么以及如何使用它们。所以，如果还是很混乱的话，是很正常的。你可以继续和他们一起玩！您现在可以创建您的第一个中间件，在您的应用程序中使用它，甚至可以在 npm 注册表中发布它并邀请您的朋友使用它！*