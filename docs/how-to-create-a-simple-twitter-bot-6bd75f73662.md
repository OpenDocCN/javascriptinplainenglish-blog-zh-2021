# 如何用 Node.js 创建一个简单的 Twitter Bot

> 原文：<https://javascript.plainenglish.io/how-to-create-a-simple-twitter-bot-6bd75f73662?source=collection_archive---------14----------------------->

## Node.js 和 twit 模块使得创建 Twitter 机器人变得非常容易

![](img/de30e2af59ada392a6eef774714ed7b4.png)

Photo courtesy of Adam Lukomski from Unsplash

*原载于*[*https://fek . io*](https://fek.io/blog/how-to-create-a-simple-twitter-bot/)*。*

可以使用 JavaScript 和 Node.js 编写的许多流行应用程序之一是 bot。机器人可以被认为是简单的应用程序，可以用来在聊天服务、社交媒体平台和团队通信软件上做广告或回复用户。

一些服务严重依赖于机器人，而另一些则在遇到机器人时直接禁止它们。但是机器人可以用来行善也可以用来作恶。机器人也可以与某种人工智能一起使用，与用户互动。你可能在一些网站上遇到过这种情况，这时会打开一个聊天窗口，询问它是否能帮助你。

在这篇文章中，我将创建一个机器人来回答关于 meetup 群组的简单问题。这个 meetup 群有一个 Twitter 帐户，我将使用它来回答 Twitter 上的问题。

# 创建应用程序

为了创建这个机器人，我将使用 Node.js 和一个名为`twit`的节点模块。您可以使用以下 NPM 命令将它安装到您的节点应用程序中；

```
npm install twit --save
```

Twit 是一个使用 Twitter API 的模块。要使用 Twitter 的 API，你需要[注册](https://dev.twitter.com/apps/new)一个应用。Twitter 需要以下键来与他们的 API 进行交互。这些键如下:

*   消费者 _ 密钥
*   消费者 _ 秘密
*   访问令牌
*   访问令牌密码

一旦您拥有这些密钥，请确保您将这些密钥保存在安全的地方，否则您将需要重新生成密钥。您可以将它们存储在 dotenv 文件中，或者将它们添加到您的环境变量中。

# 配置我们的机器人

为了创建我们的机器人，我们需要做的第一件事是配置`twit`来使用我们的密钥。

既然我们已经配置了应用程序来使用我们的密钥，我们将使用 Twitter 的流 API。使用 stream API，我们可以监听某些单词或标签。对于我们的 meetup 应用程序，我将监听我的 meetup 组的名称， [JaxNode](https://www.jaxnode.com) 。

上面的代码示例过滤流以监听关键字`jaxnode`。任何时候有人用那个关键词发推文，我们都可以使用`on('tweet')`事件实时捕捉那些推文。对于我们的应用程序，我们将在我们的过滤流中回复任何包含以下单词之一的推文:`what`、`where`和`when`。为此，我将获取 tweet 的文本，将其转换为一个数组，并过滤其中一个限定词。

# 使用 Meetup API

为了回答有关我们下次会议的问题，我们将使用 meetup 的 API 来查找有关我们下次会议的最新信息。我们可以使用`axios` HTTP 客户端从 Meetup 检索信息。

这个 API 返回一个 JSON 数组，其中包含我们的 meetup 组的所有即将到来的事件。要用`what`回复任何推文，我们将假设用户想知道下一次会议是关于什么的。返回的对象中有一个`name`属性。我们就用名字来回答`what`的问题。

为了用 tweet 回复，我们将使用 Twitter API 的另一部分来发送 tweet。为此，我们将创建以下函数:

现在，我们可以通过构造回复并发布更新来完成我们的机器人逻辑。

现在，我们可以添加逻辑来回答我们的`what`、`where`和`when`问题的所有三个问题。

# 托管您的机器人

有几个选择来托管你的机器人。如果您有一个现有的 Node.js 服务器，您可以在那里运行您的 bot，但是您也可以使用像 [Vercel](https://vercel.com/) 或 [Heroku](https://heroku.com) 这样的服务来托管。这些云应用服务器通常需要一个 HTTP 侦听器来托管您的 Bot。我们可以通过在 bot 的末尾添加下面一行来实现这一点；

```
http.createServer().listen(3000);
```

当我们完成时，我们的最终机器人应该看起来像下面这样；

# 结论

我认为重要的是要记住，这些机器人应该用于良好的目的。大多数在线服务会试图阻止你向他们的用户发送垃圾邮件。试着尊重分享你平台的其他用户。

这些机器人可能非常有用，当与人工智能结合时，可能非常强大。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)