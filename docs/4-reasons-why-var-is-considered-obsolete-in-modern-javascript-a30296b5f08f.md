# “var”在现代 JavaScript 中被认为过时的 4 个原因

> 原文：<https://javascript.plainenglish.io/4-reasons-why-var-is-considered-obsolete-in-modern-javascript-a30296b5f08f?source=collection_archive---------3----------------------->

## 使用“var”的陷阱以及“var”和“let”的区别。

![](img/d1587ac1afdc0d9353028b2738a4db93.png)

Photo by [Pakata Goh](https://unsplash.com/@pakata?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是一种强大的语言，因为你可以编写一个完整的软件，根本不用采用任何其他编程语言。

`var`曾经是 JavaScript 中声明变量的一种方式。然而，以这种方式声明一个变量或对象现在已经很少见了，因为它会在你的 JavaScript 项目中制造噩梦。

```
var obj = {} 
// instead let (or const) is used to declare a variable 
```

从 ECMAScript 6 开始，引入了`let`语句。

下面简单介绍一下为什么在 JavaScript 项目中不再或很少使用`var`来声明变量。

> **注意:**如果你已经熟悉使用 var 的陷阱，这篇文章仍然可以作为一个很好的复习。

## 1.范围界定——避免 var 的主要原因

作用域是 var 和 let 的关键区别。

`var`变量的作用域是直接函数体(因此是函数作用域),而`let`变量的作用域是直接*包围由`{ }`表示的*块。

让我们通过代码来理解这意味着什么。

```
function run() {var foo = "Foo";
let bar = "Bar";
console.log(foo, bar); // Foo Bar{
 var moo = "Mooo"
 let baz = "Bazz";
 console.log(moo, baz); // Mooo Bazz
}
console.log(moo); // Mooo
console.log(baz); // ReferenceError}run();
```

将关键字`let`引入语言的原因是函数作用域令人困惑，这也是 JavaScript 中错误的主要来源之一。

## 2.吊装——不用担心`let`

首先，我们需要回顾一下什么是吊装。

> 变量甚至在声明之前就可以在它们的封闭范围内被访问。

```
function run() {

  console.log(foo); // undefined 
  // Hoisting in action !

  var foo = "Foo";
  console.log(foo); // Foo
}

run();
```

但是不用担心！`Let`不会让这种情况发生。

```
function checkHoisting() {
  console.log(foo); // ReferenceError
  let foo = "Foo";
  console.log(foo); // Foo
}

checkHoisting();
```

## 3.全局对象绑定

> 在顶层，`let`与`var`不同，不在全局对象上创建属性。

```
var foo = "Foo";  // globally scoped
let bar = "Bar"; // not allowed to be globally scoped

console.log(window.foo); // Foo
console.log(window.bar); // undefined
```

## 4.重新申报。不擅长 Let

> 在严格模式下，`var`将允许您在相同的范围内重新声明相同的变量，而`let`会引发一个 SyntaxError。

```
'use strict';
var foo = "foo1";
var foo = "foo2"; // No problem, 'foo1' is replaced with 'foo2'.

let bar = "bar1"; 
let bar = "bar2"; // SyntaxError: Identifier 'bar' has already been declared
```

查看实际的[**stack overflow**](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var/11444416#11444416)线程以获得更多信息，或者如果您认为我遗漏了什么，请写在评论中。我会补充这一点，并相应地更新文章。

快乐阅读！

*更多内容尽在* [***说白了***](http://plainenglish.io/)