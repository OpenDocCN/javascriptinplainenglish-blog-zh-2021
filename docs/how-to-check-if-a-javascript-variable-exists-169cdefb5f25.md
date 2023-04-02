# 如何检查一个 JavaScript 变量是否存在？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-javascript-variable-exists-169cdefb5f25?source=collection_archive---------12----------------------->

![](img/64918c0fa26c45182c4cfade0dd62e6e.png)

Photo by [Kyle Glenn](https://unsplash.com/@kylejglenn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 变量可以在不设置值的情况下声明。

它们也可以设置为`undefined`。

在本文中，我们将看看如何检查一个 JavaScript 变量是否被初始化或者它是否是`undefined`。

# 运算符的类型

检查 JavaScript 变量是否存在的一种方法是使用`typeof`操作符。

例如，我们可以写:

```
let x;
console.log(typeof x === 'undefined')
```

如果`x`没有初始化，那么它和设置为`undefined`是一样的。

所以`typeof x`返回`'undefined'`。

因此，`console.log`返回`true`。

# 虚假检查

我们还可以检查一个变量是否为 falsy，看它是否为 falsy 值，包括`undefined`、`null`、`''`(空字符串)、0、`NaN`或`false`。

真值是除这些值之外的任何值。

例如，我们可以写:

```
let x;
console.log(Boolean(x))
```

然后控制台日志记录`false`，因为`x`未初始化，所以是`undefined`。

由于`Boolean`将任何 falsy 值转换为`false`，这就是我们得到的结果。

同样，我们可以使用`!!`做同样的事情:

```
let x;
console.log(!!(x))
```

# 结论

我们可以使用`typeof`操作符或者`Boolean`函数来检查一个变量是否被初始化。

*更多内容请看*[***plain English . io***](http://plainenglish.io)