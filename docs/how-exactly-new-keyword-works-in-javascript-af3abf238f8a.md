# JavaScript 中的“new”关键字到底是如何工作的？

> 原文：<https://javascript.plainenglish.io/how-exactly-new-keyword-works-in-javascript-af3abf238f8a?source=collection_archive---------16----------------------->

![](img/496e05feeec271a5873d58ef4c6fe7f6.png)

对于程序员来说，知道编程语言的确切工作方式是非常重要的，而不是假设他们的工作方式。这可以让你以不同的方式处理问题，并提出有效的解决方案。我要说的是，它给了你对代码的信心。

编程语言中有许多强有力的关键字，程序员没有从它们那里得到太多，因为他们误解了它们。比如 JavaScript 中的“this”关键字就是一个非常强大的关键字。遗憾的是，很多程序员并没有意识到这一点。顺便说一句，如果你是其中之一，我强烈推荐你阅读我关于以下主题的文章:

[](https://zmjdev.medium.com/how-exactly-this-keyword-works-in-javascript-78497c8279c6) [## “this”关键字在 Javascript 中到底是如何工作的

### 你应该对 Javascript 中的函数和对象有很好的理解，并对动态…

zmjdev.medium.com](https://zmjdev.medium.com/how-exactly-this-keyword-works-in-javascript-78497c8279c6) 

接下来，我假设您对 JavaScript 中的对象有很好的理解。如果你误解了 JavaScript 的一些特性，你总是会在代码中遇到错误。“新”这个关键词不在其中。几乎每个程序员都使用“new”关键字来创建类的实例，他们很少遇到问题。这篇文章的目的是展示“新”这个关键词是如何让我们的生活变得更加容易的。

您可以用各种方式创建对象。其中之一是通过使用函数。我们来看看是怎么做的。我们声明一个返回对象的函数。通过查看下面的代码片段，您将理解这意味着什么。

由于上面的函数“createEmployee”返回一个对象，我们称之为工厂函数。在第 8 行，我们在“employeeFunction”对象和一个由“Object.create()”返回的空对象之间建立了一个链接。然后在第 9 行和第 10 行，我们将参数赋给新创建的对象“newEmployee”的属性。然后我们把它退回去。

作为总结，我们

1.  创建了一个空对象
2.  建立了到“员工职能”的链接
3.  将给定的参数赋给对象的属性
4.  返回了对象

现在让我们来看看“new”关键字的作用。

新关键字做 4 件事:

1.  创建一个空对象
2.  建立到“CreateEmployee.prototype”对象的链接
3.  将创建的对象分配给此
4.  返回“this”(如果函数没有返回对象)

上面的代码片段几乎等于前面的代码片段。我说*几乎是*是因为在第一段代码中，我们链接到了“employeeFunctions”对象，但是在第二段代码中，我们链接到了“CreateEmployee.prototype”对象。这是唯一的区别。

我想你还记得我们做了四件事来创建和返回一个对象。“new”关键字为我们做了四件事。我们只需调用带有“new”关键字的函数。我们称新关键字“构造函数”调用的函数为函数。下面的代码片段显示了第 10 行是如何解析的:

这就是我们如何在 JavaScript 中创建类的实例。class 关键字可以被认为是构造函数的语法糖(这只是部分准确)。

如果您一直想知道原型对象是什么，我强烈建议您阅读下面链接的文章:

[](https://zmjdev.medium.com/deep-understanding-of-prototypes-in-javascript-367a81f98847) [## 深刻理解 javascript 中的原型

### 到这个故事结束的时候，你会对 __proto__ 和 prototype 有很好的理解。

zmjdev.medium.com](https://zmjdev.medium.com/deep-understanding-of-prototypes-in-javascript-367a81f98847) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)