# 我如何使用 Blitz.js 和 CRON 自动化我的每周时事通讯

> 原文：<https://javascript.plainenglish.io/how-i-automated-my-weekly-newsletter-using-blitz-js-and-cron-4c38ec244762?source=collection_archive---------12----------------------->

![](img/74f136ee36966380773ab1ccf7a87a01.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我最近发现了 Blitz.js，喜欢这个框架让你构建应用程序的速度，但我最喜欢的部分是命令行工具。Blitz.js 有一个控制台，可以用来通过节点 REPL 环境运行预定义的查询和变异，这对于从命令行手动运行任务来说非常好，但在 CRON job 内部运行时就不太好了，因为它会接管正在运行的任何进程。

我有一份收集新闻故事的时事通讯，我想每隔一周自动发送这份时事通讯。我需要一个通过不使用 expect 命令的 bash 脚本启动的 CRON 解决方案，所以我开始研究 child_process 模块。

如果你是第一次接触媒体，你可以在这里注册来支持我的写作:

[](https://john-grisham.medium.com/membership) [## 阅读约翰·格里森姆的每一个故事(以及媒体上成千上万的其他作家)

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

john-grisham.medium.com](https://john-grisham.medium.com/membership) 

# 清除旧数据

Blitz.js 建立在 Next.js 的基础上，所以托管是灵活的，但对我来说，赢家是 Render.com。我并不隶属于他们，但在我尝试过的托管平台中，他们是最便宜、最容易建立的。这篇文章不会深入讨论如何使用 Render 进行托管，只需知道这是我设置 CRON 作业的主机。

Render 提供一个简单的 CRON 服务。我希望我的孩子一周做两件事。

1.  从我的数据库中删除超过 6 天的记录
2.  如果星期是奇数(每隔一周)，运行我的时事通讯自动邮件变异

我的 bash 脚本将是入口点，并将启动这些过程。

我使用 ts-node 调用这里的其他 Typescript 文件，这些文件将执行我想要完成的核心逻辑。让我们看看第一个。

该文件将使用带有自定义 stdio 配置的 blitz 控制台生成一个新进程。这个配置很重要，也是唯一适用于我的解决方案的配置。我一直遇到的问题是，一旦 blitz 控制台启动，它会搞乱我的主进程，并阻止我在控制台内运行进一步的命令。我们正在为父流程和子流程输入建立一种通信方式。父母可以告诉孩子做什么，反之亦然。至于输出和错误通道，我们分别将它们默认为主进程 stout 和 sterr。

我还告诉 blitz 进程通过错误事件处理程序记录任何错误。我使用一些实用方法来运行我的 clearOld 变异，这将从我的邮件数据库中删除旧记录。我还使用 Axel Rauschmayer 的 stringio 包来管理控制台执行流。

该文件将向新的子进程写入多个命令，然后结束流。完成后，我们将退出 blitz 控制台子进程。如果你感兴趣的话，我的 clearOld 突变是这样的。

# 发送简讯

bash 脚本的下一部分每隔一周运行一次自动邮件程序文件。该文件将从 Firebase 获取我的注册信息，并通过 Sendgrid API 向他们发送一组新闻故事。这里的子进程设置是相同的，唯一的区别是我有一些参数，我希望在运行这个文件时能够传递，我使用了盗版主题的命令行参数包 Yargs。

[](https://github.com/yargs/yargs) [## GitHub — yargs/yargs: yargs 是乐观主义者的现代海盗主题继承者。

### Yargs be a node . js library for heaties try ter parse opt strings Yargs 帮助您构建交互式命令行…

github.com](https://github.com/yargs/yargs) 

我也有一些实用的方法来制作一个带有 HTML 的临时文件，我将在发送时事通讯时加载它。这个 HTML 将作为我保存在另一个表中的新闻稿的模板。总之，所有这些都超出了本教程的范围，所以这里是自动邮件文件的基本代码。

# 结论

我希望这有所帮助。Blitz.js 很棒，开发起来很有趣，但是 CLI 也可以用于生成文件和文件夹之外，这带来了一些有趣的 CRON 作业解决方案。我发现这个控制台使用起来很简单，也很有趣，但是在试图通过 bash 自动运行命令的时候就有所欠缺。我的解决方案非常适合我的使用案例，如果我没有为我的时事通讯设定这样一个特定的目标，我会使用现有的电子邮件时事通讯解决方案。

本指南并不打算成为使用 blitz 控制台的 CRON 工作的分步解决方案，但它应该会给你灵感，让你知道使用这些技术可以自动化你的工作流程。如果你像我一样，需要其他 Saas 提供商提供的解决方案之外的解决方案，你可以使用 CRON 和一些额外的资源来创建你的自动化工作流。你觉得我的解决方案怎么样？是否有改进的空间或者我是否过度设计了它？如果你好奇的话，你也可以看看我为这个 CRON 任务创建的时事通讯。

[](https://echo-breaking-news.com) [## 媒体素养和新闻

echo-breaking-news.com](https://echo-breaking-news.com) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)