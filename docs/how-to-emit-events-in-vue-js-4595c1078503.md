# 如何在 Vue.js 中发出事件

> 原文：<https://javascript.plainenglish.io/how-to-emit-events-in-vue-js-4595c1078503?source=collection_archive---------13----------------------->

## 通过一个例子了解如何在 Vue.js 中发出事件。

![](img/bf8a33929b490c73fb1593028843395b.png)

Photo by [Daria Nepriakhina](https://unsplash.com/@epicantus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在执行一些前端任务时，指令和事件是一些令人惊叹的功能。

我们可以利用它们，根据特定的条件和流程，用它们制作一些很酷的东西。

在本文中，我们将看看如何在 Vue.js 中发出事件

举一个例子，您正在处理一个特定的项目，您想将一些参数甚至函数从子组件传递到父组件。

我们如何做到这一点？我们可以通过在 Vue.js 中使用 emit 事件来实现这一点。

举个例子，我们有一个子组件，在它上面附加了一个 click 事件，我们想在 click 事件上传递一个将从父组件执行的函数。

以下面显示的代码片段为例。

因为我们希望函数 ***deleteTask*** 在父组件中处理，我们可以简单地发出给定的函数，这样它就可以在父组件中运行。

我们可以重组代码，如下所示。请记住， ***$emit*** 将接受两个参数，第一个是要运行的函数，而第二个参数是将在函数中传递的给定参数。

从代码片段中，您可以看到我们正在将 ***deleteTask*** 和任务标题传递给父组件。

在父组件上，我们现在可以很容易地访问这个参数，并有效地处理我们的用例。

从上面的代码片段中，在 Task 子组件上，我们已经附加了一个 ***v-on*** 指令，并且我们已经传递了从子组件传递的函数。

现在，在我们的方法中，我们可以轻松地创建 ***deleteTask*** 函数，并在那里传递我们的逻辑。

这就是我们在 Vue.js 中散发和散发事件的方式

## **结论。**

感谢您的关注，希望这篇文章对您有所帮助。

如果你能与他人分享这篇文章，对我来说意义重大。

## **更读**

[](/how-i-would-learn-to-code-if-i-were-to-start-over-4fc1b5f62482) [## 如果重新开始，我将如何学习编码

### 如果我要重新学习编程，我的学习方法。

javascript.plainenglish.io](/how-i-would-learn-to-code-if-i-were-to-start-over-4fc1b5f62482) [](/how-to-create-a-toggle-button-in-vue-js-10fe76abf433) [## 如何在 Vue.js 中创建切换按钮

### 通过一个例子学习如何在 Vue.js 中制作一个切换按钮。

javascript.plainenglish.io](/how-to-create-a-toggle-button-in-vue-js-10fe76abf433) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)