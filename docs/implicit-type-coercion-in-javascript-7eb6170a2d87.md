# JavaScript 中的隐式类型强制

> 原文：<https://javascript.plainenglish.io/implicit-type-coercion-in-javascript-7eb6170a2d87?source=collection_archive---------5----------------------->

## 要想在技术面试中胜出，你需要知道的关于隐式类型强制的一切

![](img/c73f72eb6b2715b8de19e8e26e9b8c8f.png)

Photo by [Cookie the Pom](https://unsplash.com/@cookiethepom?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

你对 JavaScript 中的隐式类型强制有什么了解？这个问题经常在初级开发人员的技术面试中出现。如果你不知道答案或者你以前从未听说过这个术语，他们可能会重新措辞: ***“如果你试图将 2 和‘2’相加，JavaScript 会输出什么？”***

这里不需要猜测，JavaScript 有时可能会输出不可预测的结果。虽然真的有可能！如果你对不可预测的结果感到好奇，请观看布莱恩·勒鲁的精彩视频:

你被问到的问题是一个非常合理的问题，你需要知道正确的答案。

# 类型强制

那么，什么是类型强制？

类型强制是将一个值从一种数据类型转换成另一种数据类型的过程

JavaScript 中有九种数据类型(根据最新 ECMAScript):未定义、null、boolean、string、number、bigInt、symbol、object 和 function。

你可能会听到有人说隐式或显式强制，尽管在这种情况下*类型强制*与*类型转换是混淆的。这些术语之间有细微的差别。当我们谈到*类型强制*时，总是 ***自动或隐式地将值从一种数据类型转换为另一种数据类型*** (想想 JavaScript 自动将字符串转换为数字)。*

*类型转换*(或类型转换)可以是隐式的，也可以是显式的。

如果我们在控制台中键入`“2” + 2`，JavaScript 会将 2 从一个数字强制转换成一个字符串，然后将这两个值连接在一起。输出将是`“22”`。JavaScript 没有将两个值都转换成数字，而是选择将它们转换成字符串。

如果我们希望我们的输出是`4`，那么我们必须使用 *Number()* 方法显式地将`“2”`转换成一个数字。在您的控制台中尝试:

`Number(“2”) + 2 // 4`

# 转换为字符串

现在让我们继续类型强制(*记住它总是隐式的！*)。在 JavaScript 的所有算术运算符中，加法运算符是最棘手的一个，当试图理解编译器如何转换数据时，它最有可能导致一些问题。

> 加法运算符产生数字操作数或字符串连接的和。

如果我们有两个数字，JavaScript 将输出这两个数字的和。但是如果只有一个值是数字，JavaScript 会将两个值都转换成字符串，并连接这些值。

```
"2" + 2 // "22""hi" + 2 // "hi2"[] + 2 // "2"
```

最后一个例子可能对你来说没有任何逻辑意义。我们有一个物体和一个数字。JavaScript 将`[]` 和`2`转换成字符串，并输出`“2”`。

如果我们尝试:

```
15 + 3 + "2" // "182"
```

JavaScript 从第一个值开始，这是一个数字。它将它与下一个值(也是一个数字)相加，然后检查第三个值的类型。因为第三个值是一个字符串，它连接了`18` 和`“2”`。所以输出会是`“182”`。

但是如果我们尝试:

```
"2" + 15 + 3 //"2153"
```

JavaScript 首先评估第一个值的数据类型，在本例中是字符串，然后检查第二个值的类型并将其转换为字符串，然后检查第三个值的类型并再次将其转换为字符串。

# 转换成数字

其余的算术运算符，如减法、乘法或除法运算符具有更可预测的行为。使用这些操作符的转换过程类似于调用`Number()` 方法。

在下面的例子中，JavaScript 在一个字符串上使用了`Number(“2”)`方法，并将其转换为一个数字，因此我们有以下输出:

```
"2" - 2 // 0"2" * 2 // 4"2" / 2 // 1
```

在下一个例子中,`“hi”` 不能被转换成数字，结果我们得到了`NaN` (不是数字)的输出:

```
"hi" - 2 // NaN"hi" * 2 // NaN"hi" / 2 // NaN
```

如果我们有一个数字和一个空对象`[]`，这个对象将被转换为 0。

在您的控制台中尝试:

```
[] - 2 // -2[] * 2 // 0[] / 2 // 0
```

在上面的例子中，我们看到了字符串和数字的转换。布尔人呢？

# 布尔转换

任何`true` 将被转换为 1，任何`false`将被转换为 0。

```
true + true // 21 + false // 1 !!("Hi there") // true !!(2) // true
```

*JavaScript 中的所有值都可以转换为 true，除了下面的*:

```
!!""!!0!!undefined!!null!!NaN!!false
```

***(提示:使用双 bang 将任意值转换为布尔值)。***

# 使用比较运算符的类型强制

这里还得提一下`==`和`===`。松散的`==`运算符将比较两个不同类型的值*，强制其中一个值的数据类型*比较相同的数据类型。

所以，`2 == "2" // true`。

大多数情况下，使用松散操作符是不可取的，您可能想知道是否要将数据与不同类型的数据进行比较。使用严格的`===`操作符将允许您比较值*，而无需首先对它们执行类型强制*。所以，`2 === "2" // false`。

# 结论

JavaScript 中的隐式类型强制可能是一个棘手的话题，如果您不确定 JavaScript 将如何对您的值执行类型强制，请首先在控制台中检查它们。

我希望我的博文能帮助你理解什么是隐式类型强制以及它是如何工作的。现在，我希望你能回答一个面试问题:

-如果你试图对 2 和 false 求和，输出会是什么？

`2 + false // 2`

**资源:**

[](https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion) [## 类型强制

### 类型强制是值从一种数据类型到另一种数据类型的自动或隐式转换(例如从字符串到…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion) [](https://developer.mozilla.org/en-US/docs/Glossary/Type_Conversion) [## 类型转换

### 类型转换(或类型转换)意味着将数据从一种数据类型转换为另一种数据类型。隐式转换发生在…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Glossary/Type_Conversion)