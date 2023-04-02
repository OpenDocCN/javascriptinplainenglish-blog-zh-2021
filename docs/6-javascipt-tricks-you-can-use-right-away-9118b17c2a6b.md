# 6 个可以立即使用的 JavaScipt 技巧

> 原文：<https://javascript.plainenglish.io/6-javascipt-tricks-you-can-use-right-away-9118b17c2a6b?source=collection_archive---------7----------------------->

## *代码更智能，而不是更难！*

![](img/b69fed810a295ae6888e735e4a79338a.png)

Photo by [Tim Mossholder](https://unsplash.com/@timmossholder?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/learning?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

JavaScript 在越来越多的地方被使用，并且还在不时更新。既然更新了，就有新的功能和新的方法来实现某些编程目标。

其中一些功能可能需要 polyfills 或其他库，如 Babel，以确保所有代码都能在最老的浏览器上正常运行。

让我们回顾一些有用的功能。

# 1.传播算子

[传播算子](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)太有用就不说了。它允许扩展诸如数组或字符串之类的可迭代对象。这对于添加新值非常有用。

这非常有用，我已经用过几次了。主要用于更新 React 中的状态。

# 2.设置对象

[Set 对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)是 JavaScript 中的一种新对象类型，可用于创建无重复的数组。当您希望拥有一个可以使用非唯一数组快速创建的唯一列表时，这很有用。

当独特的价值观很重要时，我曾亲自使用过几次。语法很容易记住，集合甚至有更多的功能，如`.has()`函数，用于检查集合是否有特定的值。

# 3.三元运算符

[三元运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)是一个简写的条件运算符。这对于根据其他条件设置值很有用。在 React 中非常有用，例如，如果所有数据都已加载，则根据条件设置`View`。

它比使用常规的`if`要短得多，如果没有嵌套的话，可读性也很好。我一直在用这个，尤其是在 React 或 React Native 中编写 JavaScript 时。

# 4 .模板文字

[模板文字](https://developer.mozilla.org/nl/docs/Web/JavaScript/Reference/Template_literals)是 JavaScript 中字符串的一种形式。它们是用反勾(```)而不是普通的引号写的。它们接受使用`${expression}`的表达式，并且可以跨越多行。

我开始每次越来越多地使用这些。对于编写查询很有用，基本上是 GraphQL 查询的标准。

# 5.那个？操作员

那[？操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)或可选的链接操作符是一个有用的操作符，用于检查一个值是否已经设置，并在设置后继续操作。

我已经写了无数的`if`语句来检查一个值是否已经被设置，这肯定会有助于解决这个问题。

# 6.那个？？操作员

[nullish 合并操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)是一个检查左边的值是否为`null`的操作符，如果是，它将返回右边的值。

当值还没有被加载时，这在空检查或返回一个`loading`字符串时可能非常有用。

我还没有使用这个特定的操作符。我最近了解到它，它似乎足够有趣，可以使用。语法没那么奇怪。我可以肯定地看到有人认为这是一个空支票。

# 结论

JavaScript 作为一种语言正在以前所未有的速度发展。至少从我开始学起。每天我都发现新的有趣的方法来解决问题或完成任务，这些方法更容易编写，执行更快，两者兼而有之，或者只是有点古怪。

有没有你已经用过的或者你以前从未听说过的运算符？我确实学到了一些新的。

总之。非常感谢您的观看，祝您愉快。