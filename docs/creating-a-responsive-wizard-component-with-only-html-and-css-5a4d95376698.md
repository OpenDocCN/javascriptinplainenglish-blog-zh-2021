# 仅用 HTML 和 CSS 创建响应式向导组件

> 原文：<https://javascript.plainenglish.io/creating-a-responsive-wizard-component-with-only-html-and-css-5a4d95376698?source=collection_archive---------8----------------------->

![](img/6d45d6b5bf617446457a85e915575426.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

向导组件基本上是一个组件，它显示了为了完成一个大任务而需要完成的一组小操作/步骤。例如，在线购买产品通常是一个多步骤的过程，包括首先选择产品，提供送货信息，付款，最后确认购买。

在这种情况下，一个设计巧妙的向导组件可以指导用户完成整个过程，还可以指示用户在该过程中所取得的进展。

在本文中，我们将讨论如何只用 HTML 和 CSS 创建一个响应式向导组件。

我们的向导组件将包含以下部分:

1.  计步器
2.  步骤标签
3.  进度条
4.  已完成步骤的复选标记

**那么，事不宜迟，我们开始吧。**

首先，我们将看看创建向导结构的 HTML。

Wizard component HTML structure

在上面的结构中，我使用了一个`<ul>`(无序列表)标签作为容器，向导中的步骤被添加为包含标签和步骤号的`<li>`(列表项)标签。

列表项将使用不同的样式类别，以显示步骤不同状态之间的差异，即步骤当前是活动的、已完成的还是处于待定状态。下面是我们将如何处理这些状态:

1.  默认情况下，所有的步骤将显示在一个挂起的状态，需要一个接一个的行动，因此他们没有任何特定的类。
2.  当前活动的步骤将拥有`active`类。这将是这一进程开始的第一步。
3.  当一个步骤完成后，它将拥有`completed`类。完成该步骤后，将显示复选标记而不是步骤计数器，表示该步骤已完成。
4.  当所有的步骤都完成后，它们都将拥有`completed`类，因此它们中的每一个都将显示复选标记。

> 在上面的代码示例中，我将前两步标记为`completed`，将第三步标记为`active`，这样我们可以清楚地看到一个步骤的所有状态之间的区别。

**现在，让我们添加向导需要的样式。**

Wizard component CSS (SCSS)

## 我们把上面的造型分解一下，详细讨论一下，好吗？

1.  我使用了`flexbox`布局，以便将它们水平并排堆叠在一起。
2.  我使用了`::before`和`::after`(伪元素)来创建将所有这些步骤相互连接起来的时间轴。`::before`用于显示一个步骤完成后的进度。
3.  选中标记是使用`step-num`元素的`::before`伪元素创建的，该元素默认情况下被标记为隐藏，但在一个步骤完成时会显示出来。
4.  `active`和`completed`类定义了当一个步骤进入各自的状态时将应用于`li`元素的样式。
5.  最后，我使用了一个媒体查询`@media only screen and (max-width: 768px)`来定位小型设备。这样，水平向导步骤将彼此垂直堆叠，并且还将垂直定位时间轴。

我们完成了！

> 请注意，在上面的例子中，标记不同状态的步骤的类是显式添加的。要动态添加这些类，您可以使用 JavaScript 并编写逻辑，说明如何以及何时在向导步骤中应用这些不同的状态。
> 
> 此外，时间线的样式是基于个人的选择和演示的目的。随意定制组件的样式。

**这是我们在本文中创建的向导组件的预览:**

Responsive wizard component preview on Codepen

## 结论

我希望这篇文章对你有用，它能帮助你创建一个你自己的向导组件。如果您有任何问题或意见，请随时添加到回复中，我会回复您。

***目前就这些。感谢您的阅读。***

***更多故事请*** [***关注我***](https://anishdhingra.medium.com/) ***上媒。***

*更多内容请看*[*plain English . io*](http://plainenglish.io/)