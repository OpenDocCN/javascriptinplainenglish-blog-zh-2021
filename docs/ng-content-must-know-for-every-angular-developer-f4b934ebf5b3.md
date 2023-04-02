# “ng 内容”简要指南:每个 Angular 开发人员的必备知识

> 原文：<https://javascript.plainenglish.io/ng-content-must-know-for-every-angular-developer-f4b934ebf5b3?source=collection_archive---------3----------------------->

## 如何在 Angular 中用“ng-content”实现内容投影？

![](img/4349687f4efc99b99a3e8a2b27ed942b.png)

Working with Content Projection using “ng-content”

**Angular 中的内容投影**是一种在其他组件中插入内容的方法。它还可以用来使组件可重用和更加动态。

在本文中，我们将讨论如何替换和传递一些 HTML 内容给组件。让我们看看下面的例子来理解这个概念:

[https://gist.github.com/Mayankgupta688/d2e32ee7f5a17220a9d244012094536c](https://gist.github.com/Mayankgupta688/d2e32ee7f5a17220a9d244012094536c)

在这个例子中，我们需要在已经指定了“h1”标记之后替换一个给用户的称呼消息。对于不同的用户，称呼消息可以不同。其中一个用户可以有“

## 你好 Mayank，来角会话

## ”；对于另一个用户，我们可以显示“

### 欢迎客人，选择时段

### ”。

消息可以根据用例的不同而变化，在组件呈现时，我们没有任何固定的 HTML 标签或数据。

# 此问题的可能解决方案:

1.  一种选择是考虑组件内部可能存在的所有场景，并实现**逻辑来表示每个场景**。但是在这种情况下，组件会变得越来越复杂。在提供的模板中会有很多业务逻辑。
2.  根据组件需求创建**多个组件。用户可以根据需要拥有多个组件。但是在这个场景中，我们会有多个组件。**
3.  最好的选择是在 Angula r 中使用**内容投影。在下面的例子中，我们将看到内容投影的实现。**

# 在 Angular 中实现内容投影

可以使用“ng-content”实现内容投影。在下面的例子中，我们将看到实现内容投影是多么容易。

在这个例子中，我们可以看到“”被添加到组件中。现在让我们假设我们想要在相同的位置替换一些文本。我们可以在显示组件时传递 HTML 内容。下面我们可以看到 HTML 内容是如何被替换的。

[https://gist.github.com/Mayankgupta688/90a9efa455ff6458fe82c54e5fd5b606](https://gist.github.com/Mayankgupta688/90a9efa455ff6458fe82c54e5fd5b606)

我们可以在上面的 HTML 中看到，我们将不同的内容发送到同一个组件，这样，我们可以从创建的同一个组件中获得多个输出，从而使我们的组件“可重用”。

感谢您的阅读！

*更多内容看* [***说白了. io***](http://plainenglish.io/)