# JavaScript 中的 8 个有用的数组函数(带代码片段)

> 原文：<https://javascript.plainenglish.io/8-useful-array-functions-in-javascript-with-code-snippets-b8d5222bcab?source=collection_archive---------12----------------------->

*你现在应该真的知道这些了。*

![](img/5863a0ac6455086827b1c5245a7c3aa1.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/list?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

JavaScript 从一开始就有数组。它是一个非常有用的对象类型，允许我们创建任何类型的元素列表。子数组、购物清单或表格中的数据都可以来自数组。

我不会在这里详细讨论数组，我假设您知道它们是如何工作的。然而，当您在不同的场景中实际使用数组时，数组类型中内置的一些函数会非常有用。

# 一些和所有

有时，您想要检查数组中的元素是否符合任何预设的测试。这个测试应该是一个函数的形式。如果你愿意，这可以是一个箭头函数。它应该为测试引入一个参数。`some`函数寻找至少一个通过测试的元素，而`every`只在所有值都通过测试时返回`true`。

# 串联

可以用`+`操作符连接字符串，但是不能用数组连接。我们可以使用[扩展运算符](/the-three-dot-syntax-in-javascript-e812f6839fd7)，或者我们可以使用`concat`函数。我们可以在一个参数中给出我们想要添加到调用函数的数组中的数组。

# 长度

最重要的功能之一(实际上只是一个值)是`length`值。它返回数组中元素的数量。如果数组有从索引 0 到 4 的值，它将返回 5，因为它有五个元素。这在创建传统的`for`循环时非常有用。

# 包含

数组中另一个非常重要的任务是检查数组中是否包含特定的值。您可能想看看用户是否是素食者，或者食谱中是否有某种成分。该函数将返回一个布尔值，具体取决于是否在数组中找到了该值。

# 查找和查找索引

`find`和`findIndex`功能非常相似。我们通过对函数的测试，就像用`some`一样。该函数将返回通过测试的第一个值，对于`findIndex`，它将返回通过测试的第一个元素所在的索引。

# 地图

`map`函数是一个非常著名的函数，它简单地对数组中的每个元素应用一个给定的函数。它将返回一个新的数组。这对于创建 React 元素列表非常有用。

# 过滤器

过滤数组是另一个有很多使用案例的基本功能。你必须给它提供一个函数。如果一个元素通过了测试，它将被包含在新数组中，否则它将不会被包含在新数组中。

# 为每一个

除了使用实际的`for`循环，您还可以使用内置在数组中的`forEach`函数。它将为数组中的每一项执行一个函数。它基本上将`for(i=0;i<arr.length;i++)`语法缩短为`arr.forEach()`。这是一种非常优雅的循环数组的方式。您可以在函数中输入项目和索引参数。

# 结论

使用数组可能很有趣。也可能很恐怖。但前提是你不知道如何与他们共事。幸运的是，它们非常容易掌握，有了这些函数，在代码中处理数组时就没有什么可担心的了。

非常感谢您的阅读，祝您度过美好的一天。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)