# 如何处理 Express.js 中的错误

> 原文：<https://javascript.plainenglish.io/how-to-handle-errors-in-express-js-9fe2522ccc53?source=collection_archive---------9----------------------->

![](img/0dde4aae5cdc1a333981f72abd52f0b4.png)

Photo by [James Lee](https://unsplash.com/@picsbyjameslee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

经验不足的开发人员一次又一次地忽略了错误处理，但这对应用程序的稳定性、监控和性能有着重大影响。我将继续讲述如何在您的`express`应用程序中有效地处理错误。

没有明确的方法来处理错误，但有些方法比其他方法更好。让我们深入研究一下。

# 处理控制器中的错误(糟糕的方法):

在这种方法中，我们处理控制器中的错误。对于每个失败的条件/异常，控制器本身将在响应中引发并返回错误。
例如:

app.js ( Controller Level Error handling )

在这里，我们有一个路由`/post`，它在数据库中添加了一个新的帖子。在每个条件和返回响应时，错误都被显式处理。
这种设计有多种警告，会增加系统的复杂性，例如:如果你想跟踪系统抛出的所有错误，你必须到处调用这段代码(跟踪器)，甚至在单个控制器中多次调用。😑这是你从未想过要做的事！

**注意:**这种类型的应用程序架构会阻碍应用程序的扩展，并且很难跟踪所有的错误。

# **处理应用程序中的错误(更好的方法):**

在这种方法中，我们为整个应用程序使用一个通用的错误处理程序。是啊！所有的错误都在同一个地方处理。为了使这个过程更加顺利，我们将使用`[@hapi/boom](https://www.npmjs.com/package/@hapi/boom)` npm 库来生成错误和相应的代码。

app.js ( Application Level Error Handler )

这可能看起来有点复杂，但它比前面的方法好得多。
在 Express 中，我们在每个控制器中获取`next`作为第三个参数，我们简单地使用它将任何生成的错误传递给我们的错误处理程序。

这样，所有的错误都将通过这个处理程序，您可以轻松地跟踪生成的错误，并采取措施来应对系统故障。
此外，这种设计将帮助您扩展您的应用程序，您不需要为每个条件返回错误，而只需使用`next`将产生的任何错误传递给错误处理程序，其余的就可以在那里处理了。

您还可以在系统中集成类似`Sentry`的错误监控工具，以跟踪可能导致系统停机的关键错误。

# 结论

设计系统的基本原则应该是使事情尽可能简单，这也支持更大范围的扩展。

检查我为 Express，Mongoose 创建的样板文件。你会喜欢它的。

[](https://github.com/dhruv479/node) [## DH ruv 479/节点

### 节点快递猫鼬样板。在 GitHub 上创建一个帐户，为 dhruv479/node 开发做出贡献。

github.com](https://github.com/dhruv479/node) 

我希望你喜欢这篇文章，并发现它很有价值。可以关注我上 [*中*](https://dhruv479.medium.com) *和* [*推特*](https://twitter.com/dhruv479) *。感谢支持！*