# 确定优秀开发人员的 5 个 JavaScript 面试问题

> 原文：<https://javascript.plainenglish.io/5-javascript-interview-questions-to-identify-outstanding-developers-859a71c3d7f?source=collection_archive---------0----------------------->

## 这些面试问题通过测试深入的 JavaScript 知识来帮助识别优秀的 JavaScript 程序员。

![](img/154f8546f4f0c732c03e8d32fe982371.png)

Photo by [Maranda Vandergriff](https://unsplash.com/@mkvandergriff?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/interview?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

JavaScript 最初是作为一种简单的脚本语言开始的。早些时候，开发人员使用 JavaScript 使他们的网站有点动态。如今，JavaScript 无处不在。我们可以用 JavaScript 构建单页 web 应用程序、移动应用程序、桌面应用程序、物联网应用程序、CLI 程序和 RESTful APIs。另一方面，作为 JavaScript 的标准规范，ECMAScript 经常给 JavaScript 带来改进和增强。

因此，我们现代的开发人员社区有很多 JavaScript 开发人员。如果一个特定的公司用 JavaScript 构建了一个高质量的产品，他们需要从最好的中雇佣最好的来保持他们的产品干净。在这个故事中，我将分享一些面试问题，以发现优秀的 JavaScript 程序员。这些实际上与现代语法无关，但是这些问题将测试深入的 JavaScript 知识。当我参加面试时，我经常问 JavaScript 开发人员这些问题。

## 吊装问题

**问题:**解释为什么下面这段代码在 JavaScript 环境中工作，即使这个方法不是最先声明的。

**回答:**在 JavaScript 中，函数声明被挂起。因此，上述`sayHello`方法将在代码执行前移到范围的顶部。因此，当 JavaScript 运行时执行`sayHello`函数时，它已经知道了函数声明。

## 异步递归

**问题:**用递归承诺实现众所周知的阶乘函数。您可以在传统的阶乘算法中递归调用该函数。但是，您必须在阶乘问题的异步版本中递归地调用 Promise。

**回答:**我们需要从阶乘方法返回一个无极，因为我们这里需要一个异步解决方案。因此，我们必须使用`resolve`回调来完成每个递归调用，而不是直接返回值。在这种情况下，我们必须根据输入参数`n`做出一连串的承诺。查看以下代码。

第一个 if 条件是异步递归方法的基本情况。else-block 使 promises 链类似于传统的阶乘函数的调用堆栈。

## 异步/等待问题

**问题:**当我们添加`async`关键字时，JavaScript 函数会发生什么？此外，我们如何使异步函数像全局范围的阻塞调用一样？

**回答:**当我们使用`async`关键字时，JavaScript 运行时会自动用承诺包装特定函数的代码。我们在函数中返回的内容将被自动解析。因此，该函数将始终返回一个 Promise 对象。

我们可以使用 await 将异步调用变成同步调用。我们应该在异步方法中使用`await`关键字。如果我们需要在全局范围内使用`await`关键字，我们可以创建一个立即调用的函数([life](https://developer.mozilla.org/en-US/docs/Glossary/IIFE))，如下所示。

## 简单的关闭

**问题:**解释下面的 JavaScript 代码是如何工作的。这里用的 JavaScript 原理是什么？

**答案:**`nAdder`函数返回一个函数，该函数返回一个给定值与父函数作用域内的值之和。当我们调用父函数时，我们可以为子函数求和使用的第一个变量赋值。同样，我们可以用子函数为求和提供第二个值。这个原则被称为 JavaScript 闭包。

## 神奇的功能

**问题:**写一个函数接受一个动态数量的参数。解释两种可能的方法。

**回答:**对于较老的 JavaScript 运行时，我们可以使用`arguments`对象。`arguments`对象包含一个提供给特定函数的参数数组。对于较新的 JavaScript 运行时(支持 ES6)，我们可以使用新的 rest 参数语法。查看下面的示例代码。

## 结论

如今，有许多 JavaScript 库和框架。事实上，许多公司使用它们来减少开发时间，而不是从头开始实现一切。然而，当所有人都在掌握现代 JavaScript 库时，一些科技公司正在深入研究 JavaScript 原则。因此，在大多数 JavaScript 面试中，我们会听到如下问题。

*   React 是什么状态？
*   Redux 和反冲是什么？
*   JavaScript 中的语法 *< randomSyntax >* 是什么？
*   JavaScript 中的数组方法*<randomArrayMethod>*是什么？

以上问题都是基于经验的。我的想法是，理解 JavaScript 核心概念(如承诺、异步/等待、闭包、上下文和提升)的开发人员比在特定 JavaScript 库中拥有多年经验的开发人员表现更好。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)