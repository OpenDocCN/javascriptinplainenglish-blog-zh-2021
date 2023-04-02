# 你应该知道的酷 JavaScript 操作符

> 原文：<https://javascript.plainenglish.io/coolest-javascript-operators-you-wish-you-would-have-known-earlier-47a1185c58e2?source=collection_archive---------3----------------------->

![](img/8e205c8b8ad4be538ca8972a0007c772.png)

我用 JavaScript 写了很多代码，无论是在工作中还是在我的个人项目中。我经常遇到这样的情况，我不得不写许多样板代码来解决它们。例如，检查有效引用、空/未定义处理。但是最近我遇到了一些 JavaScript 操作者，他们让我的工作变得简单多了，在他们的帮助下，我可以写出更简洁的代码。

今天我将分享这些操作符，我相信你也可以用它们来编写更好的代码。

# **可选链接运算符(？。)**

如果您已经使用 JavaScript 很长时间了，那么您可能会遇到这个恼人的错误`Cannot read property '<property-name>' of undefined`。当您试图通过创建像`a.b.c.....`这样的链来访问一个位于对象深处的属性，而忘记检查链中是否存在中间值时，通常会遇到这个问题。

我们用一个恰当的例子来理解一下。

考虑一个`user`对象，它可以拥有用户的不同属性，比如地址和联系信息。`user`对象可以看起来像下面这样-

user object structure

这里，`currentAddress`属性对于一个用户来说可以是`undefined`，如果该用户目前居住在`permanentAddress`。

由于`user`对象是柔性的；我们必须添加手动检查来访问`currentAddress`中的`contact`信息，以避免如下`undefined`参考错误-

Traditional method to check for reference errors

现在，访问一个对象内部的值需要很多代码。想象一下，如果某个属性位于对象内部很深的位置，您将不得不编写大量的样板代码。

# 这就是可选的链接操作符(？。)前来救援。

根据 [MDN (Mozilla 开发者网络)文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)s:“****可选链接运算符(？。)*** *使您能够读取位于连接对象链深处的属性值，而不必检查链中的每个引用是否有效。”**

*简单地说，如果您使用可选的链接(？。)运算符，JavaScript 知道它首先必须检查链`user.addresses.currentAddress`是否有效。如果发现有效，则返回属性值；否则返回`undefined`。*

*可选的链接运算符(？。)会短路。这意味着一旦 JavaScript 发现一个无效/不存在的值，它就停止计算链中的属性。例如:在`user.addresses.currentAddress.contact`中，如果`currentAddress`不存在，那么 JavaScript 将不会计算其后的`contact`值，并将返回`undefined`作为输出。这种行为可以防止 JS 在访问无效属性时抛出错误。*

*因此，我们现在可以直接获得联系信息，而无需添加太多的样板代码。*

*Accessing properties using optional chaining*

*不仅如此，您还可以将它用于以下用途:*

*   *访问数组项，*
*   *进行函数调用*
*   *访问表达式*

```
*obj.val?.prop
obj.val?.[expr]
obj.arr?.[index]
obj.func?.(args)*
```

*真的不是很酷的运营商吗？让我们看看 JavaScript 中另一个很酷的操作符。*

# *零化合并算子(？？)*

*你是否厌倦了为处理`null/undefined`支票而写条件语句？*

*如果有一个操作符来减少样板代码会怎么样？为了更好地理解它的用例，让我们举几个例子:*

*代码 1:*

*Traditional method of Null/Undefined handling*

*代码 2:*

*Using Nullish Coalescing Operator*

*在上面的例子中，两个代码做同样的事情。当值为`null/undefined`时，它们返回一个默认值；否则看重自身。正如您将注意到的，使用代码 2 要干净得多，并且减少了许多样板文件。这就是无效合并运算符(？？)进入画面。*

*根据 [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)::*null ish 合并运算符(？？)是一个逻辑运算符，当其左侧操作数为* `*null*` *或* `*undefined*` *时，返回其右侧操作数，否则返回其左侧操作数。”**

*你们中的一些人可能会在这里争辩说，我们本可以使用**逻辑 OR 运算符(||)** 来代替。因为**或(|| )** 操作符返回第一个值，所以这在处理空检查时会非常有效，比如:*

```
*/* Using OR operator instead */
return (value || defaultValue);*
```

*然而，在使用 OR 运算符时有一个 **catch** 。*

*如果左侧值是`falsy`，OR 运算符返回右侧值，而不仅仅是`null/undefined`。JavaScript 中有六个值被认为是错误的。这些是:*

*   *`undefined`*
*   *`null`*
*   *`""`(空字符串)*
*   *`NaN`*
*   *0*
*   *`false`*

*因此，如果您使用 OR 运算符，它将返回默认值，即使该值不仅仅是`null/undefined`。这不是我们想要的。我们只想在我们的值为`null`或`undefined`时返回默认值。*

*当第一个操作数的计算结果为`null`或`undefined`(但没有其他错误值)时，nullish 合并操作符只返回第二个操作数，从而避免了这个缺陷。*

****提示:*** *当某个属性不存在于对象深处时，可以同时使用可选的链接和无效合并操作符来返回默认值。例如:**

*Using Optional Chaining and Nullish Coalescing Operator Parallely*

# *关键要点*

*   *当你需要访问一个对象深处的属性时，你可以使用**可选的链接操作符(？。)**避免因无效链导致的错误。*
*   *当您需要处理`null/undefined`检查时，您可以使用 **Nullish 合并运算符(？？)**避免编写不必要的条件检查。*

## *关于我*

*我的职业是软件工程师。我喜欢研究前端技术，比如 React、TypeScript。我是博客新手，喜欢与社区分享我的心得。我希望你会喜欢我的第一个博客。*

*如果你喜欢它的内容，请分享它来激励我写更多这样的东西。下一篇文章再见。*

**最初发布于*[*https://code slayer . hash node . dev*](https://codeslayer.hashnode.dev/coolest-javascript-operators)*。**