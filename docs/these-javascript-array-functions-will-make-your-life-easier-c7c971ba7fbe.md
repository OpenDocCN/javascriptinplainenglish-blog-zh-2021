# 这些 JavaScript 数组函数将使您的生活更加轻松

> 原文：<https://javascript.plainenglish.io/these-javascript-array-functions-will-make-your-life-easier-c7c971ba7fbe?source=collection_archive---------10----------------------->

## 我每天都用这些，你呢？

![](img/5863a0ac6455086827b1c5245a7c3aa1.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/list?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

使用数组可能是一件痛苦的事情，尤其是当您没有合适的工具来完成这项工作的时候。有时，您会创建循环来完成 JavaScript 内置函数的任务。

我可以简单地列出数组方法，并将它们链接到各自的 Mozilla 网页，我会尝试提供逻辑用例的例子，并解释它们的功能。

许多这样的功能在诸如 LoDash 这样的库中可能更容易使用，但是出于一个很好的原因，我将保持它的简单和普通。了解你正在使用的编程语言比依赖库更有价值。

# 1.过滤器

过滤数组是能够轻松成功完成的最重要的任务之一。谢天谢地，香草可以帮助我们。

它根据项目是否通过传递给函数的测试来创建一个新数组。

我通常给出的一个技巧是使用匿名数组函数作为参数来减少所需的行数。

# 2.减少

[Reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 是对每个项目执行给定函数的函数。例如，用于将所有数组项相加。

另一个可能使用它的用例是计算给定数组中所有数字的平均值。

# 3.为每一个

函数对给定数组中的所有元素执行给定的函数。用于列出或记录所有项目。

这段代码记录控制台中的所有项目。但是有比调试更好的用例。这在某些情况下消除了对简单的`for`循环的需要，并赋予它更多的语法意义。

# 4.每个和一些

从技术上讲，这是两个独立的功能。`[.every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)`和`[.some()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)`意思相近，只有一点不同。

`every`函数检查数组中的所有项目是否都通过了给定的测试。在这种情况下，我们检查每个分数是否超过 5.5，以了解他们是否通过了一门课程。(艰难的历程，我知道)。

然而，`some`函数检查学生是否收到了至少一个 10 分。或者具体来说，它检查是否至少有一项通过了给定的测试。

# 5.包含

`[includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)`函数与`some`非常相似，但是它检查数组是否包含特定的*值*，而不是通过特定的布尔测试。

# 6.地图

没有`[map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)`函数，这样的列表是不完整的。`map`函数创建了一个新的数组，并在每一项上都调用了一个函数。

在这个例子中，我们传递一个将所有值三倍化的函数。您还可以在 React 中使用它来映射一组数据，以呈现一个列表或类似的东西。

# 结论

有许多函数可以在数组上调用。其中一些我每天都在使用。`every`和`some`功能对我来说是新的，我迫不及待地想使用它们。

请注意，其中一些功能可能需要聚合填充才能正常工作。谢天谢地，有很多方法可以做到这一点，在 Mozilla 上，他们为你提供了大部分的填充。

非常感谢您的阅读，祝您有美好的一天。