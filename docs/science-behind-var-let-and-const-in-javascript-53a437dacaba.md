# JavaScript 中为什么有三种声明变量的方法？

> 原文：<https://javascript.plainenglish.io/science-behind-var-let-and-const-in-javascript-53a437dacaba?source=collection_archive---------12----------------------->

## JavaScript 中“var”、“let”和“const”背后的科学

![](img/e187a692377e52dd14dd4e8149530c7a.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) : Edited by Thushal Kulatlake

在我的第一篇文章中(见这里的)，我们讨论了什么是 JavaScript，关于 JavaScript 的著名历史，关于 ES5 和 ES6 的一些基本区别，JavaScript 的单线程行为和 JavaScript 异步行为背后的科学。这些是每个 JavaScript 开发人员在接触 JavaScript 之前都应该知道的核心概念。因此，在本文中，我们将讨论变量声明在 JavaScript 中是如何工作的，以及“var”、“let”和“const”之间的一些关键区别和相似之处。在整篇文章中，你会明白这些是什么意思。

所以让我们开始吧😉。

## “变”、“让”、“常”之美

和其他编程语言一样，JavaScript 也有一种叫做“变量”的东西。变量只是给一个内存位置(内存中的一个小位置)取一个名字，这样我们就可以用它在内存位置存储数据。例如，在 Java 编程语言中，变量可以通过使用原始数据类型来声明，如“int”、“float”、“double”、“string”等。所以，如果我们声明一个' int '变量，我们只能在内存空间中存储整数值。

令人惊讶的是，在 JavaScript 中，变量是用原始数据类型声明的**而不是**。相反，我们使用“var”、“let”和“const”来声明变量。原因是，由于 JavaScript 是一种动态编程语言，变量的数据类型将取决于我们在运行时(程序执行)赋予它的任何值。举个例子，如果我们声明一个变量为 var x，那么如果我们在运行时给它赋一个整数值，变量 x 的数据类型就变成了' int '。这在 Java 中是做不到的，因为它不是一种动态编程语言。

![](img/64bc450fd2fd17a7d18586c600e3781c.png)

VAR = LET + CONST? 🤔 (image source:- [Reddit](https://i.redd.it/fryh34q1kmt31.jpg) )

所以，我们知道，“var”、“let”和“const”可以用于 JavaScript 中的变量声明。所以现在你可能会有一个问题，如果 JavaScript 是一种动态语言，为什么我们使用 3 种类型的变量声明？我们可以只使用一种变量声明类型。有区别吗？嗯，是的，它是。两者是有区别的。接下来让我们逐一详细讨论。

## VAR —“我们的老朋友！”

在我之前的文章中(你可以在这里访问)，我们讨论了 ECMAScript 5 (ES5)和 ES6，它们是 JavaScript 语言的基础。因此，在 ES6 (ES2015)推出之前，开发人员在 JavaScript 中使用“var”进行变量声明。“let”和“const”这次没有介绍。因此，到那时，“var”是唯一用于声明变量的关键字。

作为一些例子，

根据用法，使用“var”声明的变量可以是全局范围的**或函数范围的**。所以现在你可能会想什么是“范围”呢？简单地说，作用域意味着代码中可以使用变量的区域。如果一个变量是全局作用域的，那么这个变量可以在程序的任何部分使用，如果一个变量是功能性(局部)作用域的，那么它只能在代码的特定区域使用。所以，这些“var”变量可以兼而有之。

举个例子，我们把作用域当做一个函数。如果“var”变量是在函数外部声明的，那么它的作用域就是全局的。这意味着在函数块外用“var”声明的任何变量都可以在整个程序的任何部分使用。如果“var”变量是在函数中声明的，那么它的作用域就变成了函数性的(局部的)。这意味着它是可用的，并且只能在该函数中访问。

“var”变量也可以重新声明和更新。

那么，为什么“var”声明变得越来越不受欢迎。“var”声明存在一些问题。我们用一个例子来理解一下。

因此，在上面的例子中，由于“times > 3”条件返回 true，所以“greeter”变量将被替换或更新(在编程界，我们称之为“重新定义”)。如果您有意想要重新定义“greeter ”,这并不是问题，但是如果您没有意识到变量“greeter”之前已经定义过了，这就成了问题。如果您在代码的其他部分使用了“greeter ”,您可能会对得到的输出感到惊讶。这将导致你的代码中出现许多错误。这就是为什么使用“let”和“const”是更可取的。

## 让—“新常态”

“let”声明是随着 2015 年 ES6 的发布而引入的。这个“let”变量由开发人员使用，它消除了“var”声明中的问题，这是目前 JavaScript 中声明变量的首选方式。

【让】是**块的范围。**块是由两个花括号{}限定的一段代码。花括号内的任何内容都是一个块。因此，在带有“let”in 的块中声明的变量只能在该块中使用。让我们看一个例子。

因此，正如您在上面的示例中看到的，if 条件内的 console.log 语句将显示“改为 say hello 条件外的 console.log 语句将显示为“hello is not defined”。这是因为“hello”变量不能在 if 块之外访问，因为它是块范围的。

“let”可以更新，但不能重新声明。就像“var”一样，用“let”声明的变量可以在其作用域内更新。与“var”不同，“let”变量不能在其作用域内重新声明。

所以，下面就行了。

```
let greeting = “say hi”;greeting = “say hello instead”;
```

下面将返回一个错误。

```
*let greeting = “say hi”;**let greeting = “say hello instead”;*
```

但是，如果在不同的作用域中定义了同一个变量，则不会出现错误。这两种情况被视为不同的变量。

## CONST—“我是不可避免的！”

这也是 ES6 规范和“let”一起引入的。“let”和“const”的区别在于，在“const”中，我们维护常量值(不变的值)。

“Const”也像“let”一样在**块范围**内。但是“const”不能更新或重新声明。如果我们声明一个变量为“const”，下面就做不到了。

所以，每一个“const”声明，都必须在声明的时候初始化。

对于用“const”声明的对象，这种行为有些不同。🤔虽然不能更新“const”对象，但可以更新该对象的属性。这意味着我们不能向对象添加新的属性，但是我们可以更新现有的属性。下面是一个“const”对象。

## 结论

这就是“var”、“let”和“const”背后令人惊叹的科学。一定要练习编码，这会让你势不可挡。感谢您的阅读，我希望您发现这是有用的。请继续关注更多类似的文章。在那之前，

和平。✌😉