# 用 JavaScript 同步加载脚本

> 原文：<https://javascript.plainenglish.io/synchronous-script-loading-with-javascript-531b7c44f9a7?source=collection_archive---------6----------------------->

## 创建同步加载 JavaScript 文件的函数

![](img/bf266fcf2ba4117f01778087ed859df3.png)

Synchronous Script Loading in JavaScript

在这篇由 [TechnoFunnel](https://www.youtube.com/channel/UCo-h1M-5M6Y5D4Lgut8ge4w) 撰写的文章中，我们将讨论如何让**动态加载脚本**。在我们的代码中有多种加载脚本的方式。这篇文章的重点是 l **动态加载脚本，并确保脚本列表以同步的方式加载。**

# 动态加载 JavaScript

在下面的代码中，我们将看到如何动态加载脚本。我们经常需要动态加载脚本。有些情况下，只有在特定条件下才需要脚本。在这种情况下，我们需要在条件满足时加载脚本。

[https://gist.github.com/Mayankgupta688/85306d457493008cc127f324384ce90c](https://gist.github.com/Mayankgupta688/85306d457493008cc127f324384ce90c)

在上面的代码中，我们使用 JavaScript 创建了一个脚本标签，并将该脚本标签附加到正文中。当脚本被附加到主体中时，它将被执行，对象和函数可供进一步使用。

接下来，我们需要在代码中添加以下支持功能:

1.  管理我们想要加载的脚本列表
2.  同步加载脚本并保持顺序
3.  等待加载前一个脚本。

# 为什么我们需要同步加载？

在某些情况下，要加载的 JavaScript 依赖于其他一些 JavaScript 文件。如果没有加载相关的 JavaScript，当前的 JavaScript 文件将会中断。示例“jQuery Ui”依赖于“jQuery ”,因此为了使用和下载“jQuery Ui ”,我们需要确保“jQuery”已经在浏览中加载。因此，JavaScript 的同步加载非常重要。

让我们看看如何以同步方式动态加载脚本。

[https://gist.github.com/Mayankgupta688/b51ff52402f1006b715d0eb3e33ee960](https://gist.github.com/Mayankgupta688/b51ff52402f1006b715d0eb3e33ee960)

为了使用这个功能，我们需要以下列方式调用它:

[https://gist.github.com/Mayankgupta688/faf5a727ca572f691bc17b3021914040](https://gist.github.com/Mayankgupta688/faf5a727ca572f691bc17b3021914040)

## 上述代码的解释:

下面是对上述顺序加载代码的简短解释:

1.  我们已经创建了一个名为“sequentialFileLoader”的 life，并从该 life 中公开了一个函数“loadScript ”,该函数将可以像“sequential file loader . loadScript”一样在外部使用。
2.  我们接受一个 JavaScript 文件列表作为数组，我们想要加载它。指定的脚本将按照要求的顺序加载。对于每个脚本，我们执行代码来动态加载它。
3.  一旦我们在 HTML 主体中添加了脚本。我们添加了“onload”事件，这样一旦文件被加载，它就可以递归地调用同一个函数来加载下一个脚本。从而确保仅在当前脚本的“onload”事件之后加载下一个脚本。

这样我们就可以动态地按顺序加载**脚本。**

*更多内容请看*[*plain English . io*](http://plainenglish.io/)