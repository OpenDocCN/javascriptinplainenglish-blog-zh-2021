# 2021 年在 JavaScript 中克隆对象的最有效方法

> 原文：<https://javascript.plainenglish.io/the-most-efficient-ways-to-clone-objects-in-javascript-2021-c8e4d04096a5?source=collection_archive---------5----------------------->

![](img/231bdd56cf43671ffb089ae0bb8ee039.png)

Photo by [Daniel Cheung](https://unsplash.com/@danielkcheung?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/star-war?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

克隆对象是 JavaScript 领域中最常用的操作之一。在本文中，我们将深入探讨 JavaScript (Node.js 和 Browser 环境)中存在的不同类型的克隆。我们还将讨论在 JavaScript 中浅层和深层克隆对象的最有效方法。

> 📝已经有很多关于这个主题的博客文章、文章和堆栈溢出线程。本文是我试图把互联网的集体知识整合成一个易于理解和参考的总结。

让我们潜水吧🏄‍♀️

# **本土深度克隆**

本机深度克隆在 Node.js 中被称为“结构化克隆”。该功能在浏览器中不可用。结构化克隆除了 JSON 支持的数据类型之外，还支持另外一组数据类型。下面是它支持的其他[数据类型](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm#supported_types)列表。以下是本机深度克隆的示例:

structured clone

# JSON.parse/stringify—数据丢失的克隆

当您不关心数据丢失时，Good ol' `JOSN.stringify()`是最常用的克隆对象的方法，或者对于您的用例，浅层克隆就足够了。这里有一个简单的例子

shallow copy

当要复制的对象具有复杂的嵌套数据或函数时，应用 JSON.strigify()会导致数据丢失。下面是一个在 JSON.strigify()上发生数据丢失的示例。

在样本上面的 ***攻击*** 功能将不会被复制。

# 扩展操作-浅层克隆

扩展操作是在 ES6 中克隆对象的最简单方法。这种方法也会发生数据丢失。然而，因为这是 ES6 的固有特性，所以它比 JSON.strigify()更有性能。

> 在这里检查基准[。](http://jsben.ch/#/bWfk9)

下面是一个使用 spread 运算符进行克隆的示例

# 对象. assign()

Object.assign()是一种 ES6 方法，它允许浅层克隆 simmilar 扩展操作。

# 使用 lodash 库进行深度克隆

如果您正在寻找一种可靠的深度克隆方法，并且不介意使用第三方库，那么 lodash 可能正是您正在寻找的解决方案。

# 具有自定义功能的深度克隆

最后，我们可以推出自己的深度复制对象的功能。我从堆栈溢出中找到了下面的代码片段，并一直在我的项目中使用它。

如果您关心各种克隆功能的性能，我强烈建议您看看[下面的线程](https://jsben.ch/KVQLd)。我希望这篇文章有用。今天就到这里🙂，直到下次

# **参考文献**

[https://developer . Mozilla . org/en-US/docs/Web/API/Web _ Workers _ API/Structured _ clone _ algorithm # supported _ types](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm#supported_types)

[https://stack overflow . com/questions/122102/最有效的深度克隆对象的方法是什么/5344074#5344074](https://stackoverflow.com/questions/122102/what-is-the-most-efficient-way-to-deep-clone-an-object-in-javascript/5344074#5344074)

【https://www.npmjs.com/package/lodash.clonedeep 