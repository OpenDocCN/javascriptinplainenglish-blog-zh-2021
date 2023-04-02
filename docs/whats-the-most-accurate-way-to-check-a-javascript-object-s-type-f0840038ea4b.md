# 检查 JavaScript 对象类型最准确的方法是什么？

> 原文：<https://javascript.plainenglish.io/whats-the-most-accurate-way-to-check-a-javascript-object-s-type-f0840038ea4b?source=collection_archive---------9----------------------->

![](img/acf4fb247a3a12c1a39318fb69933114.png)

Photo by [Sergei Akulich](https://unsplash.com/@sakulich?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在许多情况下，我们需要检查 JavaScript 对象的数据类型，因为它是动态的。

在本文中，我们将看看检查 JavaScript 对象类型的最准确的方法。

# 对原始值使用 typeof

我们应该使用`typeof`来检查除了`null`之外的原始值

例如，如果我们有:

```
console.log(typeof 1)
console.log(typeof '')
console.log(typeof true)
console.log(typeof 1n)
console.log(typeof undefined)
console.log(typeof Symbol())
```

我们使用`typeof`来获取数字、布尔值、bigints、`undefined`和符号的类型。

因此，我们得到:

```
number
string
boolean
bigint
undefined
symbol
```

从控制台日志中。

由于`typeof null`返回`'object'`，我们不能用它来检查一个表达式是否返回`null`。

# 使用 Object.getPrototypeOf 获取对象的原型

我们可以用`getPrototypeOf`方法检查对象的原型。

例如，如果我们有:

```
const o = {}
const proto = Object.getPrototypeOf(o);
console.log(proto === Object.prototype);
```

然后控制台日志记录`true`，因为一个对象文字继承自`Object.prototype`。

我们只是用`Object.getPrototypeOf`方法传入获取原型的对象。

如果我们从构造函数中创建了一个对象，我们可以做同样的检查。

例如，我们可以写:

```
const o = new Date()
const proto = Object.getPrototypeOf(o);
console.log(proto === Date.prototype);
```

检查`o`是从`Date`构造函数创建的。

这也应该记录`true`，因为`o`是通过实例化`Date`创建的。

# 结论

我们应该使用`typeof`来检查原始值的类型。

我们可以使用`Object.getPrototypeOf`方法来检查对象的原型。

*更多内容请看*[***plain English . io***](http://plainenglish.io)