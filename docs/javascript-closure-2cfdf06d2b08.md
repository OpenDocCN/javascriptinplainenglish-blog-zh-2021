# JavaScript:闭包

> 原文：<https://javascript.plainenglish.io/javascript-closure-2cfdf06d2b08?source=collection_archive---------0----------------------->

![](img/526f90199580740b33ce1cbc53a9c172.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中最有趣但令人难以置信的概念之一是闭包。不管喜欢与否，许多人偶然发现这个概念，并发现它很难，尤其是在面试中。大多数时候，关于闭包的理论很容易理解。然而，当你得到一个现成的问题陈述时，你很可能会出错。为什么？你可能还没有理解闭包的真正含义和意义。

在这篇文章中，我想分享一下我对什么是闭包以及为什么使用闭包的理解。

## 长话短说

首先，我坚信闭包只不过是一个函数。

当一个函数与它在外部作用域(别名词法环境)中的引用成对出现时，它就变成了一个闭包。

什么是词汇环境？它只是一个执行上下文，看起来像一个堆栈框架。在词法环境中，所有局部变量名和值都被映射。

JavaScript 一直在利用词汇环境。每个函数在词法环境中都有一个引用。当一个函数被调用时，该函数的引用被用来构建实际的执行上下文。因此，函数内部的所有代码行将能够看到外部变量的实际值。无论何时何地调用该函数，都可以看到实际值。

当一个函数调用另一个函数，而另一个函数又调用另一个函数时，就产生了一个链。对于那些不知道的人来说，这只不过是一个范围链。

```
function **foo**() {
  const **secret** = "777";
  return function inner() {
    console.log(`The secret number is ${secret}.`)
  }
}
const f = **foo**()
f()
```

让我们考虑一下上面的代码片段。你可能想知道存储在 **foo** 中的**秘密**号是什么。嗯，知道**秘密**数字的唯一方法，就是调用 **f** 。创建 foo 时，函数 inner 在构建执行上下文时用 foo 的词法环境创建一个闭包。这意味着，调用 **f** 将让你访问**秘密**号。

## 为什么需要闭包？

让我们假设 JavaScript 中从来没有闭包。现在，在上面的例子中，你如何访问**秘密**？如果没有闭包，您将在函数之间显式地传递参数**。这将使你的代码变得非常长，并且非常嘈杂。代码能够投入生产吗？这是一个你需要回答的问题。**

让变量和函数成为函数的私有部分是很棒的。使用闭包，您可以很容易地实现这一点。当你决定你需要一个私有国家的时候，你将需要闭包。

直到今天，JavaScript 还不支持私有字段。

直到 2015 年，JavaScript 都没有任何一种创建类的语法。

为什么？您可以使用闭包来实现以上目标。

```
**//Example of creating a Private Instance**function Festival(name, month, date, color) {
  return {
    toString() {
      return `${name} ${month} (${date}, ${color})`
    }
  }
}
const feast = new Festival('Christmas Eve','December','24','Gold, Red and Silver')
console.log(feast.toString())**//Example of building event oriented code**const $ = document.querySelector.bind(document)
const COLOR = 'rgba(20,20,20,1)'

function onClick() {
  $('body').style.background = COLOR
}

$('button').addEventListener('click', onClick)**//Example of building class based structures**function createObject() {
  let x = 42;
  return {
    log() { console.log(x) },
    increment() { x++ },
    update(value) { x = value }
  }
}

const o = createObject()
o.increment()
o.log() // 43
o.update(5)
o.log() // 5
const p = createObject()
p.log() // 42
```

## 使用正确的声明

有几种方法可以声明变量。可以选择**让**、 **var** 或者 **const** 。这些声明的行为在闭包中有很大的不同。

例如，如果你选择 **var** 来声明一个变量，你必须小心你计划关闭的变量。

使用 **var** 声明的变量将被提升。我们用一个简单的例子来理解这一点。

```
function **foo**() {
  var result = []
  for (var i = 0; i < 3; i++) {
    result.push(function inner() { console.log(i) } )
  }
  return result
}

const result = **foo**()
for (var i = 0; i < 3; i++) {
  result[i]() 
}
```

那么，上面这段代码会打印出什么呢？上面的代码将打印三次“3”。另一方面，预期结果将是“1、2 和 3”。

并且，上述由 **var** 引起的问题可以用 **let** 解决。

## 常见的误解

很多时候，开发人员读到了闭包，并且认为闭包只有在内部函数被返回时才被创建。构建闭包不需要返回函数或变量。将一个内部函数赋给一个变量，或者将一个参数传递给一个可以调用它的函数就足够了。闭包是在封闭函数被调用时创建的。

闭包不引用作用域中的旧值。变量成为闭包不可分割的一部分。当您访问一个变量时，您将能够看到最近的值。这使得用循环构建内部函数的过程非常困难和棘手。

闭包可能会消耗大量内存。然而，您永远不会面临任何类型的内存泄漏。为什么？JavaScript 倾向于清理所有没有被引用的循环结构。

## 摘要

闭包代表一个代码块，它满足三个标准:

1.  你可以把它作为一个值来传递
2.  它可以按需执行。任何拥有该值的人都可以执行它。
3.  可以引用用于创建闭包的上下文中的变量。

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***