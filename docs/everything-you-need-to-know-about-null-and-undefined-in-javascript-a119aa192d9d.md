# 关于 JavaScript 中的 Null 和 Undefined，你需要知道的一切

> 原文：<https://javascript.plainenglish.io/everything-you-need-to-know-about-null-and-undefined-in-javascript-a119aa192d9d?source=collection_archive---------23----------------------->

## JavaScript 中的 Null 和 undefined 用例子解释它们的异同。

![](img/7d13e69f704ba5fd4efa9b467304e238.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Null 和 undefined 是用 JavaScript 编程时最常见的错误。这些错误可能很烦人，尤其是当你不知道它们之间的潜在差异时。

首先，使用这种编程语言有点困难。在这篇文章中，我们将看看 null 和 undefined 之间的根本区别。

Null 和 undefined 有很多相似之处，但它们之间有明显的区别。

## **相似之处**

null 和 undefined 错误都意味着它们对于您试图访问的变量没有任何值。

当您使用等号==来比较 null 和 undefined 时，将返回 true 值，但是当您使用三重等号===时，您将发现返回 false。
以下面的代码片段为例:

```
console.log (null == undefined);Trueconsole.log (null === undefined);False.
```

这仅仅意味着 null 和 undefined 不相等。
如果你检查 null 和 undefined 的类型，你会发现它们也不是截然不同的。Null 具有 object 类型，而 undefined 具有 undefined 类型。
看看下面的代码片段

```
console.log(typeof (null));objectconsole.log(typeof (undefined));undefined
```

## **空值**

对于空值错误，它具体意味着某个东西或变量没有特定的值。假设我们正在编写一些函数来查找对象列表，以搜索用户的特定输入，我们将设置相关函数，该函数将循环遍历条目列表，如果没有找到相关输入，我们可以编写一个返回函数来通知用户他们正在搜索的条目为空，这意味着没有找到，没有任何价值。这仅仅意味着该事物不存在于列表中。

## **未定义**

对于 undefined，它并不完全意味着没有值，而仅仅意味着变量或者你试图访问的任何东西已经被声明了，但是在程序中还没有赋值。
以下面的代码片段为例，我们试图注销变量 age，在第一种情况下，该变量在我们的程序中已经声明但没有赋值。如果我们检查年龄的类型并试图记录它，我们会得到未定义的。对于 undefined，我们必须声明变量，并给它赋值。

```
var ageconsole.log(age);undefined
```

## **最终想法**

null 和 undefined 一开始会让人感到困惑。Null 仅仅意味着我们试图访问的东西根本不存在，而 undefined 意味着给定的变量要么已经声明，要么根本没有赋值。
感谢您阅读本文，希望对您有所帮助。

## **更多内容:**

[](/3-data-structures-you-need-to-know-7bb5eec3cbf7) [## 你需要知道的 3 种数据结构

### 数据结构是编程的一些基本要素

javascript.plainenglish.io](/3-data-structures-you-need-to-know-7bb5eec3cbf7) [](/getting-started-with-adonisjs-backend-javascript-framework-ffca60d80391) [## AdonisJS 后端 JavaScript 框架入门

### 用 AdonisJS JavaScript 框架构建后端应用。

javascript.plainenglish.io](/getting-started-with-adonisjs-backend-javascript-framework-ffca60d80391) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)