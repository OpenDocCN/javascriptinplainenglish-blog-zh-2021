# 我把 TensorFlow.js 塞进了一个 React 应用

> 原文：<https://javascript.plainenglish.io/i-stuffed-tensorflow-js-into-a-react-app-3fd8678019f5?source=collection_archive---------5----------------------->

## 以下是我对网络工作者的了解。

![](img/4ff5a9ff47304148521b8ea4fc4d6f03.png)

项目源代码在底部。
[https://autoyeai.com/](https://autoyeai.com/)

当我在道明银行的创新实验室工作时，我经常发现自己需要理解大数据。时间序列预测、图形遍历、图像分类，应有尽有。这些工具中的大多数都可以作为 Python 软件开发工具包使用，或者你需要将你的 AI 模型从以 Python 为中心的技术栈转换为 iOS 或 Android 原生模型。出于概念验证或用户测试的目的，在 AWS 上制作和部署一个快速 Flask API 来托管模型通常更有效。

但是如果我不想要后端或数据库的开销呢？我想到了一个项目的想法，这个项目正好需要:张量流模型的全 JS 实现。

我不想在这个项目中使用计算服务器的主要原因是:

1.  数据是静态的。没有网络事件。唯一的输入是一个模型的种子，我可以使用一个干净的源文本数据源提前训练它。
2.  这是我免费分享的一个玩具。如果项目不是一个实际的业务，我不想有 GPU 云计算服务器或长期运行的无服务器功能的开销成本。
3.  在测试期间，运行在 Python 上的 TensorFlow/Keras 模型比 TensorFlow.js 版本的训练迭代次数少得多，但产生 200 个字符的结果的实际时间同样缓慢。基于上一点，对结果质量的影响是最小的…至少以我对 NLP 和构建 ML 模型的了解。

有了这些，我训练了我的模型，并将其转换为 tensor-flow.js (tfjs)格式，并在我的 React web 应用程序界面中进行了测试。

我对 AutoYeAi.com 项目的解决方案是使用 LSTM 模型，这需要使用先前的结果渲染多个帧。它平衡了可预测性和随机性，为非结构化文本产生良好的结果。一个伟大的 MVP 让抒情一代工作。问题是每一帧都需要一段时间来渲染。在我的例子中，每个 tfjs 帧是一个字母，执行时间是累加的。

毫不奇怪，具有繁重计算的长时间运行的任务锁定了 javascript 事件循环。在速度较慢的设备上，这种情况更加明显，很容易导致网络浏览器崩溃。javascript 在 web 浏览器中的单线程特性显示了它的局限性。Chrome 会抛出错误 5 或 6(本质上是恐慌错误)，检查器会崩溃，窗口会崩溃。一切都崩溃了。甚至不要让我开始担心移动 web 浏览器会因为沉重的 tfjs 负载而崩溃。

显然，我需要更多的 CPU 线程，这样用户界面才不会锁定。

## 解决方案:网络工作者！

Web Workers 允许您拥有一个无头浏览器选项卡(本质上是一个看不见的选项卡)，它可以访问自己的 CPU 资源。

您在根文件夹中添加一个新的 javascript 文件，在我的例子中是 tfworker.js，然后向其中发送和发布事件。如果您曾经做过浏览器扩展，那么工作流类似于 options.js、background.js 和主内容页面之间的通信。它需要对基于动作调度器和事件监听器的系统进行重构，但是我得到了额外的线程！

这里有一个陷阱。新的 javascript 文件需要成为新的 web 包入口点，因为 web 工作者不能导入其他 javascript 包。幸运的是，[谷歌有一个很棒的包](https://www.npmjs.com/package/worker-plugin)可以让这变得更容易。另一个包， [react-app-rewired](https://github.com/timarney/react-app-rewired) ，让我在不牺牲伟大的 create-react-app 默认设置的情况下修改 webpack 配置。

这解决了我的线程问题，但仍会偶尔导致网络浏览器崩溃。工作线程将被锁定，并且在主选项卡关闭后它的执行将持续，这使得开发变得乏味。除了更多的代码优化，主要的解决方法是禁用 UI 输入，以防止多个张量流执行队列的建立。另一个解决方案是将整首歌曲生成的默认字符数量减少到几个小节，以供低端设备使用。生成的大量张量流帧将导致廉价 Android 手机更加不稳定。

说来奇怪，我的 iPad 比我的 MacBook Pro 快。

下一次，当您准备用 JS 进行大规模计算时，请让 Web 工作者尝试一下！这可能比部署 web 服务器更好。

看 AutoYe 在行动:【https://autoyeai.com/ 

![](img/0db71f38cb1e8c36216ea8037a970e1a.png)

# 资源

## 源代码:

[](https://github.com/FrankFlitton/autoyeai.com) [## GitHub-FrankFlitton/auto yeai . com:tensorflowJS Kanye West 歌词生成器和数据摄取…

### tensorflowJS Kanye West 歌词生成器和数据摄取管道。-GitHub-frank flitton/auto yeai . com:A…

github.com](https://github.com/FrankFlitton/autoyeai.com) 

网络工作者插件:[https://www.npmjs.com/package/worker-plugin](https://www.npmjs.com/package/worker-plugin)
React-app-rewired 包:[https://github.com/timarney/react-app-rewired](https://github.com/timarney/react-app-rewired)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)