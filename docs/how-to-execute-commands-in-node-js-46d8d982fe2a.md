# 如何在 Node.js 中执行命令

> 原文：<https://javascript.plainenglish.io/how-to-execute-commands-in-node-js-46d8d982fe2a?source=collection_archive---------5----------------------->

## 了解如何在 Node.js 中运行外部命令

![](img/db6a512272489cc43ae13742e09ff629.png)

Image by Portswigger

Node.js 非常强大，因为它为我们提供了一个可以运行 JavaScript 文件和代码的运行时环境。

假设您想在 Node.js 中运行一些外部命令，比方说在某些情况下，您想在应用程序的某个特定点运行 git 命令。我们如何才能做到这一点？嗯，我们可以利用许多库来完成这项工作。

幸运的是，它很容易在 Node.js 中执行，不需要任何第三方库和包。在本文中，我们将了解如何在 Node.js 环境中运行外部命令。

## **子进程 _ 救援**

Node.js 有很多我们可以在盒子外面利用的模块。对于我们的例子，我们需要 Node.js 中的一个模块，称为 child_process。

Node.js 中的 child_process 模块非常强大，它使我们能够直接访问操作系统的功能。有了它，我们可以在系统上运行各种命令。

child_process 模块提供了四种不同的方式来创建和利用它们。这四种中我们有`***exec()***`*`***spawn()***`*`***fork()***`***和*** `***execFile()***`。**

**对于这一部分，我们将只关注 exec 组件。如果您想深入了解 child_process 的其他组件，可以查看这个 [***链接。***](https://nodejs.org/api/child_process.html)**

## *****exec()*****

**`exec()`采用以下语法。**

```
**child_process.exec(command[, options][, callback])**
```

**`exec()`语法如下:**

**`exec()`使用外壳执行命令。这非常方便，因为您可以直接在操作系统上运行各种命令。**

## ****exec()在行动****

**现在假设我们想在 Node.js 中的操作系统上执行一些命令。**

**对于我们这里的例子，我们将使用`exec()`在 Node.js 中执行一些 git 终端命令。**

**现在，如果您使用 Node.js 运行 JavaScript 文件，那么`***git - -version***`命令将会运行。**

**请记住，这个命令是一个 git 终端命令，只有在安装了 git 的情况下才能使用。**

**当您想要运行其他命令时，语法非常相似。**

## **结论**

**当您想在旅途中用 Node.js 执行一些任务时，它非常强大和方便。我希望你能从这篇文章中学到一些东西。**

**感谢您花时间通读这篇文章，希望对您有所帮助。**

## ****更多阅读****

**[](/how-to-auto-rename-files-with-javascript-a72f4b6f2528) [## 如何用 JavaScript 自动重命名文件

### 了解如何用 JavaScript 重命名文件

javascript.plainenglish.io](/how-to-auto-rename-files-with-javascript-a72f4b6f2528) [](/5-amazing-resources-to-ace-your-css-skills-cd11baee7714) [## 5 个惊人的资源来提高你的 CSS 技能

### 帮助您提高前端技能的资源

javascript.plainenglish.io](/5-amazing-resources-to-ace-your-css-skills-cd11baee7714) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)**