# 如何在 Vue.js 中使用插槽

> 原文：<https://javascript.plainenglish.io/how-to-use-slots-in-vue-js-f509eec1fb39?source=collection_archive---------15----------------------->

## 正确使用插槽—用一个例子解释。

![](img/f3f1e399cbdb3862017232171ca2db29.png)

Photo by [Christina @ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 什么是插槽？

当我们想要呈现一些从父组件传递到子组件的数据时，插槽是非常重要的。

与道具不同，插槽有很大的不同，并且很容易在应用程序中实现。

插槽还使我们能够根据我们希望呈现的内容和位置来呈现不同的信息。

根据 dev Mozilla，<slot>的说法， <slot>HTML 元素——Web 组件技术套件的一部分——是 Web 组件中的一个占位符，你可以用自己的标记填充它，这样你就可以创建单独的 DOM 树，并把它们放在一起。</slot></slot>

## **属性**

该元素包括全局属性。

名称—插槽的名称。

命名槽是一个带有名称属性的<slot>元素。</slot>

简而言之，插槽为我们提供了将数据从父组件无缝传递到子组件的特权，而无需使用 props。

## **如何使用插槽**

实现插槽的使用非常简单，只需将插槽放在接收数据的子组件中。

slot 是 Vue 中的保留关键字。JS 所以一切都应该很好。

看看下面的代码片段。

我们有一个父组件，它向内部名为 ***HelloWorld*** 的子组件传递一些信息。

我们如何将信息呈现到我们的子组件中？

请记住，我们正在将一些数据传递给子组件，而这些数据最初并没有被呈现。

为了呈现我们作为插槽传递的数据，我们必须在子组件***“hello world***”内部声明接收数据以访问插槽。

检查下面显示的代码片段。

因此，如果我们检查我们的开发服务器，您将看到我们从父组件传递的数据现在正在呈现。这就是老虎机的工作原理。

## **命名插槽**

通过插槽传递的数据有时会有不同的值，我们可以给它们分配不同的插槽名称( ***命名插槽*** )。

当您希望呈现通过不同实例上的插槽传递的不同信息时，会出现这种情况。

看看下面显示的代码片段。

这里我们将 ***标题*** 和 ***副标题*** 作为两个不同的插槽传递给 HelloWorld 子组件。请注意我们是如何使用名称 slot 属性为它们分配不同的插槽名称的。

如果我们想将信息呈现到 ***HelloWorld*** 子组件中，现在该怎么办。

从上面的代码片段中，我们传递了指定的插槽并相应地呈现它们。

这是实现使用命名槽的一种简单得多的方法。

在 Vue.js 中有很多关于插槽的使用，我们刚刚介绍了插槽的基础知识。

如果你想知道更多关于老虎机的信息，请点击下面的链接。

## **资源:**

Vue.js [***文档。***](https://v3.vuejs.org/guide/component-slots.html)

## **结论**

当您希望将动态数据从父组件传递到子组件时，Vue.js 插槽非常重要。

我希望这篇文章对你学习老虎机的基础知识有所帮助。如果你认为其他人可能会觉得这篇文章有帮助，请不要犹豫，分享出来。

## **更多内容:**

[](/10-useful-css-tips-and-tricks-every-developer-should-know-4d8b2a5dcea1) [## 每个开发人员都应该知道的 10 个有用的 CSS 技巧和窍门

### 改善前端开发过程的有用 CSS 技巧列表。

javascript.plainenglish.io](/10-useful-css-tips-and-tricks-every-developer-should-know-4d8b2a5dcea1) [](/5-projects-you-can-build-in-a-week-that-will-get-you-hired-c9e88c17753b) [## 你可以在一周内完成 5 个项目，让你被录用

### 如何建立一个基于项目的编程组合，给招聘人员留下深刻印象并吸引他们，让你被聘用。

javascript.plainenglish.io](/5-projects-you-can-build-in-a-week-that-will-get-you-hired-c9e88c17753b) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)