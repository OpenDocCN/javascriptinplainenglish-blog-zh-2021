# 5 个有用且棘手的 JavaScript 问题

> 原文：<https://javascript.plainenglish.io/5-useful-and-tricky-javascript-questions-4b50b5106a2b?source=collection_archive---------7----------------------->

## 在 JavaScript 中需要知道的一些棘手问题。

![](img/88098586054521f7f0fa73b5ca1dafa6.png)

Photo by [JASUR JIYANBAEV](https://unsplash.com/@djianbaev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

JavaScript 是最好的编程语言之一，尤其是在 web 开发中。为了成为更好的 JavaScript 开发人员，您需要深入研究该语言的基础。这需要大量的练习，而不仅仅是学习。然而，当试图用 JavaScript 解决问题时，有时会有点棘手。这就是为什么我决定与你分享一些棘手的问题，这些问题将帮助你理解 JavaScript 的概念，比如提升、闭包等等。

在本文中，我们将为您列出一些 JavaScript 中有用的棘手问题，包括它们的答案。让我们开始吧。

# 问题 1

控制台中的变量`a`和`b`的输出是什么？

```
console.log(a)
console.log(b)
var a = 2
let b = 2
```

*如果您在控制台上运行问题，请记住一些变量正在重复出现。所以，从一个问题到另一个问题刷新您的页面。*

**答案:**

当代码执行时，编译器查找变量声明，如果变量已声明，它会将其提升到顶部，如下所示:

```
var a;
console.log(a)
console.log(b)
a = 2
let b = 2;
```

请注意，用`let`或`const`声明的变量没有被提升。这就是为什么变量`b`在这种情况下没有被提升。

所以当我们运行上面的代码时，我们会得到`undefined`代表`a`，而`b is not defined`代表变量`b`。如果你得到正确的答案，那意味着你理解起重。

# 问题 2

调用`a`和`b`会有什么输出？

```
a()
function a(){
    console.log("a")
}
b();
var b =function(){
    console.log("b")
}
```

**答案:**

在这种情况下，通过调用`a()`我们将得到字符串`a`打印在控制台中，因为函数也在类似变量的 JavaScript 中被提升。

通过调用`b()`，您将在控制台中得到`b is not a function`的类型错误。因为`b`是存储函数的变量。当它将被吊起时，存储的功能将不会被吊起。吊装后，代码如下:

```
**function a(){
    console.log("a")
}
var b**a()
b();
b =function(){
    console.log("b")
}
```

这就是为什么在 JavaScript 中理解提升的概念非常重要。我写了一篇关于这个概念的短文，如果你想看看的话。

[](https://medium.com/dev-genius/4-things-you-should-know-about-javascript-hoisting-8b53803a1ed0) [## 关于 JavaScript 提升你应该知道的 4 件事

### 用实例理解 JavaScript 的提升

medium.com](https://medium.com/dev-genius/4-things-you-should-know-about-javascript-hoisting-8b53803a1ed0) 

# 问题 3

调用下面的函数的输出是什么？

```
function myFunction(){
    return a = 2
  }
  myFunction()
```

**答案:**

在这种情况下，你可以说`a`没有定义。但答案是`2`。

这就是为什么 JavaScript 是一种独特的语言。当我们在 Java script**(`**a=2**`)**，**中做没有声明的赋值时，编译器会把变量保存在全局范围内。所以输出才是`2`。如果你愿意，你可以通过使用严格模式`"use strict”`来避免这种行为。**

# **问题 4**

**打印`answer`到控制台的输出是什么？**

```
var answer = 0;

const baseValue = value => multipleValue => value * multipleValue;

const multiple = baseValue(2);
answer = multiple(5);
console.log(**answer**);
```

****答案:****

**嗯，这是一个非常棘手的问题。这是关于闭包的，这是 JavaScript 中一个非常重要的概念。这种情况的答案是`10`。**

**闭包允许内部函数访问外部函数。我们可以看看像全局作用域(外部函数)和局部作用域(内部函数)这样留在全局作用域内部的闭包(`baseValue`)。像 JavaScript 中的常规作用域一样，局部作用域可以访问全局作用域。因此，编译器可以知道什么是`value`。**

**通过将变量`multiple`设置为`baseValue(2)`，内部函数将存储在`multiple`中，外部函数的参数将具有值`2`。此外，在调用`multiple(5)`之后，内部函数的参数将有一个值`5`。这就是为什么在内部函数中返回乘法后会得到`10`的原因。**

# **问题 5**

**下面这种情况的结果是什么？**

```
var a = 1
function foo(){
 var a = 2
 console.log(a)
}
foo()
console.log(a);
```

****答案:****

**这个问题是关于 JavaScript 中的作用域，如果你知道这个概念，你很可能会得到正确的答案。**

**如果你说的是`2`和`1`，那你就对了。有两种类型的作用域:全局作用域和局部作用域。JavaScript 函数中声明的变量成为局部变量，函数外声明的变量成为全局变量。**

**`var a = 1`从函数中声明并保存在全局内存中。`var a = 2`在函数内部声明并保存在本地存储器中。这是记忆中不同的地方。**

# **结论**

**如您所见，知道这些棘手问题的答案需要实践和对重要 JavaScript 概念的深刻理解。**

**感谢您阅读本文，希望您觉得有用。如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！****

# **更多阅读**

**[](https://medium.com/javascript-in-plain-english/the-front-end-web-developer-roadmap-for-2021-bcf88c5d4ccd) [## 2021 年前端 Web 开发者路线图

### 成为现代前端 web 开发人员的一步一步指南。

medium.com](https://medium.com/javascript-in-plain-english/the-front-end-web-developer-roadmap-for-2021-bcf88c5d4ccd)**