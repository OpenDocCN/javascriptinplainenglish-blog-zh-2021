# JavaScript 中的类型转换:魔力

> 原文：<https://javascript.plainenglish.io/type-conversion-in-javascript-the-magic-c93cf96ba4da?source=collection_archive---------10----------------------->

![](img/725e588529ef5beb79264a7c096acb53.png)

image Credit : Instagram — @chris.lawton

如果你是一名 JavaScript 开发者，那么你一定知道 JavaScript 有三种基本类型:****字符串*** 和 ***布尔。****

*但是你知道吗，这些类型是互相转换来执行某个程序的。这种现象被称为**类型转换。***

*JavaScript 类型转换有两种方式；*

1.  ***隐式***
2.  ***明确地***

*让我们来探索这每一个；*

# *1.隐式类型转换*

*JavaScript 的对象和函数自动将值转换为特定操作的正确类型。例如:*

*当你执行一个 **console.log()** 时，表达式自动转换成字符串:*

```
***const** num = 1001;  // num is a number
**console**.**log**(num) //> 1001
//? This num has become a ***string*** to print.**console**.**log**("20"+"10") //> 2010
**console**.**log**("20"-"10") //> 10  (same for * and /)
//? Here + operator simple concatenate the "20" and "10" as string and give 2010,whereas - operator converts the values into number to give output 10.*
```

*同样适用于 **alert()** 。这也会转换字符串中的值。*

```
***const** isAlive = true:
**alert**(isAlive)  //> true
//? This isAlive has become ***string****
```

*当您使用 if 执行条件操作时，也会发生这种隐式类型转换..否则就换。*

*如果 块内的表达式被转换成布尔型来执行运算。*

```
***const** point = 100;**if(**point**) {** 
  console.log(`You have ${point} points`)
**} else {**
  console.log(`Collect some point first`)
**}
/**/? though point in number but it converts in **boolean(true)**
//! Since we know all the positive number is true except 0
// the output will be console.log(`You have ${point} points`)*
```

*顺便说一下，如果你不知道这个``和${}，它们被称为**模板文字**。这是 ES6 中的新特性。这是一个非常方便的记录语句的工具。一定要去看看。*

*一些更多的函数和操作符也做这种隐式类型转换，但这不是我们所关心的。我们不需要担心所有的功能，但是如果你想了解它们，你可以通过做一些研究来了解它们。*

*让我们探索另一个:*

# *2.显式类型转换*

*在这里，我们通过使用一些操作符和构造函数来手动转换不同类型的值。*

## *Number()构造函数*

*这将表达式转换成数字。*

***转换规则:***

```
***undefined** converts into ***NaN***
**null** converts into ***0***
**""** converts into ***0***
**true** converts into ***1***
**false** converts into ***0***
**string** converts into ***NaN****
```

***例如:***

```
***const** input = true;
**const** output = **Number**(input);
**console.log**(input);  //>true
**console.log**(output); //>1
**//?** The Number constructor converts the **boolean** value **true** of input into **numeric** value **1***
```

***更多例子:***

```
***let** value;
console.log(value);  //>**undefined**
console.log(Number(value));   //>**NaN** (Not a Number)value = null;
console.log(value);  //>**null**
console.log(Number(value));   //>**0**value = "";
console.log(value);  //>""
console.log(Number(value));   //>**0**value = "1to4";
console.log(value);  //>"1to4"
console.log(Number(value));   //>NaN [ to is string ]*
```

## *String()构造函数*

*这将表达式转换成字符串。*

*示例:*

```
*let isAlive = true;
console.log(isAlive);  //>true
console.log(typeof isAlive);  //> booleanisAlive = String(isAlive);
console.log(isAlive);  //>true
console.log(typeof isAlive);  //> string//> Thought **typeof(isAlive)**, second time, is true, but this true is not boolean, it's a string due to **String()***
```

*任何传入 string()的东西都会变成 String，不管它以前是什么。*

## *布尔()构造函数*

*这将把表达式转换成布尔值。*

***转换规则:***

```
***0, "", undefined, null, NaN** covert into **0**
**others than above** convert into **1***
```

***示例:***

```
*console.log(Boolean(0)); //> false
console.log(Boolean(123)); //> true
console.log(Boolean('wooh')); //> true
console.log(Boolean("")); //> false
console.log(Boolean([])); //> true
console.log(Boolean("0")); //> true
**//? Last one :** Here the **quote** is not empty, it has a **value "0"**.
That's why it returns **true** rather than false*
```

*除了 Number()、String()、Boolean()之类的类型构造函数之外，还有一些运算符可以转换值的类型。*

*Like +运算符。*

*看一看:*

```
*console.log(2 + "2");  //> 22
console.log(2 + +"2");  //>4*
```

*但是为什么会这样呢？*

**在表达式****2 ++ 2****中，多出来的* ***+*** *运算符放在“2”之前，迫使“2”变成了***。因此结果是 4 而不是 22***

# **结论**

**在 JavaScript 中有三种类型:数字、字符串和布尔值。**

**对于隐式类型转换，JavaScript 编译器会自己处理，不会打扰我们。对于显式类型转换，我们使用名为 Number()，String()和 Boolean()的类型构造函数。**

**这就是 JavaScript 中的类型转换。**

**我会在下一篇文章中看到你。现在，继续阅读，继续学习。**

***更多内容看*[***plain English . io***](http://plainenglish.io)**