# JavaScript:特殊数字

> 原文：<https://javascript.plainenglish.io/javascript-special-numbers-404dd5bf5f20?source=collection_archive---------15----------------------->

## JavaScript 中特殊数字的简短意识流

![](img/7f568650d890b3fc583896d6a9ac7555.png)

Photo by [Alexander Sinn](https://unsplash.com/@swimstaralex?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我第一个承认数学和我合不来。这并不是说我不擅长，也不是说我不喜欢，更多的是，有时，当编码时，它的行为与我预期的不同，因为我把我的期望强加于它，所以我是失望的一方(*我感觉治疗会议即将到来#toxicrelationship* )。嗯，你可以想象当我被介绍给 JavaScript 中的`[NaN](https://en.wikipedia.org/wiki/NaN)`时我的懊恼。您也可以想象当我运行这段代码时，我的困惑/烦恼是如何增长的…

```
console.log(typeof(NaN));
// number
```

如果 NaN 代表“不是数字”，那么为什么 JavaScript 告诉我它是“数字”类型的？

## 圆盘烤饼

这是因为从 JavaScript 的角度来看，它是数字类型的。它代表一个无效的响应，但它不是`null`、`undefined`或不同的类型；因此，上面的代码是这样运行的。JavaScript 需要一种方式来告诉程序员正在运行的方程返回一个无法表示的值，例如:

```
0 / 0;
// NaNMath.sqrt(-4);
// NaN
```

这让我不禁要问，JavaScript 还包含哪些特殊数字？

谢天谢地，没有那么多。

以下是使用 JS 产生特殊数字的几个问题:

```
let zero = 0;let i = 1 / zero; 
// Infinitylet negI = -i; 
// -Infinitylet negZero = 1 / negI; 
// -0
```

## 无穷大&-无穷大

`[Infinity](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity)` [&](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity) `[-Infinity](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity)`是 JS 中全局对象的属性，代表无穷大的数值。

> `Infinity`是一个错误值，表示两个问题之一:一个数因为量值太大而无法表示，或者发生了被零除的情况。
> 
> `Infinity`大于任何其他数字(除了`NaN`)。同样，`-Infinity`比其他任何数都小(除了`NaN`)。
> 
> ——[**speakingjs.com**](http://speakingjs.com/es5/ch11.html)

## +0 & -0

现在，这个让我有点困惑。在 JS 中并不真正需要正负零，但是它们确实存在。发生这种情况是因为使用 IEEE-754 格式的数字是如何分配比特的(单独的主题是另一篇文章), 1 比特被分配给数字的符号。

> 因为 JavaScript 的数字保持大小和符号分开，所以每个非负数都有一个负数，包括`0`。
> 
> 这样做的基本原理是，无论何时用数字表示一个数字，它都可能变得很小，以至于与 0 无法区分，因为编码不够精确，无法表示差异。然后一个有符号的零允许你记录“从哪个方向”你接近零；也就是说，这个数在被认为是零之前有什么符号。维基百科很好地总结了[带符号零](http://en.wikipedia.org/wiki/Signed_zero)的利弊:
> 
> *据称，在 IEEE 754 中包含带符号零使得在一些关键问题中更容易实现数值精度，特别是在使用复杂初等函数进行计算时。另一方面，有符号零的概念与大多数数学领域(以及大多数数学课程)中的一般假设相反，即负零与零是一回事。允许负零的表示可能是程序中错误的来源，因为软件开发人员没有意识到(或者可能忘记)虽然两个零表示在数字比较下表现为相等，但是它们是不同的位模式，并且在某些操作中产生不同的结果。*
> 
> ——**[**speakingjs.com**](http://speakingjs.com/es5/ch11.html)**

**我也喜欢德里克·奥斯汀博士在这个问题上的发现:**

> **自然，存在一个不完全为零的单独的零值有点令人费解。为什么 IEEE 标准会包含两个零？**
> 
> **用户[阿戈斯顿·霍瓦特](https://stackoverflow.com/users/493759/agoston-horvath)解释了[堆栈溢出](https://stackoverflow.com/questions/7223359/are-0-and-0-the-same)的原因:**
> 
> ***“其实这个行为模型在数学上限制了计算。例如，函数 1/x 在 0 中有一个无穷大的值，然而，如果我们从正的一面或负的一面接近 0，它就分离了；前者，结果是+inf，后者，-inf。”***
> 
> **但是应该是那样吗？Chris Hemedinger 在 2ality 博客上的评论[中认为这种行为令人困惑:](https://2ality.com/2012/03/signedzero.html)**
> 
> ***“零[0]有两种或两种以上的表示，这是 IEEE-754、符号和幅度表示以及补码表示的公认缺陷。”***
> 
> **其他一些编程语言使用一种叫做[二进制补码](https://en.wikipedia.org/wiki/Signed_number_representations#Two.27s_complement)的东西来避免对两个零的需求。**
> 
> **然而，JavaScript 有两个不同的零，`+0`和`-0`。**
> 
> **— [**德里克·奥斯汀博士**](https://medium.com/coding-at-dawn/is-negative-zero-0-a-number-in-javascript-c62739f80114)**

**在 JS 中运行不同的方程时，你可能会发现许多意想不到的行为，比如`0.1 + 0.2 === 0.3`返回`false`，这是因为我们在日常生活中通常使用[基数为 10 的数制](https://en.wikipedia.org/wiki/Decimal)，而计算机使用[基数为 2 的数制或二进制数制](https://en.wikipedia.org/wiki/Binary_number)。然后，当你加上 JavaScript 遵循 [IEEE-754](https://en.wikipedia.org/wiki/IEEE_754) 格式进行[浮点运算](https://en.wikipedia.org/wiki/Floating-point_arithmetic)的事实时，你就有了一个比我在副标题为“Brief”的博客中所能概括的更复杂的答案。然而，下面有一些我觉得有趣的进一步阅读，围绕着数学和 JS 的细节。**

****要点提示** : *由于 JavaScript 查看数字的精度有限，所有这些特殊数字有时是 JavaScript 表示操作结果的唯一方式。* *你偶尔会碰到* `*NaN*` *，很少会碰到这里列出的其他特殊号码。这可能会在面试中出现，但也可能不会。但是，如果是的话，你现在有一些 JS 琐事技能可以炫耀了。*💡**

**快乐编码🤓**

# **进一步阅读**

*   **[‘这里是你需要知道的关于 JavaScript 的数字类型](https://indepth.dev/posts/1139/here-is-what-you-need-to-know-about-javascripts-number-type)’
    ——[马克斯·科瑞茨基](https://twitter.com/@maxkoretskyi)**
*   **['浮点数学](https://0.30000000000000004.com/) '
    — [埃里克·威芬](http://erik.wiffin.com/)**
*   **[“每个 JavaScript 开发人员应该知道的关于浮点的知识](https://modernweb.com/what-every-javascript-developer-should-know-about-floating-points/)”
    —[Brian rina ldi](https://twitter.com/remotesynth)**
*   **什么是二进制，为什么计算机要使用它？’
    ——[安东尼·赫丁斯](https://twitter.com/anthonyheddings)**