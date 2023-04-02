# 如何在 3 小时内编写并发布一个 Chrome 扩展

> 原文：<https://javascript.plainenglish.io/how-to-write-and-publish-a-chrome-extension-in-under-3-hours-bf07a887f0ab?source=collection_archive---------15----------------------->

## 一个快速简单的项目为您的投资组合。

![](img/1ac2bcd91af4d56f1f3723c4ada98b31.png)

Photo by [Firmbee.com](https://unsplash.com/@firmbee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你是一个初学程序员，你可能经常问自己的一个问题是你应该从事什么样的项目。我以前写过的一个很好的选择是[克隆现有的网站](/how-to-start-and-finish-a-clone-project-that-gets-you-jobs-fast-b3ac2c462ed6)，我认为这是学习如何编码的最好方法。在我看来，另一个很好的选择是编写和发布 Chrome 扩展，这甚至可能比克隆项目更容易，同时可能对您的投资组合产生更大的影响。在本文中，我将向您介绍我从开始到结束获得 Chrome 网上商店发布的扩展的过程。

# 为什么选择 Chrome 扩展

在我们开始开发 chrome 扩展之前，我想给你一些理由，告诉你为什么应该考虑在你的投资组合中加入这样一个项目

## 1.练习你的普通 JavaScript

对初学程序员的一个更常见的建议是，在进入框架之前，要很好地掌握普通的 JavaScript。我认为这是一个很好的建议。要编写一个 Chrome 扩展，你最有可能使用普通的 JavaScript(尽管有一些变通方法也可以使用框架)。这是一个锻炼您的普通 JavaScript 的极好项目。

## 2.学会与浏览器更亲密

Chrome 或其他浏览器是我们每天都要交互的强大工具。对网络开发者来说更是如此，因为这是我们发布应用的环境。写一个扩展会帮助你对浏览器的工作原理有更深的理解，让你成为一个更好的开发者。

## 3.已发布的应用程序影响更大

将扩展发布到 Chrome 网络商店相对容易，这对你的投资组合来说是一件好事。一个已发布的应用程序是一个很好的投资组合，因为它向潜在雇主展示了你能够发布工作项目。

# 这个想法

在开始编写扩展之前，我们需要一个想法。

有一天，我的一个同事问我如何快速编辑网页内容，他不是一个精通技术的人。他需要一种方法来更改文本内容，以快速模仿他作为团队中开发人员的反馈的一些想法。我告诉他可以在检查工具中将页面上的 [contenteditable](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/contenteditable) 属性设置为 true。我的同事对此欣喜若狂，但是作为一名开发人员，每次都必须使用 inspector 工具来做这件事的想法让我感到困扰。这也是我想到[可编辑](https://chrome.google.com/webstore/detail/editable/mmekofhljljfembnembkfbbmamnimoph)的原因——我想让自己和其他人更容易切换页面上的内容可编辑属性。

对于那些需要了解扩展功能的人，我的建议是查看浏览器控制台上提供的 API，这些 API 对于普通用户是不可用的。就像我对 contenteditable 所做的一样。另一个例子是这个[视频速度控制器](https://chrome.google.com/webstore/detail/video-speed-controller/nffaoalbilbmmfgbnbgppjihopabppdk)扩展。尽管今天你在互联网上看到的几乎每一个视频都有一个速度控制器——视频速度控制器 API 允许更精细的速度变化或超过许多控制器的 2 倍限制——这就是这个特殊扩展如此有用的原因。

# 编写扩展

一旦你有了自己的想法，你现在就必须实际地扩展。我不会在这里详细讲述我是如何编写代码的，而是留给你 Github repo 的链接。如果你需要 chrome 扩展开发工作流程的介绍，请查看我的文章[如何开始使用 Chrome 扩展](https://jl978.medium.com/chrome-extensions-for-beginners-46019a826cd6)。

[](https://github.com/JL978/editable-page-extension) [## GitHub-JL 978/可编辑页面扩展

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/JL978/editable-page-extension) 

# 准备您的扩展以供审查

下一步，你需要有一个完整的 Chrome 扩展。为了准备发布你的扩展，首先，你需要通过这个[链接](https://chrome.google.com/webstore/developer/dashboard)创建一个 Chrome 网络商店开发者账户。一旦您创建了您的帐户，将您的扩展打包成一个. zip 文件，然后点击仪表板右上角的新项目按钮并上传文件

![](img/a9427d454b6220d082ef7d8ebbaf701d.png)

点击您刚刚添加的新行，我们现在将开始填写 Chrome 商店所需的所有必要信息，以便发布您的扩展。在商店列表选项卡上，您需要填写哪些字段是相当明显的。请注意，在这一步，您将需要一个 128x128 png 的扩展图标图像。

![](img/95d66a5080d07eaa0ae3ccb04e269d3f.png)

现在是这个过程中更令人困惑的部分。在您填写完上面的字段后，您仍然不能将其发送以供审阅。这是因为您需要在 privacy practices 选项卡中填写另一个表单，您可以从左侧导航栏导航到该表单。

在这一页上，您首先需要填写您的扩展的目的，这可以是一句简短的描述。

![](img/4686ffb38ea971cc1d9fd82dfbda0469.png)

下一部分是权限证明——它将列出您在清单文件中设置的所有权限，并且您必须证明为什么您的扩展需要特定的权限才能工作。这是我遇到最大麻烦的部分——我的扩展被拒绝，因为我列出了太多不必要的权限。因此，您应该仔细检查以确保您只拥有您需要的权限。

![](img/f417cda6abcd198de10f955a2b72de5c.png)

最后，勾选最后所有必要的框，现在您应该能够提交您的扩展以供审查

# 评论和出版

点击“提交以供审查”后，您所要做的就是等待。如果您的扩展被接受，那么它将自动发布。如果没有，你会在几天内看到你的延期被拒的原因。根据我的经验，反馈间隔大约是 48 小时。因为我上面提到的权限问题，我的扩展被拒绝了 3 次，所以在你根据反馈做出改变后，不要害怕继续尝试提交审查。

# 结论

就是这样。创建一个扩展并将其发布到 app store 上实际上非常简单。如果你想在 Chrome 网上商店查看我的扩展，你可以在这里找到它。如果你最终创建并发布了一个扩展，请在下面的评论中分享它。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)