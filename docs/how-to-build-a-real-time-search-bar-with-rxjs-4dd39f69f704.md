# 如何用 RxJS 构建实时搜索栏

> 原文：<https://javascript.plainenglish.io/how-to-build-a-real-time-search-bar-with-rxjs-4dd39f69f704?source=collection_archive---------5----------------------->

## 简单而有效 HTTP 呼叫的搜索引擎。

![](img/fbdd79501ce32ecdc0af0f84aac682ab.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](/s/photos/coding?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在本文中，我们将使用 [RxJS](https://rxjs-dev.firebaseapp.com/) 构建一个功能丰富的搜索栏，返回实时结果。如果你以前从未使用过 RxJS，这将是一个很好的介绍。您将看到 RxJS 库如何将一组相当复杂的需求转化为易于管理、易于阅读和理解的代码。

在现代应用程序中很常见的一种情况是，您必须构建一个搜索栏，允许用户搜索数据库的一部分，如果不是全部的话。

这就是我们所说的实时搜索栏或搜索引擎，每次搜索都需要向服务器发出请求并返回结果。众所周知，不断调用服务器对我们的应用程序性能不利。我们不知道用户会敲多少次键盘，向服务器发出不必要的请求。因此，像搜索栏这样常见的东西需要进行各种检查。

我们开始吧。

## 第一步:设置

对于这个例子，我只是使用了一个简单的 JavaScript 项目。

我们有两个对主元素的引用，一个用于搜索输入，另一个用于我们将要加载结果的 div 元素。

为了将我们的输入事件转化为可观察的序列，我们使用了`[fromEvent()](https://rxjs-dev.firebaseapp.com/api/index/function/fromEvent)` [操作符](https://rxjs-dev.firebaseapp.com/api/index/function/fromEvent)，并将我们的搜索输入作为目标。

## 第二步:最少搜索词

RxJS 的好处是我们可以将操作符链接在一起，就像我们可以将数组方法链接在一起一样。Observables 有一个叫做`[pipe()](https://rxjs-dev.firebaseapp.com/api/index/function/pipe)`的方法，它允许我们完成这个链，同时也易于阅读。

咱们顺水推舟用`[pluck](https://rxjs-dev.firebaseapp.com/api/operators/pluck)`[符](https://rxjs-dev.firebaseapp.com/api/operators/pluck)。这允许我们映射源值(输入的返回对象)并挑选出我们感兴趣的嵌套属性。正如您在这里看到的，我们正在获取嵌套在输入返回对象中的`target`对象中的`value`属性。

如果是一个需要搜索的大型数据库，那么下一个操作符非常重要，这一步是设置一个搜索项最小值。在这里，我将设置搜索词的最小值为 3 个字符，任何少于 3 个字符的内容都不会返回相关结果。我们将使用`[filter](https://rxjs-dev.firebaseapp.com/api/operators/filter)` [操作符](https://rxjs-dev.firebaseapp.com/api/operators/filter)来设置最小值，并将长度条件设置为大于 2。

## 第三步:去抖时间

让我们开始减轻服务器上的一些负载。为了确保请求只在 500 ms 的间隔内发送，我们可以使用`[debounceTime](https://rxjs-dev.firebaseapp.com/api/operators/debounceTime)` [操作符，](https://rxjs-dev.firebaseapp.com/api/operators/debounceTime)允许我们控制用户输入的速率。

## 第四步:区分时间变化

我们现在想要减少发送的 API 调用的数量。要做到这一点，我们希望应用程序忽略搜索词，如果自上次 API 调用以来没有任何变化。例如，用户可能键入“侏罗纪 P”，然后键入“侏罗纪”，然后再次键入“侏罗纪 P”。`[distinctUntilChange()](https://rxjs-dev.firebaseapp.com/api/operators/distinctUntilChanged)` [](https://rxjs-dev.firebaseapp.com/api/operators/distinctUntilChanged)将非常适合这种情况，它将记住之前通过流传递的数据，并且只有在不同的情况下才会继续流。

## 步骤 5:查询 API

现在我们需要添加查询 API 的代码。说到多个可观测流，`[switchMap](https://rxjs-dev.firebaseapp.com/api/operators/switchMap)`应该是你的首选。这被视为扁平化最安全的默认设置，它切换到一个新的可观察对象，同时取消之前的内部可观察对象，确保响应按顺序返回。

`[catchError()](https://rxjs-dev.firebaseapp.com/api/operators/catchError)` [操作符](https://rxjs-dev.firebaseapp.com/api/operators/catchError)将接收错误和捕捉到错误的可观察值(如果您希望重试)。这里，我们在由我们的`switchMap()`操作符返回的`ajax`可观察值上捕捉错误，因为我们不希望整个`input$`流在错误的情况下被完成。

在`catchError`中是你想要放置错误处理代码的地方。对于这个例子，我只是通过控制台记录错误，并返回一个空的可观察值，这允许流在不发出任何值的情况下完成。

## 步骤 6:激活并更新 DOM

最后一步是用订阅激活一切并更新 DOM。为了做到这一点，我们使用了`subscribe`操作符，使观察者能够看到被观察对象发出的数据事件。

## 第 7 步:可选附加组件。

值得一提的是，你应该始终记住，更新 DOM 可能是一项资源密集型操作，因此减少更新 DOM 的次数将对你的应用程序的性能产生积极的影响。

根据用户的情况和服务器结果的响应，添加一个`filter`或`distinctUntilChanged`操作符有助于减少 DOM 更新的次数。

类似这样的东西👇

这一次，我们**而不是**使用`distinctUntilChanged`操作符来查看整个数据是否已经更改(就像我们对输入值所做的那样)。比较整个响应将等于糟糕的性能和次优的用户体验，这将是一个非常繁重的操作，所以相反，我们比较响应的`key`属性。

在这两个值匹配的情况下(先前的响应和新的响应),数据被过滤掉，并且不沿着可观察的流传递。

## 结论

这就是了。有了这个解决方案，您就拥有了一个可靠的、功能丰富的实时搜索栏，旨在提供卓越的性能和卓越的用户体验。RxJS 操作符的易用性和将操作符链接在一起的能力意味着您可以轻松地在上面的解决方案中删除或添加操作符，以满足您的应用程序需求。

如果你是 RxJS 的新手，你可能会开始意识到这个库有多强大，它会给你的下一个项目带来多大的帮助。

## 源代码

💻[GitHub 上的示例代码](https://github.com/MeganRook18/real-time-search-engine)。
🏃‍♀️ [在 StackBlitz 上运行代码。](https://stackblitz.com/edit/real-time-search-bar-rxjs)

我用过的算子你都同意吗？您会添加更多还是使用不同的运算符？请随时留下你的想法。

快乐编码。