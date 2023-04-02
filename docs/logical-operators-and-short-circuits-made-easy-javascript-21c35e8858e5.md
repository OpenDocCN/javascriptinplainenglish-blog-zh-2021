# 逻辑运算符和短路变得简单——JavaScript

> 原文：<https://javascript.plainenglish.io/logical-operators-and-short-circuits-made-easy-javascript-21c35e8858e5?source=collection_archive---------16----------------------->

## 掌握“&&”、“||”和“？?"

![](img/b955fe53ae0d5d832b0cd50473fd027e.png)

Foto di [Daniel Reche](https://www.pexels.com/it-it/@daniel-reche-718241?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) da [Pexels](https://www.pexels.com/it-it/foto/lampadina-gialla-1556704/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

```
**TABLE OF CONTENTS**1\. [*Introduction*](#5257)2\. [*Examples*](#12dc)3\. [*Explanation*](#cba6)4.[*Short-circuit evaluations*](#ccb9)5.[*OR “||” and Nullish Coalescing Operator “??”*](#f60c)6\. [*Recap and conclusion*](#3c72)7\. [Resources](#5e3d)
```

# **简介**

这些运算符不返回布尔值！我说了…至少不一定。只是*他们让他们这么做*，这不是他们的错，他们通常不会这么做。

玩笑归玩笑，**二元逻辑操作符**是你接触 Javascript 时最先学会的东西之一，乍一看，它们看起来很简单……但是过一段时间后，你很可能会开始对它们的确切工作方式感到困惑，尤其是当你开始将它们视为 *if…else* 条件句的替代品时。

让我给你一个简单可靠的方法来帮助你。我将首先关注逻辑操作符“& &”(AND)，以便我们稍后可以使用我们在第一部分中学到的知识来处理其他两个操作符。我们走吧！

# 例子

让我们从这些操作符最常见的用例开始，可能你已经知道其中一些的结果。在你的浏览器控制台上玩一会儿，试着从广义上理解它们是如何工作的。

# 说明

逻辑运算总是从左向右求值，它们由**一个** **运算符** ( *例如*&&或“||”)和**两个** **操作数**组成，分别位于其左右两侧。左边的是第一个操作数*右边的是第二个操作数**。*

## *第一法则*

为了容易理解，你必须记住的第一条 **关键规则**是:

```
a logical operator always returns one of the 2 operands
```

它不一定返回布尔类型或任何预设类型，它只是返回*逻辑运算*的两个操作数之一:左或右。很简单。

## 第二条规则

要知道运算将返回两个操作数中的哪一个，就得看**第一个操作数**。对于& &操作符:

```
- if it’s a [falsy value](https://developer.mozilla.org/en-US/docs/Glossary/Falsy), it will return the first operand;
*(example 1.2: bar gets assigned b, because b is the first and falsy, so it gets returned)*- if it’s a [truthy value](https://developer.mozilla.org/en-US/docs/Glossary/Truthy), it will return the second operand;
(*example 1.1: foo gets assigned b, because the first operand is truthy and so the second, b, gets returned*)
```

记住这两条规则，你就拥有了掌握这个话题的一切。例如，你已经可以理解和解决任何类似于例 1(赋值)中的运算。我们来看最后一步，通常是困惑的原因。

## 布尔值

也许你现在想知道:它们有时是如何返回真的或假的呢？你不是说他们总是返回左或右操作数吗？是的，它们返回两个操作数中的一个，但是在这些情况下，它们被强制将返回值转换为布尔值。

以下是倒数第三个要点:

```
they return *true* or *false* only when coerced to boolean values
```

当它们与布尔值*一起使用时，它们会——令人惊讶地——返回一个布尔值。例如，再看看例 2:*

一个*中的*条件*如果...else* 将括号内的内容转换(强制)为布尔值，因此使用我们所学的内容:

1.  `c`和`d`是两个操作数
2.  `first operand`为真，所以第二个操作数被返回
3.  括号之间的 *if 条件*将返回值`d`(第二个操作数)强制转换为布尔值:`d`在这种情况下已经是一个布尔值(但是任何 false 值都将被转换为 false)，因此 *false* 将被返回，因此条件变为 false，并且`else block`将被执行

第二个和第三个规则的结果是，当" &&" 与布尔值一起使用时:

*   如果两个操作数都为真，运算将返回真
*   如果其中一个或两个都是 false，操作将返回 false

# 短路评估

现在我们准备处理逻辑操作符的“最棘手”的用法，*短路评估*。让我们为“& &”运算符收回第 2 条规则:

```
- if the first operand is truthy, the second operand gets returned

- if the first operand is falsy, it gets directly returned
```

这意味着当第一个操作数为 falsy 时，第二个操作数甚至不会被计算，因为返回值只能是第一个操作数，所以 JS 计算第二个操作数是没有意义的。这就是所谓的**短路**因为它只需要在第一个操作数为 falsy 时对其求值，跳过第二个，使其*短路*。

这也意味着如果第一个操作数为真，那么第二个操作数将被求值(并返回)。让我们看看第 3 个例子:

例 3.1: `a`是一个真值，所以第二个操作数`console.log`被求值并返回。
例 3.2: `d`为 false，那么将立即返回 false 并跳过第二个操作数。

现在，简而言之，我们通常不关心操作的**返回值**，因为正如你可能已经注意到的，操作没有被赋值给任何变量或者没有被强制为布尔值，所以返回值会丢失。

相反，我们对逻辑运算的**副作用**感兴趣:在我们的例子中，副作用是`console.log()`。这是一个副作用，因为我们认为逻辑运算可能会根据第一个操作数的值返回第二个操作数，为此，它首先需要计算并运行第二个操作数！

这允许我们将任何函数或表达式作为第二个操作数运行:如果左边的值为 falsy，函数将不运行，而如果为 true，函数将运行。所以可以作为 **if 语句**的简写(不带 *else* )。例如，如果第一个操作数为真，可以执行如下操作:

```
truthy && doSomething();
```

我发现这是一种非常简洁的方式来创建条件，避免在不需要的时候使用冗长的 if 语句。请记住，很多开发人员不喜欢以这种方式使用逻辑运算符来替换条件语句，但是我和我的团队使用它没有问题，所以这完全取决于团队和个人的偏好。不管你是否会这样使用它们，了解它们仍然很重要。

# 或者“||”和无效合并运算符”？?"

我们终于可以用目前所学的知识来讨论最后的 **2 个二元逻辑运算符**。有趣的是，我们上面所说的，对这些操作者也是有效的，所以除了对每个操作者确实特定的不同的**规则 n. 2** 之外，没有什么可说的:

## “||”运算符

```
- if the first operand is truthy, it will get returned- if the first operand is falsy, the second operand will get returned
```

因此，当与布尔值一起使用时，如果两个操作数中的一个或两个为*真*，则逻辑运算的结果将为*真*；否则永远是假的。

例如，这个操作符很适合在某个东西为假时分配*回退值*:`let a = falsy_value || 10;``a`在这种情况下将为`10`。但是您也可以使用它来有条件地运行函数。

## "??"操作员

```
- if the first operand is anything but *null* or *undefined*, it will get returned- if the first operand is *null* or *undefined*, the second operand will get returned
```

该操作符对于将*回退值*分配给变量也很有用，特别是当您的变量打算接受 falsy 值，但从不接受*未定义的*或 *null* : `let b = 0 ?? 10;` `b`将为`0`，因为 falsy 值被接受——不包括前面提到的两个值。

## 例子

如您所见，除了返回值的不同规则之外，其余内容仍然适用。让我们看一些最后的例子，并尝试使用我们在上面学到的规则:

# 总结和结论

这篇文章最终比预期的要长，但是尽管篇幅很长，我还是试图让它尽可能的线性和清晰。我希望它有帮助。如果你从现在开始遵循这些步骤，你就不会再出错了:

1.  识别 2 个操作数
2.  检查第一个操作数值，并通过对所使用的运算符应用特定的规则来确定将返回哪个操作数
3.  看看逻辑运算是否被强制为布尔运算(*，例如*在 *if 条件*中，或者 *for loop 条件*):如果是，研究 truthy 和 falsy 值，总是知道结果会是什么
4.  如果逻辑运算没有被强制为布尔值，或者它的返回值没有被任何东西收集，那么它很可能被用作一个短路，它的第二个操作数将根据所用运算符的特定规则进行计算和运行

很符合逻辑，不是吗？😊

```
**Resources**:- [Javascript.info: logical operators](https://javascript.info/logical-operators)- [MDN: binary logical operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators#binary_logical_operators)- MDN: [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) and [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) values- MDN: new logical assignment syntax for [&&](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators), [||](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR_assignment), and [??](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_nullish_assignment)
```

*更多内容请看*[***plain English . io***](http://plainenglish.io/)