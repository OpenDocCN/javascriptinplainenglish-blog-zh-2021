# 打字稿简介

> 原文：<https://javascript.plainenglish.io/introduction-to-typescript-basic-overview-on-interface-types-and-enums-fab183de5c1e?source=collection_archive---------17----------------------->

## 关于类型脚本接口、类型和枚举的基本概述

![](img/7fb0d2e3f6817e53bc775a3917cbd0ec.png)

Photo by [Luca Bravo](https://unsplash.com/@lucabravo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

要理解 TypeScript，我们首先需要理解 JavaScript 引入了什么样的问题。

在 TypeScript 出现之前，JavaScript 没有类型检查的概念。它是一种动态类型语言。在一端，你可以声明一个变量并让它存储一个字符串。在另一端，你可以让它存储一个数字。让我们看看下面的例子:

如果您正在编写一个简单的应用程序，这是没问题的，但是这也有它自己的含义。让我们来看看下面的场景:

哦不！通常情况下，我们不会重新声明 obj 并将其设置为数值。但是，像这样的事情，在我们发展的时候是可以发生的。

输入 TypeScript。

使用 TypeScript，我们可以指定这些对象可以生成的字段的类型:

假设我们有字段，但我们不确定用户是否会有一个数字，那么我们可以执行以下操作:

在我们深入什么是接口之前，让我们先讨论一下内置于类型中的 TypeScript 以及它们是什么。

正如我们所看到的，TypeScript 在语句声明上实现了强类型。以下是 TypeScript 提供的不同内置类型:

*   数字
*   布尔型
*   线
*   列举型别
*   空的
*   空
*   不明确的
*   任何的
*   从不
*   排列
*   元组

这些类型中有很多是不言自明的，但是有一些返回类型值得研究:never 和 void。

两者有什么区别？让我们更仔细地看一看:

对于 void，我们总是期望返回一个值，也就是 void。实际上，它不会产生我们在代码中使用的任何值，但从技术上讲，它仍然会返回值。

从技术角度来看，没有任何价值会返回或被观察到。

有吗？对于 any，它只是意味着您可以声明一个类型的变量，并将其重新赋值给任何其他类型:

很奇怪，对吧？如果您允许用户将任何类型赋给一个变量，这几乎违背了 typescript 本身的目的。好吧，当我们不知道我们期望从提前得到的数据中得到什么类型时，任何都是有用的。

也就是说，典型的行业标准表明 any 不是一个好的关键字。请记住，typescript 的目的是捕捉错误，并确保变量被赋予它们应该接受的类型。

![](img/334522780c9c4de6d4131f15a488ed72.png)

Photo by [Volodymyr Hryshchenko](https://unsplash.com/@lunarts?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我知道我已经讲了很多关于类型的东西，让我们回到接口的问题上来。

接口是实体应该遵守的语法契约。换句话说，如果我们可以创建一个具有名称和 id 字段的用户，那么作为用户的对象的所有实例都必须具有这两个字段。

接口定义属性、方法和事件，它们是接口的成员。接口只包含成员的声明，由声明者来指定这些属性和事件的行为。

enum 怎么样？

Enum 允许开发人员定义一组命名的常量。使用枚举使得对代码有特殊意义的常量列表的分类变得更加容易。

我们来看看下面这个案例:

如果我们想在代码中使用它们，它看起来会像这样:

现在简单说一下类型。

类型同样支持作为 interface 关键字的别名，但也可用于指定基元、联合或元组的类型:

对于联合，这意味着如果我们实例化一个对象，那么它必须是第一类型或第二类型。使用 tuple，我们可以指定数组中类型的顺序。

TypeScript 简介到此为止。还有更多的内容，但我会在以后的文章中介绍。

*更多内容看*[***plain English . io***](http://plainenglish.io)