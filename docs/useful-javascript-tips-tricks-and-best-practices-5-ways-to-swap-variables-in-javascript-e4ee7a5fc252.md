# JavaScript 中交换变量的 5 种方法

> 原文：<https://javascript.plainenglish.io/useful-javascript-tips-tricks-and-best-practices-5-ways-to-swap-variables-in-javascript-e4ee7a5fc252?source=collection_archive---------9----------------------->

## 思维程序员

## 改进 web 开发

![](img/b276512b81470f404506780eeaac1151.png)

Photo by [Kumpan Electric](https://unsplash.com/@kumpan_electric?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

"*写一个函数互换两个变量？*

"*如何在没有临时变量的情况下互换两个变量？*

这些都是编码面试中常见的问题。实际上，很多算法也需要交换两个变量。

# 让我们现在开始吧

假设我们有两个变量，`a`和`b`，我们有一个任务是写一个程序在 Java 脚本中交换它们。

最初，`a`是`3`，`b`是`5`。

```
var a, b;a = 3
b = 5console.log(`before: a = ${a} and b = ${b}`)
```

# JavaScript 中交换变量的 5 种方法

## 临时变量

我们使用`temp`变量来临时保存 a 的值。然后我们将`b`的值放在 a 中，稍后将`temp`放在`b`中。通过这种方式，值被交换。

```
temp = a
a = b
b = temp

console.log(`after: a = ${a} and b = ${b}`)
```

让我们看看如何执行交换。

*   `temp`被赋予`a`的值。
*   `a`变量被赋予了`b`的值。
*   变量`b`被赋予`temp`和**的值。**

## 加法和差分

这个想法是得到两个给定数字之一的和。然后，可以使用总和以及总和的减法来交换这些数字。

```
a = a + b;
b = a - b;
a = a - b;

console.log(`after: a = ${a} and b = ${b}`)
```

让我们看看如何执行交换。

*   `a = a + b`将值`8`分配给 a。
*   `b = a — b`将值`3`分配给 b。
*   `a = a — b`将值`5`分配给**。**
*   `a = a ^ b`将值`6 ^ 4`分配给 a(现在为 **2)。**

## 乘法和除法

类似地，乘法和除法可以用来执行交换。

```
a = a * b
b = a / b
a = a / b

console.log(`after: a = ${a} and b = ${b}`)
```

让我们看看如何执行交换。

*   `a = a * b`将值`15`分配给 a。
*   `b = a / b`将值`3`分配给 b。
*   `a = a / b`将值`5`分配给一个**。**

## 按位异或运算符

如果两个操作数不同，按位 XOR 运算符的计算结果为`true`。

```
a = a ^ b
b = a ^ b
a = a ^ b

console.log(`after: a = ${a} and b = ${b}`)
```

让我们看看如何执行交换。

*   `a = a ^ b`将值`6`分配给 a。
*   `b = a ^ b`将值`3`分配给 b。
*   `a = a ^ b`将值`5`分配给一个**。**

## 解构分配

```
[a, b] = [b, a]

console.log(`after: a = ${a} and b = ${b}`)
```

析构赋值(ES2015 的一项功能)允许您将数组中的项提取到变量中。

# 结论

最后，`a`是`5`，`b`是`3`。

今天，你已经学会了如何使用临时变量交换两个变量。

```
*You can get the source code of the article here:* [https://github.com/housecricket/Awesome-tips-for-improving-web-development-in-JavaScript](https://github.com/housecricket/Awesome-tips-for-improving-web-development-in-JavaScript) 
```

但请记住以下几点。

*   如果 a 和 b 太大，算术解可能会超出整数范围。
*   如果其中一个数字为 0，基于乘法和除法的方法就不起作用，因为不管另一个数字是多少，乘积都会变成 0。
*   当我们使用指向变量的指针并进行函数交换时，当两个指针都指向同一个变量时，上述所有方法都会失败。

很简单，对吧？

*更多内容请看*[*plain English . io*](http://plainenglish.io/)