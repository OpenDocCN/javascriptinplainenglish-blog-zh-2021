# 如何在 Vue.js 中创建切换按钮

> 原文：<https://javascript.plainenglish.io/how-to-create-a-toggle-button-in-vue-js-10fe76abf433?source=collection_archive---------13----------------------->

## 通过一个例子学习如何在 Vue.js 中制作一个切换按钮。

![](img/590c601e35c2c6abe765a7b96b3be6dd.png)

Photo by [Nikita Kachanovsky](https://unsplash.com/@nkachanovskyyy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue.js 很棒，它的学习曲线也很简单。学习构成 Vue.js 的一些核心原则，对理解其核心功能是惊人的。

通过构建和测试这个和那个，我们可以从分解事物和试图修复它们的过程中学到很多东西。

在本文中，我们将研究如何制作一个简单的切换按钮，从而在两个给定的状态之间进行切换。

首先，我们需要创建一个 Vue.js 项目。如果你不熟悉 Vue.js，那么你可以按照下面的说明安装一个新的 Vue.js 应用程序并开始编码。

## **安装** Vue.js **CLI。**

要安装 Vue.js，您必须安装 Vue.js CLI 来控制和安装我们将需要的各种 Vue.js 组件。

打开您的开发人员终端，运行下面显示的命令。

```
npm install -g @vue/cli
```

***-g*** 命令标志全局安装 CLI，以便您可以从计算机内的任何地方访问 CLI。这可能需要一段时间，请耐心等待。

## **创建我们的** Vue.js 应用程序。

现在，既然我们已经成功安装了 Vue.js CLI，我们可以使用命令轻松地创建我们的应用程序。

```
vue create <name of your project> -n
```

Vue.js 可能需要一段时间来创建您的应用程序并为您准备好一切，因此如果需要一些时间，请耐心等待。

***-n*** 命令标志用于防止为项目选择各种特性的默认弹出窗口。它将跳过所有这些，立即生成应用程序。

现在打开你的项目，进入 ***src*** 文件夹，打开 ***app.vue*** 文件。这是我们将要创建切换按钮功能的文件。

创建切换按钮功能。

现在，我们的代码示例应该类似于上面所示的代码片段。

我们有两个按钮，我们基于 ***isActive*** 状态有条件地呈现它们。

我们正在实现使用 ***v-if 指令*** 来有条件地测试和呈现下面显示的各个按钮。

同样，在按钮上，我们攻击了各种 ***@click*** 函数，这些函数将根据给定的按钮点击来设置和取消设置 ***isActive*** 状态。

这是我们在 Vue.js 中实现和创建切换按钮的最简单的方法之一。

# 最后的想法

感谢您阅读这篇文章并继续编码。

我希望这篇文章对你有所帮助，如果有，请不要犹豫，与其他可能从中受益的人分享。

## **更多内容:**

[](/how-i-would-learn-to-code-if-i-were-to-start-over-4fc1b5f62482) [## 如果重新开始，我将如何学习编码

### 如果我要重新学习编程，我的学习方法。

javascript.plainenglish.io](/how-i-would-learn-to-code-if-i-were-to-start-over-4fc1b5f62482) [](/vue-js-best-practices-you-should-adopt-3f3b3a8abace) [## Vue.js 您应该采用的最佳实践

### 使用 Vue.js 时的最佳实践

javascript.plainenglish.io](/vue-js-best-practices-you-should-adopt-3f3b3a8abace) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)