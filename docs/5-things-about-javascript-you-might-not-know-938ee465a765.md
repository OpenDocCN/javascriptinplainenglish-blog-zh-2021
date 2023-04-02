# 关于 JavaScript 你可能不知道的 5 件事

> 原文：<https://javascript.plainenglish.io/5-things-about-javascript-you-might-not-know-938ee465a765?source=collection_archive---------17----------------------->

## JavaScript 思想的食粮

![](img/fee1fdd06fc74ca002f0d1b22cc84f0d.png)

Photo by [Ben White](https://unsplash.com/@benwhitephotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是一种美丽的语言，它有自己的秘密，很多人会对此感到惊讶。尽管我们每天都在学习新的东西，但它从未停止给我们带来惊喜。这里收集了一些保守的 JavaScript 秘密。

# 1.NaN 是一个数字

你知道`NaN`是一个数字吗？对，没错！不是一个数(NaN)显然是一个数。

```
console.log(typeof NaN); //number
```

此外，NaN 甚至不等于它本身，也不等于任何其他对象。如果你必须检查任何东西是否是`NaN`，你需要使用`isNaN()`

```
NaN === NaN // falseisNaN(NaN) //true
```

# 2.void 运算符

JavaScript 中有一个`void`操作符，是的，你没听错。想知道它是做什么的？它接受后面的任何表达式，对其求值并总是返回`undefined`。听起来没用吗？我也是这么想的。

```
void {}; // undefinedvoid "any text at all"; // undefinedvoid (() => {}); // undefinedlet a = 0;void a; // undefined
```

我们真的需要这个愚蠢的接线员吗？令人惊讶的是，是的，这是必要的。用于定义`undefined`。我甚至不知道**未定义的**可以是**定义的**。

```
(() => {const undefined = "foo";console.log(undefined, typeof undefined); // "foo", "string"console.log(void 0, typeof void 0); // undefined, "undefined"})();
```

因为 undefined 不是一个关键字，所以它可以作为一个变量名使用，因此它可以在一定范围内覆盖全局变量。

# 3.立即调用函数表达式(IIFE)

我相信这不是什么大秘密。立即调用的函数表达式基本上是可以在定义后立即调用的函数。通常，一个生命由一个圆括号括起来，后面跟着另一个圆括号来调用定义的函数。

```
() => {// …})();
```

当一个函数有一个返回类型或者当它被赋值给一个变量时，并不总是需要圆括号。

```
void function () {// …}(); const result = function () {// …}();
```

# 4.in 运算符

JavaScript 中很少使用的操作符之一是`in`操作符。运算符的用途是检查一个对象是否包含某种属性。

```
let obj = { x: 1, y: 2, z: 3 };"x" in obj; // true"a" in obj; // false
```

那么，当人们可以使用 object[property]进行检查时，为什么还需要一个`in`操作符呢？它为检查是否存在任何属性提供了方便，即使它包含任何假值。在这种情况下，人们通常会使用:

```
typeof obj[prop] === "undefined"
```

除此之外，可以使用以下内容:

```
"prop" in obj
```

# 5.Null 是一个对象

我们都假设 null 基本上意味着没有对象，对吗？但是只要试着检查一下`null`的类型就可以了:

```
console.log(typeof null); //object
```

但是，`null`不是**而不是**被认为是一个对象的实例，因为`null`基本上没有任何值，因此它显然不是任何对象的实例。因此，

```
console.log(null instanceof Object); // false
```

# 结论

这些只是一些我真的不知道的 JavaScript 概念。如果你已经知道了其中的一些，或者你知道任何不太为人知的 JavaScript 秘密，让我们在评论中讨论吧:)