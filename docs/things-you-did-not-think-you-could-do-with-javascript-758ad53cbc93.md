# 你认为用 JavaScript 做不到的事情

> 原文：<https://javascript.plainenglish.io/things-you-did-not-think-you-could-do-with-javascript-758ad53cbc93?source=collection_archive---------4----------------------->

阅读一些您可以用 JavaScript 做的惊人的事情

![](img/dfc2196a05ba270a27851c13ed0d9b51.png)

Photo courtesy of Jacqueline Brandwayn from Unsplash

*原载于*[*https://fek . io*](https://fek.io/blog/things-you-did-not-think-you-could-do-with-java-script)*。*

我经常惊讶于人们用 JavaScript 作为语言编写的一些软件。当 JavaScript 在 1995 年首次推出时，它被许多人认为是一种“玩具”语言。那时，Java 被认为是一种严肃的语言，带有可以在网页上运行的“Java 小程序”。

从那时起，JavaScript 已经在许多不同的地方实现，包括微控制器、服务器应用程序甚至桌面应用程序。还有许多不同的引擎可以使用，因此 JavaScript 基本上可以在任何地方运行。

![](img/c9c199bb9a8416a1e758716754621d8f.png)

我最喜欢的定律之一是博客作者兼软件工程师杰夫·阿特伍德的阿特伍德定律。**阿特伍德定律**规定:任何*可以*用 JavaScript 编写的应用，*最终都会*用 JavaScript 编写。我对可以用 JavaScript 编写的应用程序感到震惊。在我看来，这意味着你认为必须用 C 或其他低级语言编写的应用程序可以用 JavaScript 编写。

# 图像处理

信不信由你，你可以用 JavaScript 做图像处理。有许多你可以使用的库和工具，但是有一个是用纯 JavaScript 编写的，它叫做“Jimp”。Jimp 的名字类似于“Gimp”开源应用程序，它允许你进行简单的转换，比如调整大小、应用过滤器和转换成其他文件格式。看看下面这个例子；

# 编程机器人

是的，机器人。不仅有运行 JavaScript 的微控制器，还有许多不同的 NPM 模块，可以用来控制传统的微控制器，如 Raspberry Pi 和 Arduino。

## 强尼五号

Johnny-five 已经被移植到几乎所有的微控制器板上。只需将你的 Arduino 连接到电脑上，你就可以运行 JavaScript 代码来控制你的硬件项目。相当于“Hello-World！”微控制器的程序是使 LED 灯泡闪烁。这里有一个例子，告诉你如何使用 Johnny-five；

# 系统脚本

虽然许多人用 Bash 或 Python 等语言编写所有的系统脚本，但您可以用 Node.js 编写系统级脚本。

假设您有一个任务，需要清除或删除一个文件夹的内容，这可以通过使用`exec`函数执行命令来完成。下面是这个函数删除一个文件夹的例子；

# 机器学习和人工智能

机器学习在现代计算任务中变得越来越重要。使用先进模型的多层神经网络正被用于从自然语言处理到创造车辆的自动驾驶。

大多数构建机器学习应用程序的框架都倾向于集中在 Python 社区，但也有一些可供 JavaScript 开发人员使用。

## Brain.js

Brain.js 是一个 JavaScript 框架，可以在 Node.js 和浏览器中工作，并可以使用 GPU 加速。它使用一个名为`headless-gl`的本机模块来支持 GPU。它还依赖于 Python 2.7。

## TensorFlow.js

TensorFlow.js 基于谷歌的 TensorFlow 库。TensorFlow 是一个用于机器学习的端到端开源库。

像 Brain.js TensorFlow.js 既可以在浏览器中运行，也可以在 Node.js 中运行，它可以运行预先训练好的模型，也可以重新训练现有的模型。

# 编写原生移动应用

是的，原生移动应用。有许多框架可以用来创建基于 JavaScript 的本地应用程序。

## 反应自然

可能这些原生框架中最流行的是`React Native`。该框架由脸书推出，使用 React 应用程序框架来构建应用程序，但结合了 JavaScript 桥来呈现和控制原生组件。

这个框架不像 Cordova 或 PhoneGap 那样是 WebView 的包装器，而是一个真正的本地实现。他们甚至创建了自己的 JavaScript 引擎，可以在 Android 和 iOS 上运行，名为 [Hermes](https://engineering.fb.com/2019/07/12/android/hermes/) 。

## 原生脚本

像 React Native 这样的 NativeScript 允许开发者编写原生应用，但你可以使用多个不同的框架，包括 React、Angular、Vue.js 或 Svelte。

NativeScript 还附带了一个命令行工具，您可以使用它来基于您选择的框架的模板创建新项目。

## 科尔多瓦

Cordova 是 PhoneGap 的开源版本。这个框架允许开发人员使用他们的技能构建 HTML/CSS/JavaScript 应用程序，以便在 WebView 中重用这些应用程序。该框架只是将基于 HTML 的应用打包到一个本地 WebView 中。它使用 iOS 中的 WKWebView 和 Android 中的 WebView 控件。这些打包的应用程序可以像本地应用程序一样发布到本地应用程序商店。

# 编写视频游戏

许多人过去认为 3D 第一人称射击游戏必须用 C++之类的语言编写，但几年后，Emscripten 展示了如何将这些类型的游戏移植到浏览器中运行。

我看到的第一个 Emscripten 示例之一是一个用 C++编写的游戏中的 3D 第一人称射击游戏。这些类型的项目帮助激发了 WebAssembly 的创建。

WebAssembly 为编译器制造商提供了一个目标，可以使用一种叫做`WASM`的低级二进制格式将几乎任何程序移植到 JavaScript 运行时。

也有一些 JavaScript 框架允许你用纯 JavaScript 构建游戏，比如 [Kaboom.js](https://kaboomjs.com/) 。

虽然有许多游戏框架，Kaboom 致力于让游戏变得有趣和快速。它包括对精灵，字体和着色器的支持。

# 连接到乐器

JavaScript 让网络开发者可以利用大量的网络应用编程接口。其中一个更有趣的 Web APIs 是通过 Web-MIDI 接口连接和控制乐器。

Web-MIDI API 允许开发人员连接和控制数字乐器。查看这篇关于[在浏览器](https://www.keithmcmillen.com/blog/making-music-in-the-browser-web-midi-api/)中制作音乐的文章。

# 结论

很难想到一个不能用 JavaScript 编写的应用程序。尤其是现在有了 WebAssembly 这样的工具，看起来不可能的应用程序现在可以在 JavaScript 运行时中运行。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)