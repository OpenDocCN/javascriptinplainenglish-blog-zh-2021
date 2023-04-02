# 如何在 Vue.js 中使用道具

> 原文：<https://javascript.plainenglish.io/how-to-work-with-props-in-vue-js-f6912f8ac6f0?source=collection_archive---------9----------------------->

## 用 Props 向子组件传递数据。

![](img/f43c7305f5f61ae4f6040bb5e3232899.png)

Image by theTribe

Vue.js 的应用和组件结构相当惊艳。它还提供了一些惊人的功能。

在这篇文章中，我们将看看如何在 Vue.js 中使用和实现 props。

## **什么是道具？**

简单来说，props 就是 properties 的缩写。当我们想要将数据从父组件传递到其他子组件时，Props 是非常重要的。道具总是采取自上而下的方法。

也就是说，props 只能从父组件流向子组件，而不能从子组件流向父组件。道具也可以是各种类型如 ***字符串、数组、对象、数字、布尔、*** 甚至 ***函数。***

## **我们什么时候用道具？**

当构建动态网页时，以及当您想要访问其他组件的一些数据时，Props 非常有用。

Pros 还使传递其他组件所需的数据和信息变得更加容易。

因为道具很重要，所以它们的频繁使用有时会导致一个叫做道具训练的问题，这会使我们的程序在调试问题时读起来不干净。

通常认为，不要在许多组件层中传递过多的道具是一个好的做法。

## **如何实现道具的使用？**

让我们举一个例子，我们从一个 API 获取一些信息，并将数据存储到我们的程序中。

然后，我们将把信息从 API 传递给其他组件结构。

检查下面显示的代码片段。

从上面的代码片段中，您可以看到我们正在通过 API 获取一些信息，并通过 props 将数据传递到 Photos 子组件中。

请看一下我们是如何传递道具的。

要将数据作为道具传递，我们要么使用 ***v-bind*** 指令，要么我们可以使用 ***':'*** 符号来表明我们传递的数据是道具。

从代码片段中，您可以注意到我们正在遍历来自 API 的数据，并将相关的道具分配给 Photos 子组件。

## **如何注册组件内部的道具**

还记得我们将道具从父组件传递到照片子组件。

现在，为了访问传入的道具，我们需要在 Photos 组件中注册这些道具，这样我们就可以轻松地访问它们。

我们只是以数组的形式提供道具，并传入从父组件接收的道具。在下面的代码片段中，我们注册了名为: ***img、name、attrib、imgcap、*** 和 ***id 的属性。***

检查下面显示的代码片段。

您可以很容易地识别出我们是如何在子组件中注册道具的。

## **渲染子组件内的属性值。**

我们可以使用组件中的 ***小胡子*** 或 ***双花括号*** 轻松呈现组件中道具的值，如下所示。

在我们的例子中，我们将 ***name*** prop 的值呈现给我们的组件 UI。

## **资源**

Vue.js [文档](https://vuejs.org/v2/guide/components-props.html)

## **最终想法**

当您想要将一些数据从父组件传递到子组件时，Props 非常重要。

相反，确保适度使用道具，否则你可能会发现自己处于一个实施大量道具训练的场景中。

感谢您阅读本文到目前为止，如果您发现它有帮助，请不要犹豫与他人分享。

## **更多内容:**

[](/10-useful-css-tips-and-tricks-every-developer-should-know-4d8b2a5dcea1) [## 每个开发人员都应该知道的 10 个有用的 CSS 技巧和窍门

### 改善前端开发过程的有用 CSS 技巧列表。

javascript.plainenglish.io](/10-useful-css-tips-and-tricks-every-developer-should-know-4d8b2a5dcea1) [](/how-to-use-font-awesome-icons-in-react-229af382dfa0) [## 如何在 React 中使用字体出色的图标

### 了解如何在 React 中使用字体出色的图标。

javascript.plainenglish.io](/how-to-use-font-awesome-icons-in-react-229af382dfa0) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)