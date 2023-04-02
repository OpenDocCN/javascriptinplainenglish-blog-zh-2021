# 揭开 JavaScript 中“var”、“let”和“const”的神秘面纱

> 原文：<https://javascript.plainenglish.io/demystifying-var-let-and-const-in-javascript-9a241615d3a1?source=collection_archive---------15----------------------->

![](img/0e5052474a21713df1d06db762293d59.png)

JavaScript 是一种动态类型语言。动态类型语言是这样的语言，其中变量的类型完全取决于存储在变量中的值的类型。例如，如果值的类型是字符串，那么变量的类型也应该是字符串。

目前有三种方法可以在 JavaScript 中声明变量。它们是——var，let 和 const。这三者在用途、范围或提升方面都互不相同。让我们借助一个例子来理解其中的每一个。

# 案例一— var

## 使用

```
 “use strict”
var variableWithVar = 5;
var variableWithVar;
console.log(variableWithVar); // Prints 5 
```

**var** 是一个特殊的关键字，用于声明如上所示的变量。即使在严格模式下，重复的变量声明也不会导致任何错误(**使用严格的**)，并且值不会丢失，除非给该变量赋一个新值。

## 范围

就作用域而言， **var** 声明如果在函数内部声明，则是函数作用域，否则，它将被视为全局变量，存储在全局对象内部。这些还被添加到全局环境记录的内部名称列表 **[[VarNames]]** 中。函数作用域的变量是那些只能在声明它们的函数内部访问的变量。

```
 // Example One
function varScope() {
 var variableWithVar = 1;
 console.log(“Inside Function”, variableWithVar);
}
varScope() // Prints ‘Inside Function’ 1
console.log(“Outside Function”, variableWithVar) // ReferenceError: variableWithVar is not defined  // Example Two
var variableGlobal = 5;
function varScopeTwo() {
 console.log(“Inside Function”, variableGlobal);
}
varScopeTwo() // Prints ‘Inside Function 5’ 
```

在上面的代码片段中，示例一是一个明确的例子，说明了 **var** 是函数作用域，而示例二是一个明确的例子，说明了 **var** 是全局变量。

**吊装**

在提升方面，所有使用 **var** 关键字声明的变量都会被提升。提升的概念是所有的声明语句都将被移动到顶部，甚至在任何代码被执行之前。重要的是要记住，只有变量声明会被提升，而不是它们的值。提升后的所有变量声明将被赋值 **undefined，**因此，建议在使用之前声明变量。

```
 console.log(variableWithVar); // Prints ‘undefined’
var variableWithVar = 5; 
```

在上面的代码片段中，首先，Javascript 解析代码，在此期间，所有的声明语句都将被挂起。在这种情况下， **var variableWithVar** 将被移到顶部，并被赋予值 **undefined** 。因为不再有声明语句，所以它转到代码执行阶段，执行 **console.log()** 语句。在执行时，它在全局内存中搜索变量 **variableWithVar** 。一旦找到它，它就将该值作为参数传递给 **console.log()** 方法。由于 **variableWithVar** 的值未定义，它打印**未定义的**

# 案例二——让

## 使用

```
 let variableWithLet = 5;
console.log(variableWithLet); 
let variableWithLet;// Output
/*
SyntaxError: Identifier ‘variableWithLet’ has already been declared. (3:4)
*/ 
```

**let** 是一个特殊的关键字，用于声明如上所示的变量。重复的变量声明会抛出错误，如上面的代码片段所示。使用 **let** 声明的变量可以重新赋值，类似于 **var** 。

## 范围

就范围而言，**让**声明是块范围的。借助 **{}** 表示块。块范围的变量是那些只能在声明它们的块内部访问的变量。简单地说，任何块( **{}** )都变成了一个块范围，如果块内的任何变量都是用 **let** 声明的。与 **var** 不同， **let** 不会在全局对象中创建属性。

```
 // Example One
function exampleOne() {
 let one = 1;
 console.log(one);
}
exampleOne() // Prints 1
console.log(one) // ReferenceError: one is not defined 
```

在上面的代码片段中，**示例一个**是一个函数，其中函数体出现在 **{}** 中。在这个函数中使用 **let** 声明任何变量都会使它成为块范围的。 **console.log(one)** 当我们试图在 **exampleOne** 块外访问变量 **one** 时抛出错误。

```
 // Example Two
{
 let one = 1;
 console.log(one) // Prints 1
}
console.log(one) // Prints ReferenceError: one is not defined 
```

