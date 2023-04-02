# 您不应该跳过的 JavaScript 核心概念

> 原文：<https://javascript.plainenglish.io/javascript-core-concepts-you-should-not-skip-95e05f89ca8d?source=collection_archive---------4----------------------->

## 了解语言的核心才能成为更好的程序员。

![](img/5a9c6af32c873c56861502356d2577fc.png)

Photo by [Mimi Thian](https://unsplash.com/@mimithian?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

开始学 JavaScript 了吗？JavaScript 是最流行和最强大的语言之一，然而人们经常误解这种语言。但是一旦你掌握了这门语言，你就会感受到它的真正力量。

这里有一些作为 JavaScript 开发人员应该知道的技巧和诀窍。

# **动态类型**

JavaScript 是一种松散类型的动态语言。这意味着，与 C 或 C++不同，JavaScript 中的变量不直接与特定类型相关联。任何值都可以赋给变量。让我们看看下面的例子。

```
**let** x = 34; *// Now x is a number*x = ‘hello world’ *// but you can reassign x to a string or*x = true; *// a boolean*x = 34.6; *// or a float*
```

正如您在示例中看到的，您可以将变量分配或重新分配给任何您想要的类型。

# **原始类型**

在 JavaScript 中，原始数据类型不是对象或者没有任何方法。JavaScript 中有 7 种原始数据类型:**数字、字符串、布尔、BigInt、空、未定义、符号。**

## **编号**

number 类型表示数值，但与 C 或 C++不同，JavaScript 只有一种类型— **数字、**，这可以是 **32** 或 **32.04、**，JavaScript 还将**无穷大**和 **NaN** (不是数字)视为**数字。**让我们看一个例子。

```
console.log(typeof(32)); *// output will be number*console.log(typeof(32.04)); *// output will be number*console.log(typeof(NaN)); *// output will be number*console.log(typeof(Infinity)); *// output will be number*
```

尝试在您的浏览器或编辑器中运行这段代码，您将获得相同的输出。

## **字符串**

字符串是一系列字符。只要记住一件事—字符串必须用引号括起来。可以是单引号，也可以是双引号，实际上，它们之间没有区别。

引号内的任何内容都是字符串。与 C 或 C++不同，JavaScript 中没有**字符**类型。在 JavaScript 中，只有一种类型是**字符串，**和**字符串**可以是空的，也可以有单个字符或多个字符。让我们看一个例子。

```
console.log(typeof(‘hello world’)); *// output will be string*console.log(typeof(‘434323’)); *// output will be string*console.log(typeof(‘’)); *// output will be string*console.log(typeof(‘h’)); *// output will be string*
```

尝试在编辑器中运行这段代码。

## **布尔型**

布尔是一种只存储值**真**或**假**的类型，或者你可以说**‘是’**或**‘否’**。如果我们比较像 **4 > 2、**这样的两个数字，我们就会得到**真值。**或者，在**4<2**的情况下，它会给我们**假。让我们看一些例子来进一步阐明这一点。**

```
console.log(4 > 2); *// will give true*console.log(4 < 2); *// will give false*
```

在第二个例子中，我们将检查不同值的类型。第一行将给出 true，因为 4 是一个数字，第二行也将给出 true，第三行将给出 **false** ，因为 3.14 是一个数字，而不是一个字符串。

```
console.log(typeof(4) == ‘number’);console.log(typeof(‘hello’) == ‘string’);console.log(typeof(3.14) == ‘string’);
```

我们将在另一篇博客中讨论逻辑运算符布尔运算。请记住，boolean 只有一个值，真或假。

## **空**

Null 表示对象或变量没有值。根据 MDN 文档，null 表示有意缺少任何对象值。这意味着您可以将 null 赋给任何变量或对象。Null 是一个赋值，你可以给它赋一个变量或对象。人们经常误解 null 和 undefined，undefined 是否是无意发生的。在 JavaScript 中，null 是一个假值。

## **未定义**

Undefined 意味着声明了一个变量，但没有给该变量赋值。如果我们看看这个例子，我们会理解得更好。

```
**var** a;console.log(a);
```

我们声明了一个变量，但没有给这个变量赋值。如果我们打印变量，那么我们会得到未定义的。

人们经常误解 null 和 undefined，但是如果我们严格检查，那么我们会看到它会给我们一个假值，因为 null 和 undefined 是不一样的。

```
console.log(null === undefined); // this will give us false
```

## **BigInt**

BigInt 是一种特殊的数字类型，表示大于 253–1 的整数。可以通过在整数后面追加 **n** 或者类似下面的方式来写 BigInt。

```
**var** x = 3**n**;console.log(typeof(x)); *//output will be bigInt**// or like***var** bigNumber = BigInt(12232323232);console.log(typeof(bigNumber)); *//output will be bigInt*
```

## **符号**

该符号在 ES6 或 ECMAScript 2015 中引入。你可以简单地通过调用`Symbol()`来创建一个符号。每次我们调用一个`Symbol`，它都会创建一个不同于所有其他符号的独特符号。让我们看一个例子。

```
**var** sym1 = Symbol(‘foo’); *// creates a new symbol***var** sym2 = Symbol(‘foo’); *// creates another new symbol*console.log(sym1 === sym2); *// output will be false*
```

# **变量声明— var、let 和 const**

在 Javascript 中，有三种方法来声明变量。最初，var 用于在 JavaScript 中声明变量；后来，当 ES6 发布时，JavaScript 增加了两种声明变量的方法，分别是 let 和 const。var、let 和 const 之间有一些区别。

## **Var**

在 ES6 之前，只有 var 用于声明变量。Var 可以是全局作用域或函数作用域。范围仅仅意味着变量可以在哪里使用。当 var 在函数外部声明时，它是全局范围的；如果 var 是在一个函数中声明的，那么它的作用域就是函数。当 var 是全局作用域时，我们可以在程序的任何地方使用它。如果我们在函数中声明 var，那么 var 只能在函数中访问。让我们看一个例子。

```
**var** msg = ‘hello world’;**function** greetings() {console.log(msg); *// this line will show ‘hello world’, msg can be accessible inside function***var** foo = ‘hello’;}console.log(foo); *// this line will show an error because foo is only accessible within the function*
```

Var 可以被重新分配和重新声明。这意味着你可以给 var 赋值，也可以重新声明。

```
**var** greet = ‘hello JS people’;console.log(greet); *// will show ‘hello JS people’*greet = ‘hello world’;console.log(greet); *// will show ‘hello world’***var** greet = ‘hello’; *// or you can redeclare it like this*console.log(greet);
```

用 var 声明的变量被提升到其作用域的顶部。提升是一种将变量和函数声明移到执行堆栈顶部的机制。让我们看另一个例子来简单地理解这个机制。

```
console.log(msg); *// will show ‘hello JS people’***var** msg = ‘hello JS people’;*// this will interpreted like this***var** msg;console.log(msg); *// it will show undefined*msg = ‘hello JS people’;
```

## **让**

在 ES6 中引入了 Let。用 let 声明的变量是块范围的。我们可以说 **{}** 里面的任何东西都是块范围的。这意味着一个块被 **{}绑定。**

var 和 let 的区别在于，var 可以重声明，而 let 不能重声明。

```
**let** newMsg = ‘hello’;**let** newMsg = ‘world’;console.log(newMsg); *// if we do this then it will throw an error*
```

和 var 一样，let 声明也悬挂在顶部。但是它们之间有一点点不同。Let 没有初始化，这意味着如果你想使用 let like var，你会得到一个 ***引用错误*** 。在 var 的情况下，我们得到 ***未定义。***

```
console.log(newMsg); *// if we do this then it will throw a ReferenceError***let** newMsg = ‘hello’;
```

## **常量**

Const 也是块范围的，并被提升到执行堆栈的顶部。但是如果你用 const 声明一个变量，那么它将保持不变。常量不能重新声明或重新分配。Const 用于声明常数值。

```
**const** color = ‘white’;console.log(color); *// will show white*color = ‘red’;console.log(color); *// will throw a TypeError*
```

# **== vs ===**

JavaScript 中的==(相等)和===(相同)运算符有所不同。==松散地检查并执行**类型的强制**。类型强制是将一个值从一种类型转换成另一种类型的过程(我将在后面的**中进一步讨论这个过程)。如果我们比较**‘323’**和 **323，**我们就会得到真。**

```
***323 == ‘323’******// true***
```

因为==将执行类型强制，这意味着它将简单地将字符串' **323'** 转换为数字。如果我们使用 `**===**` 做同样的事情，那么我们将得到 false。`**===**`操作符寻找相同的类型和相同的值。`**===**` 运算符严格检查类型和值。

```
***323 === ‘323’******// false******32 === 32******// true***
```

# **函数声明和函数表达式**

函数是程序的主要组成部分。函数是执行特定任务的代码块。在 javascript 中，我们可以用四种不同的方式编写函数。现在我们将讨论编写 JavaScript 函数的两种方法。

## **功能声明**

在函数声明中，首先是单词 function，然后是函数名，最后是用于接收参数的括号。我们可以接收由逗号分隔的参数列表。我们可以像这样声明一个函数。

```
**function** greeting(str) {console.log(str)}
```

## **函数表达式**

在 JavaScript 中，一个函数可以存储在一个变量中，它被称为函数表达式。

我们可以使用如下函数表达式创建函数:

```
**let** greeting = **function**(str) {console.log(str);}greeting(‘hello’);
```

就是这样。这些是您需要熟悉的一些基本 JavaScript 概念。希望这篇文章是有用的，感谢您的阅读。

*更多内容看*[***plain English . io***](http://plainenglish.io/)