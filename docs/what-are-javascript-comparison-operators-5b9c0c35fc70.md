# 什么是 JavaScript 比较运算符？

> 原文：<https://javascript.plainenglish.io/what-are-javascript-comparison-operators-5b9c0c35fc70?source=collection_archive---------10----------------------->

## 了解 JavaScript 中比较运算符的所有知识。

![](img/96b23cb1e8d3c5fdfd950fcdcc86f09a.png)

# 比较运算符

在计算机科学中，比较运算符也称为关系运算符。这是一种编程语言结构或运算符，用于定义和测试两个对象之间的某种关系。这些包括数字相等，例如 5 = 5，和不相等，例如 4 ≥ 3。通常，如果两个操作数之间的条件关系成立或不成立，这些运算符的计算结果为 true 或 false。比较运算符可以理解为逻辑基的不同情况。

**JavaScript 中的比较运算符是这样写的:**

*   大于或小于:a > b，a < b.
*   Greater or less than or equals: a > = b，a <= b.
*   Equals: a == b, (Double equality sign) == means the equality test, though a single one a = b means an assignment.
*   Not equals, a! = b.

# Triple Equality sign (===)

This is a type of comparison operator, precisely an equality operator. We use it to compare two things to understand if they’re equal. We may use the equality operator to relate a variable with a string, a variable with a number, a variable with a math expression, or a variable with a variable. We can use it to compare various combinations. Below are all legal first lines in if statements:

```
if (fullName === "Mansoor" + " " + "Ahmed") {if (fullName === firstName + " " + "Mansoor") {if (fullName === firstName + " " + "Mansoor") {if (fullName === firstName + " " + lastName) {if (totalCost === 81.50 + 135) {if (totalCost === materialsCost + 135) {if (totalCost === materialsCost + laborCost) { if (x + y === a - b) {
```

The equality operator is case-sensitive. “Rose” does not equal “rose”, when we’re comparing strings. Another comparison operator, !==, is the opposite of ===.It means is not equal to.

```
1 if (myTicketNumber !== 487208) {2 alert("Better luck next time.");3 }
```

Alike ===, the not-equal operator can be used to compare numbers, strings, variables, math expressions, and combinations. Using the not-equal operator is case-sensitive, Like ===, string comparisons. It’s true that “Rose”! == “rose”. Following are 4 more comparison operators, typically used to compare numbers.

```
> is greater than< is less than>= is greater than or equal to<= is less than or equal to
```

# Result in Boolean

The boolean value is being returned by all comparison operators:

*   True: means “yes”, “correct” or “the truth”.
*   False: means “no”, “wrong” or “not the truth”.

False: means “no”, “wrong” or “not the truth

For example:

```
alert ( 2 > 1 ); // true (correct)alert ( 2 == 1); // false (wrong)alert( 2 != 1 ); // true (correct)
```

The result of a comparison can be assigned to a variable, same as any value:

```
let result = 6 > 5; // allocate the result of the comparisonalert ( result); // true
```

# String comparison

[JavaScript](https://www.technologiesinindustry4.com/) 使用假定的“字典”或“词典编纂”顺序来了解一个字符串是否大于另一个字符串。字符串是一个字母接一个字母的。

例如，比较两个字符串的算法很简单:

1.  关联两个字符串的第一个字符。
2.  如果第一个字符串的第一个字符大于或小于其他字符串，则第一个字符串大于或小于第二个字符串。我们完成了。
3.  然后，如果两个字符串的第一个字符相同，以同样的方式比较第二个字符。
4.  重复，直到任何字符串结束。
5.  如果两个字符串以相同的长度结束，则它们相等。否则，字符串越长越大。

# 不同类型的比较

当链接不同类型的值时，JavaScript 将这些值更改为数字。

例如:

```
alert( '2' > 1 ); // true, string '2' becomes a number 2alert( '01' == 1 ); // true, string '01' becomes a number 1
```

对于布尔值，True 变为 1，false 变为 0。例如:

```
alert( true == 1 ); // truealert ( false == 0); // true
```

严格平等

常规的等式检查==可能无法区分 0 和 false:

```
alert ( 0 == false); // true
```

空字符串也会发生类似的情况:

```
alert(‘‘ == false ); // true
```

这是因为不同类型的操作数被相等运算符==转换为数字。就像 false 一样，空字符串会变成零。如果我们想区分 0 和错误，需要准备什么？固定相等运算符===在不进行类型转换的情况下检查相等。我们可以换句话说，如果 a 和 b 是不同的类型，那么 a === b 直接返回 false，而没有尝试转换它们。让我们尝试一下:

alert(0 = = = false)；// false，由于类型不同。还有一个“严格不相等”运算符！==类比于！=.公司等式操作符写起来有点长。它清楚地说明了正在发生的事情，减少了出错的空间。

# 与 null 和 undefined 的比较

当 null 或 undefined 与其他值比较时，会有一种不直观的行为。

由于它们中的每一个都进行了严格的相等检查===这些值不同是不同的类型。alert(null = = = undefined)；//假

如果非严格检查==有一个特殊的规则。这两个是“甜蜜的一对”。他们彼此平等。它们确实没有任何其他价值。alert(null = = undefined)；//真。Null 变成 0，undefined 变成 NaN 用于数学和其他比较< > < = > = null 或 undefined 转换成数字。当我们应用这些规则时，让我们看看会发生什么。其他人是最重要的，如何不陷入他们的陷阱。

奇怪的结果:null vs 0

让我们比较 null 和零:

```
alert( null > 0 ); // (1) falsealert( null == 0 ); // (2) falsealert (null >= 0 ); // (3) true
```

最后的结果形成“null 大于或等于零”。因此，在上面的一个比较中，它肯定是真的，但它们都是假的。原因是等式检查==和比较>< > = <= work differently. Comparisons convert null to a number, treating it as 0\. That’s why (3) null > = 0 为真，而(1) null > 0 为假。

***更多详情请访问:****[*https://www . technologiesinindustry 4 . com/2021/01/what-are-JavaScript-comparison-operators . html*](https://www.technologiesinindustry4.com/2021/01/what-are-javascript-comparison-operators.html)*

**更多内容看* [***说白了. io***](http://plainenglish.io/)*