上面代码片段是一个清晰的例子，它显示了 **let** 将任何块( **{}** )转换为作用域块，其中使用 **let** 声明的任何变量只能在该块内部访问，而不能在其他任何地方访问。

```
 // Example Three
function letScope() {
 let outsideOne = 1;
 if(true) {
 let insideOne = 2;
 console.log(insideOne) // Prints 2
 console.log(outsideOne) // Prints 1
 }
 console.log(insideOne) // Prints ReferenceError: insideOne is not defined
}
letScope() 
```

在上面的代码片段中，在执行 **letScope()** 函数时，函数中的 **if(){}** 语句变成了块范围，因为块中的变量是使用 **let 声明的。****console . log(inside one)**打印 **2** ，因为 **insideOne** 在同一个范围内。**console . log(outside one)**按照词法作用域的规则打印 **1** ，其中子函数可以访问其父函数的变量。在执行出现在 **if** 块外的 **console.log(insideOne)** 语句时，当我们试图访问 **if** 块外的 **insideOne** 变量时，Javascript 抛出一个引用错误。

```
 // Example Four
var one = 1;
let two = 2;
console.log(this.one) // Prints 1;
console.log(this.two) // Prints undefined; 
```

上面的代码片段是一个清晰的例子，它表明 **let** 没有在全局对象中创建属性。

## 提升

在提升方面，所有使用 **let** 关键字声明的变量都会被提升。在提升过程中，所有的**让**声明移动到代码的顶部。与**变量**不同，**让**变量不能被使用(读/写)，直到它们被完全初始化。只有当它们被初始化为一个值时，它们才被完全初始化。在初始化之前访问**让**变量抛出一个参考错误。

```
 console.log(one); // ReferenceError: one is not defined
let one = 1; 
```

**假设**变量在**时间死区(TDZ)** 内，直到它们被完全初始化。**时间死区**是变量被声明但不可访问的时间段，因为它们没有设置值。当**让**变量被提升时就会发生这种情况。另一方面， **var** 变量在提升期间默认设置为未定义的**值。**

```
 { 
 // TDZ of one starts
 console.log(two); // Prints undefined
 console.log(one); // Prints ReferenceError: Cannot access ‘one’ before initialisation
 var two = 1;
 let one = 2; // TDZ of one ends
} 
```

在上面的代码片段中，Javascript 引擎解析代码，将所有变量声明移到最上面— **var two = undefined** 和 **let one** 。这标志着 TDZ 的开始，因为变量 **one** 没有完全初始化为一个值。现在，随着 javascript 进入执行阶段，它为 **console.log(two)** 语句打印出**未定义的**，并为 **console.log(one)** 抛出一个错误，因为**让**变量在完全初始化之前不能被访问。

# 案例三——常数

**用法**

```
 const variableWithConst = 5;
console.log(variableWithConst); // Prints 5
variableWithConst = 6;
console.log(variableWithConst); // Prints TypeError: Assignment to constant variable. 
```

**const** 是一个特殊的关键字，用于声明如上所示的变量。重复的变量声明和重新赋值给一个**常量**变量会分别抛出一个引用和类型错误，如上所示。

## 范围

就作用域而言， **const** 声明也是块作用域，与 **let** 相同。

```
 // Example One
function exampleOne() {
 const one = 1;
 console.log(one);
}
exampleOne() // Prints 1
console.log(one) // ReferenceError: one is not defined 
```

在上面的代码片段中， **exampleOne** 是一个函数，其中函数体出现在 **{}** 中。在这个函数中使用 **const** 声明任何变量都会使它成为块范围的。 **console.log(one)** 抛出错误，因为我们试图在 **exampleOne** 的块外访问变量 **one** 。

## 提升

在提升方面，所有使用 **const** 关键字声明的变量都会被提升，与 **let** 相同。

```
 console.log(one); // ReferenceError: one is not defined
const one = 1; 
```

**常量**变量也被称为在**时间死区(TDZ)** 内，直到它们被完全初始化，这与 **let** 的完全相同。当**常量**变量被提升时会发生这种情况。

我希望这清楚了 var、let 和 const 声明在用法、范围和提升方面是如何工作的。如果你觉得这篇文章有用，请展示你的爱，并通过你的社交媒体与你的同伴分享，他们可以最大限度地利用这篇文章。请随时通过 [Twitter](https://twitter.com/ajojm) 、 [LinkedIn](https://www.linkedin.com/in/ajojohn/) 或电子邮件与我联系。

直到我们再次见面，**Mallu Dev**结束👋干杯！🥂

*更多内容请看*[***plain English . io***](http://plainenglish.io/)