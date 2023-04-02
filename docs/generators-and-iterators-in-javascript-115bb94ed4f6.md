# JavaScript 中的生成器和迭代器

> 原文：<https://javascript.plainenglish.io/generators-and-iterators-in-javascript-115bb94ed4f6?source=collection_archive---------7----------------------->

## 代码速赢

## 什么是发电机功能？我应该在乎吗？

![](img/1ac9ae6927093fcd39829172b2bed7d4.png)

Photo by [Greg Willson](https://unsplash.com/@gregwillson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

是否应该关心生成器函数是有争议的。在我的第一份开发工作中，我一次也没有使用过它们，我的同事也没有使用过。我在那里待了将近三年。

然而，我确实认为生成器函数值得理解，原因有二:

1.  避免在技术面试中被暗算。
2.  作为开发人员，不断学习应该是你的目标之一。

老实说，第一个原因是最初迫使我深入挖掘的原因。但是我很高兴我这么做了，因为我发现这很有趣。幸运的是，我现在在一个使用生成器函数的地方工作，旁边是一个名为 [redux-saga](https://redux-saga.js.org/) 的库。所以它实际上让我受益匪浅！

那么什么是生成器函数呢？为了回答这个问题，我首先想谈谈:

# 迭代器和迭代器，天啊。

iterable 对于任何 JavaScript 对象来说都是一个有趣的词，它为自己定义了在被循环(迭代)时的行为。

MDN 是这样说的:

> 如果一个对象定义了它的迭代行为，比如什么值在一个`[for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)`结构中循环，那么它就是**可迭代的**。一些内置类型，如`[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)`或`[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)`，有默认的迭代行为，而其他类型(如`[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)`)没有。

那么我如何创建自己的可迭代对象呢？为此，我需要实现 [**可迭代协议**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol) 。

iterable protocol (protocol 只是一个时髦的词，表示一种约定好的做事方式)只是要求您向自定义对象添加一个名为`Symbol.iterator`的属性。就是这样。

示例:

你可能会问，`Symbol.iterator`的值需要是多少？

`Symbol.iterator`的值需要实现另一个协议(🤦‍♂️)，称为 [**的迭代器协议**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol) 。

根据 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators#iterators) :

> 具体来说，迭代器是通过使用一个返回具有两个属性的对象的`next()`方法来实现[迭代器协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol)的任何对象:
> 
> `value`
> 
> 迭代序列中的下一个值。
> 
> `done`
> 
> 如果序列中的最后一个值已经被消耗，这就是`true`。如果`value`出现在`done`旁边，它就是迭代器的返回值。

让我给你一个图像。

对于下一个例子，让我们假设我已经提前创建了一个名为`generateMonster`的函数。每调用一次，就从零开始吐出一个不同程序生成的怪物。太棒了。

让我们现在也假设`generateMonster`是同步的。

示例:

一旦我们在自定义对象上定义了`Symbol.iterator`属性的值(使用迭代器协议)，我们就可以在`for...of`循环中使用它。上面代码的日志输出将是五个独特的怪物。

我们也可以手动迭代我们的`monsterList`，就像这样:

这为我们提供了一种按照自己的节奏逐步完成`monsterList`的方法。例如，我们可能想得到第一个怪物，但随后做一些其他的事情，然后再回来得到其他的怪物。迭代器协议允许我们这样做。

大获成功！我们现在已经创建了自己的定制对象，它符合 iterable 和 iterator 协议。

你知道还有什么符合 iterable 和 iterator 协议吗？

猜猜看。

# 发电机(最终)

现在我们有了一些背景知识，我们可以对什么是`Generator`有一个更清晰的理解，以及如何产生一个具有生成器功能的。

根据 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator) :

> `**Generator**`对象由[生成器函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)返回，它符合[可迭代协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol)和[迭代器协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol)。

简单地说，一个生成器函数给了我们一个`Generator`对象。该对象为我们处理**可迭代**和**迭代器**协议的实现。

使用一个生成器函数，下面是`monsterList`可能的样子:

上面的代码将会以与之前完全相同的方式运行。

以下是新的东西:

1.  `function*`。在`function`关键字旁边的星号就是指定它作为一个生成器函数的原因。
2.  `yield`。这个关键字相当于像我们前面做的那样返回一个带有`value`和`done`属性的对象，除了它简化了事情，只让您返回一个值。

在每个`yield`、**之后，发生器函数的迭代完成**。在这一点上，生成器功能实际上暂停了。

该函数将不会继续执行，直到下一次调用`.next()`，无论是手动完成还是在`for...of`循环中完成，就像我们前面的例子一样。

一旦函数中不再有`yield`，生成器函数将在终止前返回未定义，因此`.next()`的最终值将是`{value: undefined, done: true}`。

然而，上面的例子实际上只使用了`Generator`对象的一半值。我们目前只使用它来实现**迭代器**协议。我们仍然在实现我们自己的 **iterable** 协议，因为我们仍然在创建我们自己的自定义对象并为`Symbol.iterator`赋值。

如果我们想充分利用生成器函数，我们可以进一步简化代码:

现在我们充分利用了生成器函数语法。

# 异步发电机

现在让我们假设我的`generateMonster`函数返回一个`Promise`。幸运的是，我们仍然可以使用生成器函数异步获得一群怪物。

示例:

如果你想在一个异步的`for...of`循环中运行它:

新的东西是:

1.  我们在生成器函数`monsterList`之前使用了`async`关键字。
2.  我们在调用`generateMonster`之前使用`await`关键字。
3.  如果我们想使用`.next()`手动迭代我们的`Generator`，我们需要抓取`[Symbol.asyncIterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/asyncIterator)`而不是`Symbol.iterator`。
4.  如果我们想通过一个循环运行我们的`Generator`对象，我们使用`[for await...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of)`来完成。此外，我们必须在异步环境中包装循环。在这个例子中，我选择将它包装在一个异步的生命周期中。

# 有什么意义？

一个生成器函数可以让你遍历正在创建的值，这很酷。这可以带来更好的性能，因为它比在内存中保存一个巨大的数据结构，然后在其上循环更便宜。

为了形象化，想象你因为某种原因需要收集一英里长的绳子。

有了发电机功能，就像从魔术帽中拉出绳子一样。**你不需要整根绳子就可以开始收集**。你可以拉绳子，当你继续拉的时候，你可以神奇地得到更多的绳子。

相反，你旁边有一根很长的绳子，占据了空间，然后你抓住绳子的一端，开始从地板上收集它。

生成器函数的这种特性是它们能够很好地表达数据流的原因之一。当数据到达时，你可以增量地获取一些数据并对其进行处理。

# 离别的思绪

说到底，我不认为存在一个只有生成器函数才能解决的问题。但是编码的部分乐趣在于有这么多创造性的方法来解决同一个问题！知道了如何使用生成器函数，您的工具箱中就多了一个这样的工具。

而且，这表明你可能知道你在用 JavaScript 做什么。

感谢阅读！😄看看我在 quickwinswithcode.com 的一些早期文章。

*如果这篇文章中关于异步编程的任何内容令人困惑，请查看我的另一篇文章:*

[](https://codeburst.io/quick-wins-with-code-promises-in-javascript-4a5b09bd95c5) [## 代码速赢:JavaScript 中的承诺

### 快速浏览在 JavaScript 中处理异步代码。

codeburst.io](https://codeburst.io/quick-wins-with-code-promises-in-javascript-4a5b09bd95c5) 

**资源:**

*   [Redux-saga](https://redux-saga.js.org/)
*   [迭代协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)
*   [迭代器和生成器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)
*   [发电机](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)
*   [Symbol.asyncIterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/asyncIterator)
*   [用于](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of)的 wait……
*   [生活](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

*更多内容请看**[***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****