# JavaScript 中 6 个最常见的运算符

> 原文：<https://javascript.plainenglish.io/the-6-most-common-operators-in-javascript-599cbd914484?source=collection_archive---------8----------------------->

## 你每天都看到它们，但你知道它们是什么吗？

在 JavaScript 中，运算符是一种比较、赋值或执行运算的方式。有许多不同类型的运算符。

JavaScript 中有*二元*运算符、*一元*运算符和一个*三元*运算符。“二进制”意味着涉及两个值，或*操作数*，一个在运算符之前，一个在运算符之后。二元运算符的一个例子是`1 + 2`。在这个例子中，`1`和`2`是操作数，`+`是运算符。

“一元”操作符意味着只有一个操作数。操作数要么在运算符之前，要么在运算符之后。一元运算符的一个例子是`x++`(如果你不熟悉这个语法，不要担心，我们将在下面讨论)。

JavaScript 中的“三元”运算符涉及三个操作数。它被用作`if...else`语句的简化版本，因此也被称为“条件”操作符。三元运算符的一个例子是`num >= 0 ? "Positive" : "Negative"`。在这个例子中，三个操作数是`num >= 0`、`"Positive"`和`"Negative"`，分隔它们的运算符是`?`和`:`。

![](img/778e12104569a278b230c6b951e491f6.png)

Photo by [Elena Mozhvilo](https://unsplash.com/@miracleday?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 1.赋值运算符

一个**赋值**操作符是一个二元操作符。它根据右操作数的值给左操作数赋值。

最常见的赋值操作符是`=`，如`a = b`所示。在本例中，`a`是左操作数，它被赋予了右操作数`b`的值。

还有*复合赋值运算符*。复合赋值运算符通常将赋值运算符和算术运算符组合成一个简化版本。比如`a += b`就是`a = a + b`的简称。

下表列出了一些最常见的赋值运算符:

让我们来看看上述运算符的一些示例:

```
let x = 10;
console.log((x += 3)); // x = 10 + 3 -> x = 13let y = 8;
console.log((y -= 3)); // y = 8 - 3 -> y = 5let z = 3;
console.log((z *= 3)); // z = 3 * 3 -> z = 9let m = 6;
console.log((m /= 3)); // m = 6 / 3 -> m = 2let n = 7;
console.log((n %= 3)); // n = 7 % 3 -> n = 1
```

# 2.比较运算符

**比较**运算符是一个二元运算符。它比较两个操作数，并根据比较结果返回`true`或`false`。

一个比较运算符小于，或`<`。例如，`1 < 2`将返回`true`，因为`1`小于`2`。

当比较两个不同类型的值时，JavaScript 会做一个叫做**类型转换**的事情。这意味着，例如，如果你正在比较一个字符串和一个整数，JavaScript 将试图把字符串转换成一个数字，以便实际上可以比较这些值。有两个比较运算符**不**做类型转换:严格等于、`===`和严格不等于、`!==`。严格等于和严格不等于在执行运算之前不转换不同类型的值。

下面是 JavaScript 中的比较运算符表:

让我们来看看上述运算符的一些示例:

```
let x = 5;
let y = 2;
let z = 7;
let m = "5";
let n = "6";x == m; // 5 == "5" -> true
x != y; // 5 != 2 -> true
x === z; // 5 === 7 -> false
x !== m; // 5 !== "5" -> true
x > y; // 5 > 2 -> true
x >= z; // 5 >= 7 -> false
x < n; // 5 < "6" -> true
x <= m; // 5 <= "5" -> true
```

# 3.算术运算符

**算术**运算符可以是二元或一元运算符。作为二元运算符，它将两个数值作为操作数，执行算术运算，然后返回一个数值。作为一元运算符，它接受一个数值，执行一个运算，然后返回一个数值。

一个算术运算符是加号，`+`，用于将两个数相加。例如，`4 + 6`将返回`10`。下面是 JavaScript 中一些算术运算符的表格:

让我们来看看上述运算符的一些示例:

```
let x = 3;
let y = 5;
let z = 6;
let a = 2;
let b = 7;console.log(x + y); // 3 + 5 -> 8
console.log(y - x); // 5 - 3 -> 2
console.log(x * z); // 3 * 6 -> 18
console.log(z / x); // 6 / 3 -> 2
console.log(y % x); // 5 % 3 -> 2
console.log(a++); // 2
console.log(--b); // 6
console.log(y ** x); // 5 * 5 * 5 -> 125
```

# 4.逻辑运算符

一个**逻辑**运算符可以是一个二元运算符，也可以是一元运算符。作为二元运算符，它通常接受两个布尔值，对它们求值，然后返回一个布尔值。

JavaScript 中的一元逻辑运算符是逻辑 NOT。它接受一个操作数，并评估它是否可以转换为布尔值`true`。

下面是 JavaScript 中的逻辑运算符表:

让我们来看看上述运算符的一些示例:

```
true && true; // true
true && false; // false
false && false; // falsetrue || true; // true
true || false; // true
false || false; // false!true; // false
!false; // true
```

# 5.字符串运算符

一个**字符串**操作符是一个二元操作符。它接受两个字符串，并使用`+`将它们组合成一个字符串，在本例中称为*连接操作符*。字符串*串联*是指将两个字符串值组合在一起。

字符串操作符的一个例子是`console.log("Happy " + "birthday")`，控制台记录字符串`"Happy birthday"`。

字符串操作符还有一个缩短版，就是`+=`。例如:

```
let string1 = "birth";
let string2 = "day";
console.log(string1 += string2) // "birthday"
```

# 6.三元(条件)运算符

一个**条件**运算符，或三元运算符，用于三个操作数。它用于评估一个条件是否为真，然后根据这个条件返回两个值中的一个。

三元运算符的结构如下:

```
condition ? expressionIfTrue : expressionIfFalse
```

三元运算符将在本文中详细讨论[。](https://medium.com/javascript-in-plain-english/the-2-types-of-conditional-statements-in-javascript-ffd14dc96b8b)

这篇文章只是回顾了一些你将在 JavaScript 中使用和遇到的更常见的操作符。还有很多操作符，包括按位操作符和关系操作符，我鼓励你在 MDN 文档中了解更多关于它们的内容[这里](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators)。