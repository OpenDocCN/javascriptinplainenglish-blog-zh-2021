# JavaScript 中的数据类型——奇怪的部分

> 原文：<https://javascript.plainenglish.io/data-types-in-javascript-the-weird-part-151e8fc3f1f3?source=collection_archive---------13----------------------->

![](img/9e313823e473a4a747bcd6a7a1e0c0e1.png)

Photo by [heylagostechie](https://unsplash.com/@heylagostechie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你对编程有一段时间的了解，你就会知道什么是数据类型，以及为什么它们在每一种编程语言中都很重要。

但是如果你不知道数据类型，那么它就是你存储在变量中的数据类型(值)——就这么简单。让我们看一个例子。

```
**const** name = 'someone';    *// data type is* ***string***
**const** num = 101;           *// data type is* ***number***
**const** isAlive = true;      *// data type is* ***boolean***
```

因此，让我们深入研究数据类型并探索它们。

JavaScript 有两种数据类型:**原语** *和* **非原语。**

# 让我们来看看基本的数据类型

> **原始**数据类型是一种仅包含一个特定**值的类型，它可以是字符串、数字或布尔值，如上例所示。**

这里有一个例子:

```
console.log(**typeof** 10);     *//number*
console.log(**typeof** true);   *//boolean*
console.log(**typeof** "sdf");  *//string*
console.log(**typeof** 10.5);   /*/number*
console.log(**typeof** false);  *//boolean*
```

# 现在，让我们看看非原始数据类型

> **非原语**数据类型是包含**数据集合**的类型，该数据可以是**多种类型** : *原语*或*非原语。*

在 JavaScript 中，对象是最重要的**非原语**数据类型。众所周知，对象是 JavaScript 的准系统，所以我们将在另一篇文章中讨论它们。现在，为了理解非原始数据类型，让我们检查一下它们。

让我们来看一个例子:

```
**const** obj = { a: "apple", b: "ball" };
console.log(**typeof** obj);  *//****object***
```

# 更多的数据类型—

除了原始和非原始数据类型，JavaScript 还有另外三种数据类型。

# 1.功能

在任何编程语言中，以及在 JavaScript 中，我们最常用的是函数。

该函数有自己的数据类型，称为 ***函数。***

```
**const** whoAmI = (who) => {
console.log(`I am ${who}`);   ***// I am No one***
};
whoAmI('No one');
console.log(**typeof** whoAmI);   ***// function***
```

# 2.不明确的

它只是表示**值**是**而没有将**赋给一个变量。

```
**let** name;
console.log(**typeof** name);   ***//undefined***
```

# 3.空

数据类型 null 表示没有值-空。

```
**let** name = null;
console.log(**typeof** name);   **//null**
```

> *你可能会混淆* **未定义** *和* **空** *。但是有一个简单的解释。未定义的是* **隐式的** *，意思是我们不用设置值(或者错误值)，JavaScript 自动获取。而在 null 的情况下，它是* **显式** *，这意味着我们必须像上面的例子一样自己设置它。*

# 好吧！但是奇怪的部分呢？

在数据类型的上下文中，我可能会说 JavaScript 在某些方面很奇怪。到目前为止，我已经看到了 JavaScript 的一些怪异之处，比如:

## 1.内置构造函数的怪异之处

在 JavaScript 中，我们有一些内置的构造函数来定义变量的数据类型(不应该使用)，比如字符串、对象、日期等。

看看下面的代码:

```
console.log(**typeof** String);  ***//function*****const** place = **String**("somewhere");
console.log(typeof place);   ***//string*****const** fruit = new **String**('fruit');
console.log(**typeof** fruit);   ***//object***console.log(**typeof** Date);   ***//function*****const** now = new **Date**();
console.log(**typeof** now);   ***//object*****const** date = **Date**;
console.log(**typeof** date);  ***//function***
```

## 2.null 的怪异

```
console.log(**typeof** null); ** //object****const** name = null;
console.log(name);   **//null**console.log(**typeof** name);   **//object**
```

## 3.物品的怪异

```
console.log(**typeof** Object);   ***//function*****const** item = ['a', 'd'];
console.log(**typeof** item);   ***//object*****const** obj = { a: "apple", b: "ball" };
console.log(**typeof** obj);   ***//object***
```

所以，这就是关于 Javascript 数据类型及其怪异之处的全部内容。还有一些我还没有提到的用例。所以，如果你想了解它们，你可以自己写代码，自己探索，当你发现其他东西的时候发表评论。

最后，JavaScript 很奇怪，但这就是我喜欢 JavaScript 的原因。在未来的内容中，我们将探索更多关于 JavaScript 及其怪异之处。

目前就这些。下一集再见！

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)