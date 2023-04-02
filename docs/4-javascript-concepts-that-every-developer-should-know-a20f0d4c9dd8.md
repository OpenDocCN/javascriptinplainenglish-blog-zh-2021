# 每个开发人员都应该知道的 4 个 JavaScript 概念

> 原文：<https://javascript.plainenglish.io/4-javascript-concepts-that-every-developer-should-know-a20f0d4c9dd8?source=collection_archive---------0----------------------->

![](img/f8a6c6f98eae357ccbdb93e942920daf.png)

JavaScript 代表了互联网的三大(最常见的)支柱之一，HTML 和 CSS 分别提供了结构和风格，JavaScript 赋予了网页生命。此时此刻，JavaScript 似乎不会很快走向任何地方。超过 95%的网站使用这种语言。全部登上 JS 列车。

在这篇文章中，我将讨论作为一名 web 开发人员需要掌握的四个最重要的 JavaScript 概念。

## 1.生活

IIFE，又名 Immediately Invoked Function Expression，是 JavaScript 函数，定义为表达式，一旦定义，就立即调用和执行。在生命中声明的变量不能从外部访问，从而避免了全局范围的污染。因此，引入 IIFE 的主要原因是即时代码执行和由此产生的数据隐私。

定义生命的语法可以在下面的例子中看到:

```
(function(a,b){         
     return a + b; 
})(10,20);
```

您也可以使用箭头函数来定义生活:

```
(() => {     
    *//...* 
})();
```

## 2.范围

范围如果引用变量访问，您在不同的上下文中可以(或不可以)访问哪些变量。在 JavaScript 中，默认范围是窗口范围(也称为根范围)。作用域可以被想象成一个变量、对象和函数的边界框，它包括对变量的限制，并决定你是否能够访问变量。这限制了代码其他部分对变量的可见性和可访问性。对于开发人员来说，深刻理解这一概念至关重要。范围可以是**本地**或**全局** —本地范围允许访问边界内的所有内容，而全局范围是边界外的所有内容。全局作用域无法访问局部作用域中定义的变量，因为它被包含在边界内，除非它被返回。

例如，假设你有一个函数，你定义了一个变量—

```
function sayHello() {
    let greeting = "Hello";
}sayHello()
console.log(greeting); //a ReferenceError is returned stating that 'greeting' is not defined
```

这个 **ReferenceError** 返回为“**问候语**”是在 **sayHello** 函数的局部范围内定义的，因此不可能在函数之外访问该变量。

## 3.关闭

在之前的一篇文章中，我对闭包进行了更深入的探讨，如果你对闭包有兴趣，我会链接下面的文章，但我也会在这里猜测。

[](https://denalibalser.medium.com/ruby-blocks-procs-and-lambdas-920148136dae) [## Ruby 块、Procs 和 Lambdas

### 要理解 Ruby 语言中的块、过程和 lambdas，首先必须理解闭包的概念。

denalibalser.medium.com](https://denalibalser.medium.com/ruby-blocks-procs-and-lambdas-920148136dae) 

闭包是另一个函数中的一个函数，它能够访问外部函数中定义的变量。这个内部函数在技术上是闭包，同样能够访问定义在父(或外部)函数中的变量，以及定义在它自己的作用域和全局变量中的变量。但是，父函数不能访问内部函数的变量。

当您想要将变量、数组或方法从外部函数传递到内部函数以扩展行为时，使用闭包会很有帮助。

## 4.提升

如果没有提升的知识，许多开发人员会从他们的 JavaScript 代码中体验到意想不到的结果。在 JavaScript 中，您可以在定义函数之前调用它，而不会收到 **ReferenceError** 。这是因为 JavaScript 解释器在执行之前将变量和函数声明移到了当前作用域(无论是局部的还是全局的)的顶部——这称为提升。

比如说—

```
onePlusOne();function onePlusOne(){
    console.log(1 + 1); 
}
//2 is returned in console
```

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)