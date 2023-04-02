# ||和&&在 JavaScript 中不是“逻辑运算符”

> 原文：<https://javascript.plainenglish.io/and-are-not-logical-operators-in-javascript-5209981b7468?source=collection_archive---------11----------------------->

## 更恰当的名称是“选择器运算符”。

![](img/261cf48623a5a49a6e3c0ab43f51d4cb.png)

Photo by [bruce mars](https://unsplash.com/@brucemars?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/thinking?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

听我说完。

如果你已经用 PHP 或任何静态类型的语言编写了软件，你会知道任何表达式的值，包括`||`或`&&`都会返回一个布尔值。

输入 JavaScript。

逻辑运算符的名称并没有完全描述 JavaScript 中的`||`和`&&`的功能。一个更恰当的名称是*选择器运算符*。

这是因为，在 JavaScript 中，`||`或`&&`将返回两个表达式值中的一个(也是唯一一个)，而不是一个布尔值。

引用第 11.11 节 [ES5 规格](https://www.ecma-international.org/ecma-262/5.1/#sec-11.11)

> `&&`或`||`运算符产生的值不一定是布尔类型。产生的值将始终是两个操作数表达式之一的值。

请考虑以下事项:

惊讶吗？

`||`和`&&`运算符均对第一个表达式值(`a`或`c`)进行布尔测试。如果该值还不是布尔值(这里不是)，就会发生[到](https://www.ecma-international.org/ecma-262/5.1/#sec-9.2)的强制，从而可以执行测试。

对于`||`运算符，如果测试为真，则`||`表达式会得到第一个表达式值(`a`或`c`)。如果测试为假，则`||`表达式产生第二个表达式值(`b`)。

反之，对于`&&`运算符，如果测试为真，则`&&`表达式会得到第二个表达式值。如果检验为假，则& &表达式得到第一个表达式值。

让我们深入研究上面代码中的第一个和最后一个表达式，以便更好地理解:

在上面的表达式中，`||`操作符将首先检查第一个表达式值(`a`)是否属于布尔类型。如果不是，就会发生 ToBoolean 强制。`a` ( `10`)不是布尔型，因此，`a`会被强制为`true`，因为`a` ( `10`)是*真值*。

由于我们的测试为真，`||`操作符将返回第一个表达式值(`10` ) —而不是强制值(`true`)。

在上面的表达式中，`&&`操作符将首先检查第一个表达式值是否为布尔值，否则它将强制它。`c` ( `null`)不是布尔值，因此，它将被强制为`false`，因为`null`是 *falsy* 。

`&&`如果第一个表达式值为 falsy，则运算符返回第一个表达式值，如果第一个表达式值为 true，则返回第二个表达式值。由于`c` ( `null`)为 falsy，所以`&&`运算符会将其返回。

作为一名 JavaScript 程序员，请永远记住:

> 由`&&`或`||`运算符产生的值不一定是布尔类型。产生的值将总是两个操作数表达式之一的值。