# JavaScript 是动态语言的两个原因

> 原文：<https://javascript.plainenglish.io/2-reasons-why-javascript-is-a-dynamic-language-f896d6fbe405?source=collection_archive---------7----------------------->

## 它不像 Java 那样是静态语言

![](img/7eea0761f38f7235a0a238e28cd69f29.png)

Photo by [Greg Rakozy](https://gregrakozy.com/)

计算机语言不是静态的就是动态的。JavaScript 是动态的，这是因为这种语言非常灵活。JavaScript 将允许开发人员采取有问题的、不安全的和令人困惑的行动，这些行动会使您的完全功能性的代码显得草率 MDN Web 文档是这样描述它的。

JavaScript 的 ES6 发布了“使用严格”或[严格模式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)来对抗这种灵活性的一小部分。然而，即使去掉了严格模式的灵活性，JavaScript 仍然是一种非常灵活和动态的语言。

# 首先，变量。

在 JavaScript 中，变量是用关键字声明的:let、const 和 var。与其他语言不同，开发人员不会将数据类型赋给变量。变量不是严格意义上的整数、浮点数、布尔值、字符串或空值。事实上，在 JavaScript 中我们可以做到以下几点:

```
let a = 6;
a = "Kyle";
a = false;
```

编码人员可以给同一个变量赋予不同数据类型的新值。太不可思议了。

除了缺少数据类型之外，在 JavaScript 中，程序员甚至不需要在使用变量之前声明变量。

```
name = "Kyle";
console.log(name);
var name;
```

在上面的代码中，变量声明是在变量被使用后进行的。其他语言如 C、C++和 Java 不允许这样做。此外，在 JavaScript 中，这种语言甚至不需要任何变量声明。由于[提升](https://medium.com/@kyledeguzmanx/3-ways-javascript-hoisting-affects-your-code-a6a93626c600)，这是允许的。

```
name = "Kyle";
console.log(name);
```

这也是完全成立的。没有使用关键字(let，var，const ),也没有变量声明。

# 第二，错误

对于其他语言，如 Java，编译器会在执行代码之前检查源代码并扫描错误。在 JavaScript 中，这种情况不会发生。

JavaScript 将在运行时执行代码并定位错误。如果您的代码在中途包含 TypeError 或 ReferenceError(或任何错误),那么只有当编译器在执行过程中遇到该错误时，您才会发现。

如果您在没有不断测试和调试的情况下一行行地编写代码，您可能很难找到错误的来源。此外，如果您确实收到了一条错误消息，您只知道编译器到达了那个错误。如果在那个错误之后有多个错误，那么只有在修复了当前的错误并再次运行之后，才能发现这个错误。

如果你有更多 JavaScript 是动态语言的理由，请告诉我！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)