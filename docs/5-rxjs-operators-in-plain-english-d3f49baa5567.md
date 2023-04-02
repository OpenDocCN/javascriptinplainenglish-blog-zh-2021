# 5 个 RxJS 操作员用简单的英语

> 原文：<https://javascript.plainenglish.io/5-rxjs-operators-in-plain-english-d3f49baa5567?source=collection_archive---------5----------------------->

## 这是一个关于开发者最容易误解的主题的真实世界。

![](img/d9d43d30d989b11879af73d33e8610cd.png)

Photo by [Joshua Aragon](https://unsplash.com/@goshua13?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

你学的越多，知道的越少。这个古老的格言在很多情况下都是正确的，尤其是在编码方面。更重要的是，我认为当你，作为一个开发者，第一次遇到可观测量时，你就能发现它的本质。

与我们钟爱的承诺或回调相比，可观测量是一种完全不同的处理异步操作的方式。因此，他们的内在工作起初可能看起来模糊不清。

在我看来，了解一个未知事物最好的方法是将它与一个众所周知的事物进行比较。因此，为了让观察不那么令人畏惧，我将把五个常见的操作者与一个大家都知道的主题进行比较:高速公路交通。

## 可观察到的流量

为什么可观测量首先可以与流量相提并论？可观察性是处理异步操作的一种独特方式。当操作不阻止后续代码的执行时，它们是异步的。最常见的例子是对服务器的请求，它在处理响应时不会阻止代码的执行。

通常我们使用承诺来处理异步代码。通过将服务器请求包装在承诺中，我们可以轻松地在完成或失败时执行代码。

在下面的例子中，[获取 API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) 返回一个承诺。示例端点一应答，响应就被记录到控制台。

承诺的结果可以比作空旷高速公路上的*汽车*。一旦它完成了，孤独的车就驶向它的目的地，没有办法让它停下来。

可观测量在几个重要方面有所不同。

*   通过[订阅和取消订阅](https://rxjs.dev/guide/subscription)，您可以决定何时开始和停止监听(异步)操作的结果。换句话说，你决定高速公路何时开放或关闭。
*   承诺总是有回报的。按照设计，高速公路上只有一辆车。相比之下，可观测量返回一个流——一个数据序列。这意味着，只要你订阅了一个可观测的，新的汽车可以沿着公路行驶。
*   承诺只能处理异步操作。然而，observables 也可以处理同步操作。所以，在应许之地，我们将永远不得不等待汽车的到来，但是有了 observables，汽车也可以立即到达高速公路。

在下面的代码片段中，突出显示了一些关键差异。多辆车的*流*有一个*订阅*，同步交付*。*

## RxJS 运算符作为流量

简单的观察本身就很强大，但是与[操作符](https://www.learnrxjs.io/learn-rxjs/operators)结合起来，它们真的会大放异彩。运算符是将普通值或可观察值作为输入，并返回新的可观察值的函数。这允许您创建或修改可观察对象，直到它们以适合您需要的方式发出数据。

操作员在处理可观测量时提供的灵活性几乎是不可或缺的。但乍一看，它们似乎有点令人生畏。一个可观察对象本身可能很难理解，更不用说通过函数来改变它们的内部运作了。为了帮助你，我将把五个非常常见的现象带入现实世界，将它们与高速公路上的交通进行比较。

## [1。](https://www.learnrxjs.io/learn-rxjs/operators/creation/of)的

“Of”是创建可观测量最常用的运算符之一。由于我们在流量模拟中没有任何可观察的数据，我们可以用`of`创建一个。

`Of`将其给定的自变量转换成一个可观察量，该可观察量按照给定的顺序发出其值，并在所有值发出后完成。在下面的例子中，向操作员提供了三辆汽车。在订阅时，值是一个接一个发出的。好消息，路上堵车了！

## [2。组合测试](https://rxjs.dev/api/index/function/combineLatest)

根据[文档](https://rxjs.dev/api/index/function/combineLatest)，这是操作者所做的:“组合多个可观察值来创建一个可观察值，其值是根据每个输入可观察值的最新值计算的。”

那么，这与日常交通相比如何呢？假设我们有一个可观测的`cars`,令人惊讶地包含了汽车。此外，还有一个可观测的`speed`来监测`cars`经过的速度。

我们想知道哪些车超速了。单独的可观察值缺少信息，但是将它们的值与`combineLatest`结合，让我们打印两个罚款！

## [3。地图](https://www.learnrxjs.io/learn-rxjs/operators/transformation/map)

在上面的例子中，我悄悄地添加了另一个操作符。我们使用`combineLatest`来组合`cars`和`speed`可观察到的数据，但是为了实际发现汽车是否超速，使用了`map`。

`Map`是用于转换可观察值的最常见运算符。您可以通过地图运行源可观察值，以任何适合您需求的方式修改它们。在我们的示例中，我们将普通汽车和速度修改为关于法定速度限制的消息。

## [4。过滤器](https://www.learnrxjs.io/learn-rxjs/operators/filtering/filter)

我们现在知道高速公路上哪辆车超速了。但是我们也收到关于遵守速度限制的汽车的信息。这似乎有点多余。要获得关于实际违规者的信息，我们可以使用`filter`。

这个操作符，顾名思义，过滤掉任何不符合给定标准的可观察值。我们现在从游戏规则的结果中忽略每辆车！

## [5。乘坐](https://www.learnrxjs.io/learn-rxjs/operators/filtering/take)

现在我们应用了一个`filter,`，我们只收到超速车辆的通知。但是，假设有一名警官只需要开出一张罚单就可以完成他一天的定额。他可以使用`take`来实现这一点。Take 限制发射值的数量。因此，使用`take(1)`，警官将只得到第一辆超速的汽车的通知。

就是这样！我们已经看到了使用承诺的流量是如何不同于可观察的流量的。使用观察装置控制道路何时开放和关闭，即订阅和取消订阅。此外，道路可由多辆汽车通行，即*数据流*。

此外，道路上的交通处理方式可以根据您的喜好使用 RxJS 操作符进行修改。我们行动的结果？一辆超速行驶的福特车被罚款。

喜欢这篇文章吗？**关注我**敬请关注！

**资源**

*   RxJS 文件:[https://rxjs.dev/](https://rxjs.dev/)
*   获取 API:[https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
*   RxJS 操作员:[https://www.learnrxjs.io/learn-rxjs/operators](https://www.learnrxjs.io/learn-rxjs/operators)
*   组合最新:[https://www . learn rxjs . io/learn-rxjs/operators/combine/combine test](https://www.learnrxjs.io/learn-rxjs/operators/combination/combinelatest)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***