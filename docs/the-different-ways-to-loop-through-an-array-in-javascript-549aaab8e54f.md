# JavaScript 中遍历数组的 8 种不同方式

> 原文：<https://javascript.plainenglish.io/the-different-ways-to-loop-through-an-array-in-javascript-549aaab8e54f?source=collection_archive---------8----------------------->

探索 JavaScript 中遍历数组的不同方法。

![](img/c26602f4b8389c7f9513a496df2e5045.png)

Photo by [Boitumelo Phetla](https://unsplash.com/@writecodenow?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我们第一次开始学习编程时，我们被教导如何使用一个`for loop`来遍历一个数组。有趣的是，对于每种编程语言来说，实际上有不止一种方法可以遍历数组。

在这篇文章中，我将汇编一个 JavaScript 中循环数组的方法列表。

让我们首先初始化我们将在下面的例子中使用的数组。

# 1.for 循环

遍历数组最经典的方式。

# 2.for-of 循环

# 3.for-in 循环

注意:**不推荐**使用这个方法来循环遍历一个数组。为什么？

*   不保证索引会按顺序返回([https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Statements/for)...在#array_iteration_and_for 中...在](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in#array_iteration_and_for...in)。
*   它将遍历所有可枚举属性及其原型的可枚举属性(参见下面的示例)。

# 4.while 循环

# 5.do-while 循环

注意:下面的代码假设数组中至少有一个元素。但是，如果数组为空，我们将得到`*undefined*`。

为了安全起见，我们应该这样写。

# 6.forEach 循环

# 7.地图

此方法在迭代一个数组以转换为另一个数组而不改变原始数组时非常有用。

如果你不介意输入几个字符，我们也可以这样写。

# 8.过滤器

此方法在使用布尔表达式过滤数组时非常有用。

# 先进的

## 将 forEach、map 和 filter 链接在一起

我们也可以将 **forEach** 、 **map、**和 **filter** 链接在一起，在一行代码中一起进行过滤、转换和循环。

下面的代码将

1.  过滤 myArray 以移除`a`(使用**过滤器**)。
2.  转换过滤后的数组以追加`character:`(使用**映射**)。
3.  打印转换后的数组(使用 **forEach** )。

现在我们有了。我希望你已经发现这是有用的。感谢您的阅读。如果你喜欢这篇文章，记得关注我的更多更新！

如果您喜欢这篇文章，您可能也会喜欢:

[](https://weikangchia.medium.com/7-different-ways-to-loop-through-an-array-in-java-e0d04245c6aa) [## Java 中循环数组的 7 种不同方式

### 探索遍历数组的不同方法

weikangchia.medium.com](https://weikangchia.medium.com/7-different-ways-to-loop-through-an-array-in-java-e0d04245c6aa) 

如果你还不是一个中等会员，并且想成为一个，点击这里。

[](https://weikangchia.medium.com/membership) [## 用我的推荐链接加入媒体-伟康

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

weikangchia.medium.com](https://weikangchia.medium.com/membership) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)