# TypeScript 4.4 —新增功能？

> 原文：<https://javascript.plainenglish.io/typescript-4-4-whats-new-e8274e8d911d?source=collection_archive---------11----------------------->

JavaScript 和 TypeScript 的粉丝们，让我们一起来吧，因为 TypeScript 的新版本来了！和往常一样，TypeScript 4.4 提供了一些令人惊叹的新特性。让我们一起来发现它们吧！😆

![](img/a0a262264cb6baba3bd113085246fa51.png)

# 别名条件和判别式(类型保护变量)的控制流分析

这个听起来很奇特也很复杂，但是让我用尽可能简单的方式解释给你听！

在 TypeScript 中，我们通常希望根据变量的类型有不同的行为。假设我们想写一个函数，或者打印一个字符串两次，平方数字，或者如果它是另一种类型就返回参数。

在当前版本的 TypeScript 中，您需要使用如下的 if 语句编写一个类型保护。

在每个 if 语句内部，TypeScript 知道 arg 的类型是 string 或 number。这样做很好，但我们的问题来了，如果要提取类型保护到一个额外的变量，像这样呢？

Valid way of working in TS 4.4

在 TS 的早期版本中，这段代码不起作用，但在 TypeScript 4.4 中它是一种有效的工作方式！🥳

# 在 Catch 变量中默认为`unknown`类型

好的，对于那些喜欢使用试抓块的人来说，这是个好消息！在 TypeScript 4.4 之前，catch 块中的错误将自动属于类型`any`。

Example from the official blogpost

TypeScript 4.4 引入了新的`--useUnknownInCatchVariables`标志，它的功能与您想象的完全一样。启用此标志时，catch 块中的默认错误类型将是未知的。虽然这听起来没什么大不了的，但它提供了很多可能性。

由于未知类型，我们能够缩小传递的错误类型。看看这个来自官方博客的例子。

Example from the official blogpost

# 精确的可选属性类型

我将使用官方博客文章中的例子来解释这一点，因为这是一个非常清晰的例子！

Example from the official blogpost

这意味着在以前的 TypeScript 版本中，您可以显式地创建一个年龄为`undefined`的对象。
这当然不是我们对可选属性的期望。我们希望可选属性要么是一个数字，要么不存在于对象中

TypeScript 4.4 用`--exactOptionalPropertyTypes`标志解决了这个问题。如果指定此标志，将会发生以下情况。

Example from the official blogpost

# 更多细节，请！

正在寻找这些特性的更详细的解释或其他新内容吗？查看[官方博客](https://devblogs.microsoft.com/typescript/announcing-typescript-4-4/)！

度过严格意义上的一天！😉

*更多内容请看*[***plain English . io***](http://plainenglish.io/)