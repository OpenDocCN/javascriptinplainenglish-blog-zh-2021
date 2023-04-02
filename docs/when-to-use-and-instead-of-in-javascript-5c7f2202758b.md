# 什么时候用&&和||代替？？在 JavaScript 中

> 原文：<https://javascript.plainenglish.io/when-to-use-and-instead-of-in-javascript-5c7f2202758b?source=collection_archive---------5----------------------->

![](img/0d25605928833cee506404251312c636.png)

Photo by [Christian Wiediger](https://unsplash.com/@christianw?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText).

## 逻辑 AND 和 OR 运算符实际上可以返回非布尔值。

作为一名软件开发人员，您肯定非常熟悉[无效合并操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)(?？).如果您不熟悉这个操作符，让我简单介绍一下它是如何工作的。

如果值 a 为空或未定义，则返回 b。否则，返回 a。

今天，我想将这个操作符与 JavaScript 中的另外两个操作符进行比较:逻辑 AND 操作符 ( & &)和逻辑 or 操作符 (||)。您可能也非常熟悉这两个操作符，但是您可能不知道它们在被类型强制的情况之外使用时实际上会返回非布尔值。

AND 和 OR 运算符是最常见的——或者，根据我的经验，几乎总是——要么与布尔值一起使用，要么在各种 if 语句中使用。

在上面的代码中，if 语句将两个非布尔变量强制转换为布尔值。1 和 2 都是真的，所以条件通过。

但是，当在类型强制情况之外使用时，逻辑 AND 运算符将返回一个操作数。

在上面的场景中，表达式返回数字 2，而不是您可能认为的布尔值。运算符的规则如下:如果值 a 为 true，则返回 b。否则，返回 a。

逻辑 OR 运算符的工作方式类似:

如果值 a 为真，则返回 a，否则返回 b。

让我们并排比较这三个运算符:

这三个操作符都有用例，但是大多数开发人员只使用 nullish 合并操作符。在大多数情况下，它是合适的操作符，但是在某些情况下，您可以使用逻辑 AND 或 or 操作符。

例如，nullish 合并操作符将只检查一个值是否为空或未定义，而不检查它是否为 [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) 。然而，JavaScript 开发人员经常需要检查一个值是否为“空”，比如一个为 0 的数字或者一个空字符串。

我经常看到类似这样的代码:

想象一下，一个前端开发人员有一个可选的输入字段，并且只希望处理真实的值，而不是空字符串或 0。他们通常会运行一个 if 语句来检查值是否正确，如果正确，就对其进行处理。

这段代码有点晦涩难懂，但你已经明白了要点。

可以使用逻辑 OR 运算符编写完全相同的代码，如下所示:

我们经常需要检查 JavaScript 中的真值，理解什么时候在 JavaScript 中使用逻辑 and 和 or 操作符可以帮助您用更少的代码做到这一点。