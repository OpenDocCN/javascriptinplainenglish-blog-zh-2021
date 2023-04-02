# 如何调试电子应用程序

> 原文：<https://javascript.plainenglish.io/how-to-debug-electron-apps-3a8dcfbc2d8a?source=collection_archive---------10----------------------->

![](img/d2b6042f4047db95e804f06b0bf81622.png)

This is how you might feel debugging production Electron applications

Electron 是一个很好的框架，它使得开发跨平台桌面应用程序变得很容易。如果您是一名 JavaScript 开发人员，当您决定构建一个桌面应用程序时，这可能是您要做的第一件事。我知道我做到了。在构建我的第一个和第二个桌面应用程序时，我使用了 electronic。在这个过程中，我学到了一些技巧来帮助开发过程更加顺利。其中一个诀窍是如何更好地调试可能出现在电子应用的打包产品版本中的问题，这些问题在开发中不会出现。

如果你不熟悉[电子](https://www.electronjs.org/)，它是一个允许你用网络技术编写应用程序并在桌面上使用的框架。这是通过将你的应用程序打包到它自己专用的基于 Chromium 的应用程序中来实现的。想象一个网络浏览器。它是一个桌面应用程序，允许你浏览网络应用程序和网页。这就是 Electron 为您的应用程序所做的工作。它创建了一个一次性的桌面浏览器。这样，您可以访问传统 web 应用程序所不具备的本机桌面功能。

像许多软件项目一样，您可能会发现您的本地开发经验并不完全符合生产中发生的事情。当一个应用程序被缩小、构建、编译和打包用于生产时，可能会有一些微妙的变化会破坏应用程序的体验或完全破坏应用程序。当处理桌面应用程序时，这一点尤其正确，因为桌面应用程序比您可能习惯的 web 应用程序有更多的访问权限。当您的应用程序可以在本地工作，但不能在生产状态下工作时，调试问题可能会令人沮丧。当您在生产中只能访问 web 应用程序的 JavaScript 输出，而不能访问底层 Electron 代码的输出时，这在 Electron 中变得更加令人沮丧。幸运的是，我们可以通过使用错误监控服务来解决这个问题。

我们将利用[无异常](https://exceptionless.com/)和无异常 JavaScript 客户端来调试和监控我们的电子应用程序。Exceptionless 可以免费使用，并且完全开源。让我们开始吧。

从你的电子应用程序的项目目录中运行`npm i exceptionless`。

现在，我们可以配置无异常客户端，并在任何地方使用它。这意味着我们可以在“前端”(web app)代码和“后端”电子代码中使用它。出于本教程的考虑，我们将只关注电子代码。在您的`main.js`文件中，在您的其他导入/要求语句下面添加以下内容:

```
const { ExceptionlessClient } = require("exceptionless")
const client = ExceptionlessClient.default.config.apiKey = "YOUR API KEY"
```

您可以在无异常项目设置页面中获取项目 API 密钥。

现在，配置好客户端后，您可以开始使用 Exceptionless 来记录事件。酷的是这些不一定只是错误。如果您想记录主电子代码中某个特定函数被调用的时间，您可以使用`client.submitLog("Function called")`,但要更具描述性。通过提交特定函数的日志事件，您可以确定函数正在被调用。当然，您可以也应该跟踪错误。这就像用你的错误调用`client.submitException(error)`一样简单。

不过，这都很抽象。那么，我们来看一个实际的例子。假设您的电子应用程序正在侦听某个事件，以便将一些数据写入计算机硬盘。我们需要一个来自“前端”html/js 代码的触发器，然后我们需要读取这个触发器并采取一些行动。在 electronic 中，我们使用`ipcMain`来监听来自前端代码的事件。这方面的一个例子可能如下:

```
ipcMain.on("Save File", async (event, message) => {
  try {
    await fs.writeFileSync("/path/to/where/you/want/to/store/the/file", message)
    client.submitLog(`Wrote file successfully with the following content: ${message}`)
  } catch(e) {
    client.submitException(e)
  }
});
```

我在 try 中添加了一个发送到 Exceptionless 的日志事件，并在 catch 中捕获错误并发送给 Exceptionless。这一点的美妙之处在于，我们知道事件何时成功，这令人欣慰，但我们也知道它何时失败以及失败的原因。这很重要，因为这里的失败将是你的应用程序中的一个无声的失败。

假设您认为您试图写入的文件路径在您的电子应用程序构建和打包后并不存在(一个常见的问题是，应用程序默认公开的路径变量可能与您在开发环境中使用和可用的路径变量不同)。如果该路径不存在，`writeFileSync`命令将不起作用。您不知道为什么，您的用户只有在试图获取应该写入的文件时才知道。

想象一下在没有错误和事件监控的情况下尝试调试它。你可以在你的机器上本地启动它，运行一些测试，试着完全按照用户做的那样复制这些步骤。一切都会好的。您看不到错误，因为您的开发环境与生产环境的差异足以让您意识到生产中的写入路径不存在。

你的电子应用程序还有一百万种方式会无声无息地失败。通过添加错误和事件监控，您可以快速调试问题，否则会让您头疼不已。