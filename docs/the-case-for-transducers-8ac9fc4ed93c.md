# 传感器的情况

> 原文：<https://javascript.plainenglish.io/the-case-for-transducers-8ac9fc4ed93c?source=collection_archive---------9----------------------->

## 人们常说函数式编程对内存使用有负面影响。传感器解决了这个问题。

![](img/ad26bf44b0c21e53cb12324fac4b34fd.png)

Photo by [Patrick Hendry](https://unsplash.com/@worldsbetweenlines?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

[map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 、 [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) 和 [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reducehttps://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 函数是 JavaScript 中众所周知的数组方法，广泛应用于函数式编程中。人们可以很容易地将它们链接起来，极大地增加了开发者的体验。

然而，每个操作都会创建一个**中间数组**。对于大多数不需要性能优化的应用程序来说，这不是问题，但对于大型阵列来说，这可能会成为一个严重的限制—想想数千个，或者更糟:数百万个值。

下面的例子说明了这一点，其中的附加类型将对本文接下来的部分有所帮助:

除了初始数组(`[0, 1, 2, 3]`)，在此过程中还创建了两个中间数组:`[1, 2, 3, 4]`和`[2, 4]`。

人们可能希望有一个*工具*，一个接一个地映射、过滤和求和初始数组**的每个值，比如:**

```
Initial array -> increment -> isEven -> sum
0             -> 1         ->        -> 0
1             -> 2         -> 2      -> 2
2             -> 3         ->        -> 2
3             -> 4         -> 4      -> 6
```

这个工具叫做**传感器**。为了精确起见，在这个例子中，传感器是用`filter`连接的`map`，并与`sum`减速器一起使用。稍后会详细介绍。

```
Initial array -> transducer -> sum
0             ->            -> 0
1             -> 2          -> 2
2             ->            -> 2
3             -> 4          -> 6
```

因此，换能器是一种功能，它将一个减速器转换成另一个减速器，打开了作曲的大门:

```
reducer: (accumulator, current) -> accumulator
transducer: reducer -> reducer
```

# 作为转换器映射和过滤，允许合成

我们的目标是组合`map`和`filter`操作，这需要将这些方法重写为转换器。让我们从`map`开始:

```
map: fn -> reducer -> reducer
```

`array.map(increment)`现在改写为`array.reduce(map(increment)(identity), [])`。这是很大的进步，听起来可能很复杂，所以让我们一步一步来:

*   `identity`:顾名思义，这是一个将一个数组的值累加到一个新数组中的 reducer。因此结果等于数组本身:`[0, 1, 2, 3].reduce(identity); // [0, 1, 2, 3]`
*   `map(increment)`是一个换能器。因此，它将一个减速器(`identity`)转换成一个新的减速器，同时应用`increment`功能。

光是这一点，就将是徒劳无益的。但是一旦以同样的方式准备好`filter`方法，这将是有意义的:

```
filter: fn -> reducer -> reducer
```

同样，`array.filter(isEven)`被重写为`array.reduce(filter(isEven)(identity), [])`，推理与前面相同。

这终于有意义了(希望如此)，因为我们现在能够将`map`和`filter`重写为转换器:

挺厉害的吧？

更强大的，我应该说，因为我们可以提供这种传感器与其他初始减速器:

`sum`:

`count`:

多棒的旅程啊。但还有更多！

# 传感器 x 项目

到目前为止，我们已经处理了长度有限的数组。如`[0, 1, 2, 3]`。如何处理“无限”的物体，比如可观察的或可重复的？

让我们考虑一个建立在自然数的生成器上的 iterable:

我们希望之前制造的传感器能和这个仪器一起使用。为此，我们需要一个`reduce`函数，由我们来定义这意味着什么。

简单来说，`Array.reduce`函数有如下签名(简化是因为在[规范](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)中，缩减器接受额外的参数、索引和数组本身):

```
Array<U>.reduce(reducer: ReducerFunction<U, R>, seed: R): R
```

受这个签名的启发，我们可以定义一个`reduce`函数，它不是返回一个原始值`R`，而是返回一个新的`Iterable<R>`。这对于无限的可迭代对象尤其有意义，因为对于无限的可迭代对象，reduce 操作应该考虑“到目前为止”产生的所有值，没有结束:

```
Iterable<U>.reduce(reducer: ReducerFunction<U, R>, seed: R): Iterable<R>
```

让我们称`IterableAndReducible`为`Iterable`，它也是一个`Reducible`(即公开一个`reduce`函数):

在原生`Iterable`型上的这项工作允许重复使用以前为阵列建造的减速器和传感器。太好了！这同样适用于 RxJS 中使用[扫描](https://rxjs.dev/api/operators/scan)方法的可观察值。要点是:只要数据结构公开了一个`reduce`函数，就可以使用减速器和转换器！

# 进一步阅读

*   [https://medium . com/JavaScript-scene/Transducers-efficient-data-processing-pipelines-in-JavaScript-7985330 Fe 73d](https://medium.com/javascript-scene/transducers-efficient-data-processing-pipelines-in-javascript-7985330fe73d)(Transducers，作者 Eric Elliott)
*   [https://medium . com/@ dt ipson/JavaScript-transducers-2-stateful-gate ful-1 FAA 1 b 01 AE 50](https://medium.com/@dtipson/javascript-transducers-2-stateful-gateful-1faa1b01ae50)(stateful transducers)
*   [https://github.com/mathieueveillard/transducers](https://github.com/mathieueveillard/transducers)

*更多内容请看**[***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报在这里***](http://newsletter.plainenglish.io/) *。****