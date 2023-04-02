# 生活会改变你使用反作用力钩子的方式

> 原文：<https://javascript.plainenglish.io/iifes-can-change-the-way-you-write-the-useeffect-hook-in-react-a5cb5d69d14a?source=collection_archive---------5----------------------->

我们将学习如何使用 IIFE(立即调用的函数表达式)在 useEffect 钩子中编写异步 JavaScript。

![](img/f4f2172a95e3bd062a4a71e93edaa71d.png)

在我看来，IIFE(立即调用的函数表达式)是 JavaScript 中一种鲜为人知的语法。基本上，生命是一个在定义后立即执行的函数。你们很多人现在可能会想，这有什么意义。如果你只是想在之后立即执行一个函数，为什么还要使用它呢？这个问题的答案很简单，因为我们可以在其中使用 async-await 语法。

下面是一个生活的例子。

# 如何在 React 中使用 IIFE 的 useEffect 钩子

你们中的许多人可能已经知道，在 React 中不能向 useEffect 钩子传递异步函数。因为生活迂回曲折，我们仍然可以。让我们通过在 React 中编写一个全功能演示来看看这是如何工作的。我将使用 CodeSandbox 来演示这一点，以便您可以修改和试验这方面的代码。

您将在 useEffect 钩子的代码中看到，我们能够通过使用 IIFE 来使用 async-await 语法。真的是这样。就这么简单。IIFE 释放了在 useEffect 钩子中使用 async-await 语法的潜力。

# 结论

IIFE 是一个非常强大的 JavaScript 编码实践，对于许多不同的用例来说非常方便。事实证明，useEffect 也不例外。

*更多内容看*[***plain English . io***](https://plainenglish.io/)