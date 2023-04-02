# 提高 JavaScript 的 7 个鲜为人知的技巧

> 原文：<https://javascript.plainenglish.io/7-little-known-techniques-to-improve-your-javascript-20a9e870a5fe?source=collection_archive---------2----------------------->

## 世界上最著名的编码语言的隐藏宝石

![](img/51141885490a8c686a91ef47c00a15fe.png)

Photo by [KOBU Agency](https://unsplash.com/@kobuagency?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

JavaScript 简单易学，但很难掌握。一方面，语言是直观的。一个门外汉在半小时内就可以完成一个点击按钮的功能。另一方面，这种语言包含许多潜在的怪癖和可能性，只有在长期使用后才会显露出来。

在编写 JavaScript 的几年后，我仍然经常发现新的、更有效的方法来编写相同的功能。为了帮助你找到“JavaScript”这个宝藏，这里有 7 个技巧可以让你的 JavaScript 代码更有冲击力。

## 1.速记无效过滤

使用`filter()`过滤空值，如`null,` `undefined`或空字符串是大多数开发人员都知道的技术。但是你知道你可以简化这个方法吗？

`Filter`接受一个函数作为其参数。如果你从`Boolean` [对象包装器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)中发出`new`关键字，它的行为就像一个将给定值转换成布尔值的函数。因此，如果布尔对象包装器作为函数传递给一个`filter`，它会将所有的 all 值转换成`false`，并从列表中删除它们。好优雅！

## 2.用数字分隔符格式化数字

编码通常涉及到与数字打交道。通常情况下，它涉及到与相当多的人打交道。当在电子表格中工作时，大数字用点分隔符整齐地样式化，例如`1.000.000`，以提高可读性。但是在 JavaScript 中，一个大数字的各个部分似乎是用胶水粘在一起的。

但是有希望！请看[数字分隔符](https://github.com/tc39/proposal-numeric-separator)。第四阶段建议让你用下划线格式化大数字。模糊数字的日子已经一去不复返了。

## 3.组合数组/对象析构

[解构](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)本身已经不能被归类为“隐藏的宝石”了。这种技术允许您将数组和对象中的值直接赋给变量，节省了大量的代码。

但是你知道数组和对象的析构可以合并在一个赋值中吗？假设您有一个由`people`个对象组成的数组。您只对数组中第一个人的年龄感兴趣。通过结合这两种类型的析构，获取所需的信息变得轻而易举。

## 4.忽略数组析构中的值

使用数组析构，可以直接将数组值赋给变量。但有时并不需要数组的所有成员。您可以用一个简单的逗号来忽略它们，而不是将它们赋给未使用的变量——这是一个糟糕的做法。

## 5.在对象析构期间重命名变量

当你析构一个对象时，变量名应该默认匹配对象键。当对象关键字清晰并且没有命名冲突时，这种解决方案就足够了。但是有时对象键是模糊的，或者在当前作用域中已经存在同名的变量。

通过在析构赋值中重命名变量，可以很容易地解决这类问题。这是通过在原始键的名称后写一个冒号后跟新名称来实现的。

## 6.直接链接 await 子句

链接是在不调用新变量的情况下应用多个顺序方法的技术。例如，对一个数组应用一个`filter`和一个`map`方法，而不在两个操作之间推断一个新的变量。

当一个承诺进入游戏领域时，我经常看到这种链条断裂。必须等待 promise 的结果，一个新的变量被调用，它作为新链的起点。

然而，在履行承诺时开始一个新的链条并不是必须的。只需将一个`await`语句放在大括号中，就可以直接访问承诺的结果。

## 7.从箭头函数直接返回一个对象

JavaScript 中的箭头函数已经存在一段时间了。他们的适应现在是广泛的。大多数人还知道，arrow 函数的结果可以直接返回，不需要实际的`return`语句。只需从函数体中省略花括号，结果就会隐式返回。

但是这种技术如何应用于应该返回对象的箭头函数呢？因为对象是用花括号括起来的，所以从函数体中省略它们会导致错误。

别担心，这个问题有一个优雅的解决方案。只需将对象放在大括号中，就可以隐式地返回它。

火车已经到达了它的最终目的地。你已经通过了七站来提高你的 JavaScript。希望你在这个过程中学到了一些东西！你喜欢这篇文章吗？更多有趣内容请**关注我**。

**资源**

*   布尔对象包装:[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
*   数字分隔符:【https://github.com/tc39/proposal-numeric-separator 
*   析构:[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Operators/destructing _ assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*