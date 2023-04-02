# 揭秘 5 个奇怪的 JavaScript 怪癖

> 原文：<https://javascript.plainenglish.io/top-5-strange-javascript-quirks-demystified-61edd3e1f3a9?source=collection_archive---------9----------------------->

## JavaScript 可能很奇怪。我们来揭秘一些怪癖吧！

JavaScript 是一种有趣的语言，有着不可思议的可能性。然而，它不是没有怪癖的，不是吗？让我们来看看 JavaScript 中一些我们最喜欢的有趣的怪癖。

![](img/ac68c4501a2667eaa9df63b5b699b1b6.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 1.逻辑比较

如果`a == b`和`b == c`，那么肯定，`a == c`，对吗？让我们找出并打开我们的 JavaScript 控制台。

```
> 0 == "0"
**< true**> 0 == []
**< true**> "0" == []
**< false**
```

显然，JavaScript 并不总是这样！只有两个等号的抽象比较将根据等式左边和右边的数据类型而不同地工作。因为我们使用不同的数据类型，所以行为会有所不同。

我们可以深入研究 [EcmaScript 抽象等式文档](https://262.ecma-international.org/11.0/#sec-abstract-equality-comparison)。在这里，我们将找到不同数据类型的等式背后的确切逻辑。

这就是为什么在 JavaScript 中使用抽象等式通常不是一个好的实践。如果我们用严格的等式进行同样的尝试，我们应该会得到更稳定的结果。让我们来看看。

```
> 0 === "0"
**< false**> 0 === []
**< false**> "0" === []
**< false**
```

这个看起来好多了。数据类型都不一样，所以严格的等式总是会返回`false`。尽可能使用严格的等式。

# 2.真的，还假的？

在这个例子中，让我们对一个字符串做一些等式检查。

```
> "abc" == true
**< false**
```

一个字符串不是真的，我们不会期望有什么不同。这是有道理的。如果为假，下面的 if 语句就不应该执行，对吗？

```
> if ("abc") { console.log("'abc' is true!"); }
**< 'abc' is true!**
```

等等，我们不是刚看到结果是假的吗？那么为什么要执行这条语句呢？如果我们使用双重否定技巧把它转换成一个布尔值，让我们也来看看这个值。如果你对此不熟悉，这将返回变量的负值，通过再次取反，我们得到变量的布尔值。

```
> !!"abc"
**< true**
```

那么，这是真的？让我们把这些方程放在一起，试着弄清楚。

```
> "abc" == true
**< false**> !!"abc"
**< true**> if ("abc") { console.log("'abc' is true!"); }
**< 'abc' is true!**
```

那么变量是不是既有`true`又有`false`？不完全是。当我们用一个`if`比较一个字符串的值时，JavaScript 会比较实际的字符串值。非空字符串将返回`true`，空字符串将返回`false`。在我们的例子中，`"abc"`不为空，返回`true`。

好吧，但是`"abc" == true`返回`false`呢？类似于我们解释的第一个 JavaScript 怪癖，EcmaScript 对抽象等式有一个定义，根据变量类型的不同，行为会有所不同。在本例中，`"abc" == true`，两边都将被转换成数字，根据 EcmaScript 定义。

我们可以在我们这边模拟这个数字转换，使用`Number(obj)`函数。

```
> Number("abc")
**< NaN**> Number(true)
**< 1**> NaN === 1
**< false**
```

这类似于 JavaScript 正在做的事情，解释了`false`值。

在这种情况下，严格的平等不会解决这个问题。这不是一个真正的问题，而是 JavaScript 的一个特性。当你在一个 if 中使用一个字符串时，它会检查这个字符串是否为空，这使得字符串值的检查变得容易。

```
let termsAndConditions = "Nobody really reads this!";if (termsAndConditions) {
    showTermsAndConditions();
}
```

这是一个非常有用的特性，但是开发人员应该注意比较中的不同行为，这在开始时可能会非常混乱。

# 3.一个数组，不是一个数组？

我们确实希望编程语言有逻辑意义。让我们深入 JavaScript 控制台，测试一些逻辑。

```
> 1 == 1
**< true**
```

很有道理，`1`应该等于本身，一。接下来看看`1`是否不等于`1`。

```
> 1 != 1
**< false**> 1 == !1
**< false**
```

目前为止一切顺利，JavaScript！简单的逻辑做得很好。

但是数组呢？让我们看看一个数组是否等于它自己。

```
> [] == []
**< false**
```

数组不是数组？等一下！数组通过引用工作，这意味着我们实际上是在比较引用。由于我们实例化了两个空数组，所以它们在内存中的地址会不同，比较的结果会是`false`。为了真正地将数组与其自身进行比较，我们必须先将数组赋给一个变量，然后才能进行比较。

```
> let array = [];
> array == array
**< true**
```

好吧，一个数组等于它自己！让我们继续进行与`1`相同的测试。接下来让我们试试阴性测试。我们现在知道了`[] == [] -> false`，那么`[] != []`应该就是`true`了吧？既然是相反的，大部分逻辑都是这样的。让我们找出答案。

```
> [] == ![]
**< true**> [] != []
**< true**
```

好吧，有道理。一个`false`方程的反义词是`true`。但是，这里不是有语义上的奇怪吗？

```
> [] == ![]
**< true**
```

一个数组，是，嗯..不是数组！**JavaScript 确认，并加盖批准章。**

为了理解幕后发生的事情，我们需要看一下抽象等式的 EcmaScript 定义。

如果我们遵循这个流程，我们知道左边的数组将被转换成一个原始的数字类型，类似于我们之前讨论的怪癖。

```
> [] == ![]
*> Number([]) == Number(![])
> 0 == 0*
**< true**
```

Denys Dovhan 在 [Wtfjs 中也解释了这个 JavaScript 怪癖，这是一个非常大的 JavaScript 怪癖列表。](https://github.com/denysdovhan/wtfjs#-is-equal-)

# 4.A+数学！

让我们来测试你的数学！什么是`0.1 + 0.2`？这是一个经典，但我不得不把它包括在这篇文章中。

准备好答案后向下滚动。

![](img/d81f8c8ec860ac6149f88d36d7ca63aa.png)

Photo by [Maxim Ilyahov](https://unsplash.com/@glvrdru?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你认为`0.3`，那么你错了，至少按照 JavaScript 的标准是这样的！让我们再次将它放入 JavaScript 控制台。

```
> (0.1 + 0.2) == 0.3
**< false**
```

他们在学校教我们的数学一直都是错的。JavaScript 知道得更多。那么`0.1 + 0.2`到底是什么呢？

```
> 0.1 + 0.2
**< 0.30000000000000004**
```

好吧，这个很明显。当然`0.1 + 0.2`等于`0.30000000000000004`。就像`0.3 + 0.3`等于`0.60000000000000008`一样，对吧？

```
> 0.3 + 0.3
**< 0.6**
```

也许不是，这看起来像是另一个 JavaScript 怪癖，等待去神秘化！别担心，我们的数学知识是安全可靠的。为了好玩，我们再试一次。

```
> 0.1 + 0.2
**< 0.30000000000000004**> (0.1 + 0.2) * 2
**< 0.6000000000000001**
```

JavaScript 只是在嘲笑我们！小数，`4 * 2`当然等于`10`..那么，这里到底发生了什么？

计算机计数的方式和人类不太一样，尤其是十进制数。我们习惯于使用以 10 为基数的十进制系统，然而，计算机使用以 2 为基数的十进制系统，使用位和字节。这个系统不能很好地处理低位小数。对于幕后发生的事情的更详细的解释，我强烈推荐 TechTalkBook 的这篇文章。

请记住，在 JavaScript 中，十进制计算并不总是准确的。为了解决这个，可以使用额外的 npm 包比如 [big.js](https://www.npmjs.com/package/big.js) ，它会进行更精确的小数计算。

# 5.加号不是减号的反义词？

让我们来玩玩 JavaScript 中的加号和减号，然后打开控制台。

```
> '9' - 1
**< 8**
```

这很有希望，JavaScript 理解一个字符串`'9'`可以是一个数字`9`，并减去 1。虽然这种方法可行，但是要注意数据类型，这绝对不是推荐的方法。如果它和负号一起工作，它应该和正号一起工作，对吗？让我们试一试。

```
> '9' + 1
**< "91"**
```

我们得到一个带有值`"91"`的字符串结果，这不是我们所期望的，因为加号是减号的反义词。

原因是`+`操作符不仅仅是一个加号。它也是 JavaScript 中的串联运算符。JavaScript 很困惑，因为通常一个字符串和一个`+`组合在一起会导致串联，但另一个参数是一个数字。因此，JavaScript 试图将数字转换成字符串，并将它们连接在一起。

这是 JavaScript 中数据类型的又一个陷阱。注意始终使用正确的数据类型，并在必要时进行显式转换。

Wtfjs 也在他们的列表中描述了这个行为。他们的怪癖清单真的很完整。

# 结论

JavaScript 是一种有无数可能性的语言。因为它提供了一些自由，所以它也有一些怪癖。

我们可以从上述怪癖中吸取一些教训:

*   作为开发人员，尽可能避免抽象等式`==`，使用严格等式`===`代替。
*   虽然一个语句可以计算为`true`，但是在`if`中使用一个变量会有不同的结果，并且通常是在变量非空的情况下。
*   当处理小十进制数时，使用库来确保数学是准确的。
*   注意数据类型，确保在必要时转换数据类型，并尽量避免混合数据类型。

# 额外资源

如果你渴望更多的怪癖和它们的解释，看看下面的资源。

*   [Wtfjs:Denys dov Han](https://github.com/denysdovhan/wtfjs)[的一长串 JavaScript 怪癖](https://github.com/denysdovhan)
*   [JavaScript 等式表](https://dorey.github.io/JavaScript-Equality-Table/)由 [Dorey](https://github.com/dorey)
*   [Big.js](http://big.js) ，由 [MikeMcl](https://github.com/MikeMcl) 开发的精确数学库

[订阅我的媒介](https://kevinvr.medium.com/membership)到**解锁** **所有** **文章**。通过使用我的链接订阅，你是支持我的工作，没有额外的费用。你会得到我永远的感激。