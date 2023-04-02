# JavaScript 提升影响代码的 3 种方式

> 原文：<https://javascript.plainenglish.io/3-ways-javascript-hoisting-affects-your-code-a6a93626c600?source=collection_archive---------4----------------------->

## 你可以在声明变量之前使用它们？

![](img/1b9087013edf979f9a0a0b4cb58d5713.png)

[Photo by Joshua Aragon](https://www.instagram.com/the.brogrammer/?hl=en)

在运行程序后的最初几分钟，JavaScript 做了一些非常有趣的事情。它使这个…

```
numApples = 3;
console.log(numApples);var numApples;
```

…一段完全有效的代码，相当于…

```
var numApples;
numApples = 3;
console.log(numApples);
```

这两段代码将输出完全相同的结果:“3”。在这方面，是的，你绝对可以利用尚未正式声明的变量。我推荐吗？大概不会。如果你养成了这种习惯，你的代码可能会变得越来越复杂，越来越难调试。另外，如果你正在与一个团队合作，使用未声明的变量可能会使他们困惑。

在计算中使用变量之前，最好先声明并初始化变量；尽管如此，理解 JavaScript 的幕后提升操作仍然是必不可少的。理解这个操作可能会为您以后省去几个小时的困惑。

# 什么是吊装？

提升是 JavaScript 将变量和函数声明拉到当前作用域顶部的过程。在执行任何代码之前，都会发生提升，JavaScript 会在堆内存中为这些函数和变量分配空间。

注意:我们只是在谈论声明。

```
//DECLARATIONS
var a;
let a;
const a;
function add(x,y){
...
}
```

JavaScript 不会将初始化的变量提升到当前范围的顶部。下面是初始化的例子。

```
var a = 6;
let b = 4;
const c = 2;
```

现在，提升在 var、let 和 const 变量类型之间也有不同的工作方式。

## 无功提升

在第一个提升的例子中，展示了在声明变量之前，变量可以用于有意义的计算。让我们深入探讨一下。

```
console.log(name);
var name;
```

上面的代码会给你一个错误信息。它会告诉你‘名字’是[未定义的](https://medium.com/@kyledeguzmanx/3-differences-between-null-and-undefined-fb93fedd4fe7)。这意味着“name”是您可以使用的完全有效的变量；但是，变量“name”从未被赋值。没有可供控制台显示的值。

为了澄清，上面的代码完全等同于:

```
var name;
console.log(name);
```

那么，为什么变量的值是“未定义”呢？显然，这是因为程序员从来没有写过给变量赋值的指令或代码。然而，故事远不止于此。

在提升过程中，JavaScript 会将该变量带到当前作用域的顶部，并在堆内存中分配空间。当 JavaScript 存储变量时——特别是关键字 var——JavaScript 也会用未定义的值初始化这些变量。

这与“let”和“const”类型的变量完全不同。

## 让吊装

让我们采用上一节中的相同代码，但是将关键字替换为“Let”。

```
console.log(name);
let name;
```

提升还会将变量“name”带到当前作用域的顶部，并在堆内存中为它分配空间。区别在于提升不会用值' undefined '初始化变量。它只会让变量真正为空。

当这段代码运行时，您将得到一个引用错误，而不是被告知变量未定义。这个引用错误会告诉你你试图使用一个没有初始化的变量。

对于 const 类型的提升变量，情况也是如此。

## 未声明的变量提升

最后，讨论未声明的变量。这些变量在初始化时没有“let”、“const”或“var”。这些也是在没有正式声明的情况下使用的变量。

```
numDogs = 4;
console.log("Tyler has " + numDogs + " dogs");
```

在上面的代码中，numDogs 是在没有关键字的情况下初始化的。这是一段完全有效的代码。

```
const numSiblings = numBrothers + numSisters;
numBrothers = 1;
numSisters = 1;
```

在上面的代码中，numBrothers 和 NumSisters 都是在没有关键字的情况下初始化的变量。尽管这些变量是在没有关键字的情况下声明的，但它们仍然是可以在计算中使用的有效变量。

这些未声明的变量也会被提升，但是这些变量是特殊的。JavaScript 将把每个未声明的变量——也就是没有变量类型的变量:let、var 和 const——提升到全局范围的顶部！

> 未声明的变量总是全局变量。

这些变量出现在哪里并不重要。它们将永远是全局变量。

记住！如果我们不是在讨论未声明的变量，初始化永远不会被提升。

```
var numPuppies = 6;
const numStudents  = 400;
let numTeachers = 40;
```

这些 var、const 和 numTeachers 变量都不会被提升，因为提升只发生在变量声明上。没有关键字的未声明变量是唯一的例外。

*更多内容看*[***plain English . io***](http://plainenglish.io/)