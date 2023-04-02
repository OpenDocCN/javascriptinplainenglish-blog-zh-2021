# JavaScript 项目中的 Mongoose 入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-the-mongoose-in-your-javascript-projects-ac444d6d552d?source=collection_archive---------15----------------------->

大家好，欢迎来到我的新博客。今天，我将帮助您在 Express 服务器中使用 Mongoose 集成 MongoDB。

![](img/82e807504c5fc575362b02fe16f0b816.png)

请遵循以下步骤:

# 1.使用 URI 字符串连接数据库。它看起来会像这样—

我们可以将其封装在一个异步函数中，并等待这个 mongoose.connect()方法(或者，我们也可以使用 promises 来处理连接和错误捕获部分)。

如果我们使用 async-await，我们的连接函数将如下所示——

在承诺的情况下，它看起来像这样—

> 另外，不要忘记将 URI 字符串存储在环境变量文件中。

在定义以下内容之前，必须调用这个 connectDb 函数。

# 2.现在，要使用 Mongoose 创建一个 DB 条目，我们必须遵循以下步骤

*   创建一个 Mongoose 模式
*   使用该模式创建一个模型
*   实例化该模型并向其添加数据
*   将此对象添加到数据库中

## *i)创建模式—*

> 在这里阅读更多关于模式类型[的内容](https://mongoosejs.com/docs/schematypes.html)

## *ii)创建该模式的模型—*

## *iii)实例化模型并添加数据—*

> 请注意，我们正在添加的产品应该只有我们在模式中定义的那些键。

## *iv)在数据库中添加—*

最后，该文档将反映在数据库中。

> **注意:**我还没有介绍 npm 包的安装。所以，如果你正面临任何问题，也许这就是问题所在。

> 将此链接加入书签，因为我将在几天后添加您应该维护的文件夹结构，以遵循最佳实践。

如果这个博客对你有所帮助，那么考虑在 Twitter 上关注我，LinkedIn 上关注我👏下面。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)