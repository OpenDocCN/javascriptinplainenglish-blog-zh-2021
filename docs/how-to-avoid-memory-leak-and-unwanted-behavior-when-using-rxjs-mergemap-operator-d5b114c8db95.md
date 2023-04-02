# 使用 RxJS mergeMap 时避免内存泄漏和不必要的行为

> 原文：<https://javascript.plainenglish.io/how-to-avoid-memory-leak-and-unwanted-behavior-when-using-rxjs-mergemap-operator-d5b114c8db95?source=collection_archive---------11----------------------->

![](img/06ed94f4ddb9445d5c6b5291896202c4.png)

Photo by [Tianyi Ma](https://unsplash.com/@tma?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 语境

我**爱** rxjs…当我刚开始使用 Angular 时，我尽可能地避免使用它(主要是因为我真的很难理解它)，但现在，我无法想象没有它会做什么项目。

然而，与每一种技术或框架一样，误用它可能会导致令人讨厌的后果，比如内存泄漏、应用程序变慢或者只是不良行为。

在我看来,“rxjs”中最难的概念在于高阶可观测量。对于那些不知道它是什么的人来说，它只是一个返回另一个的可观测值。例如“合并映射”、“切换映射”、“穷尽映射”等

我读过一些(写得很好的)关于上述操作符之间的区别的文章，我认为我很好地理解了这种区别，但是今天，我艰难地发现我并不理解。这篇文章将简单地强调我落入的陷阱，让你不要做同样的事情。

# 让我们来玩吧！

与其解释我的误解，不如我们来玩一个小小的(愚蠢的)游戏。假设你有以下角度分量(不知道角度也行):

这里的想法是，我们有某种简单地保存一个数字的存储。我们还创建了一个名为“osb$”的可观察对象，它将调用商店上的“mergeMap”来返回一个每 X 秒触发一次的定时可观察对象，其中 X 是商店的值+ 1。因此，如果我们订阅它，因为这是一个默认值为“0”的“行为主体”，我们将订阅一个每 1 秒钟发出一个值的“计时器”可观察值((0+1)* 1000 毫秒)。方法“increment”简单地发出存储的增量值。

模板非常简单:

我们只是使用“异步”管道来订阅“obs$”可观察值并显示发出的值。所以现在，游戏是猜测如果我**不**点击按钮会显示什么。

好的，这并不复杂……正如预期的那样，observable 每秒发出一次并递增计数器(因为“timer”操作符发出一个递增的值)。

现在，如果我在计数器达到 5 时单击“Increment”按钮会发生什么(注意，无论当前值是多少，它都会这样做)。

如果你预料到了这种行为，那么恭喜你，你正确理解了“mergeMap”的用法。然而，如果像我一样，你只是希望看到计数器回到 0，然后每 2 秒增加一次，让我来启发你:-)

我以前对“mergeMap”的理解是，它将按照内部订阅出现的顺序来处理内部订阅。这并不是完全错误的，但是我忽略的部分实际上是“mergeMap”不会取消之前创建的内部订阅，这就是为什么可以观察到这种行为。让我们来看看发生了什么:

*   我们首先通过将“商店”观察值映射到计时器观察值来创建一个内部观察值。
*   我们使用角“异步”管道订阅这个内部可观察对象，这就是为什么我们看到计数器递增的原因。
*   当计数器达到 5 时，我们点击“增量”按钮。
*   “store”可观测值发出一个增量值(所以 1 是因为 store 的初始值是 0)。
*   此时,“obs$”可观察对象将接收新值(1 ),并使用每 2 秒发射一次的“计时器”创建另一个内部可观察对象。
*   然而，这是重要的部分，**它不会取消订阅之前创建的内部订阅(因此，在第一次订阅时从“异步”管道创建的每秒发出一次的计时器可观察到的订阅)**。

这实际上意味着在点击按钮后，“mergeMap”开始管理两个内部订阅，而不是一个:

*   每秒发出一个值的
*   另一个每 2 秒发出一个值

所以你在上面的图片中看到的实际上是这两种内在的可观察性在竞争。

# 怎么修？

## 并行论点

“mergeMap”接受第二个参数(除了返回内部可观察对象的函数之外),该参数定义了“mergeMap”可以同时处理的并发内部订阅的数量。所以你可以像这样避免这种行为:

对于这个代码变体，单击按钮不会有任何影响。事实上，由于您允许“mergeMap”一次只能管理一个内部订阅，因此它不会订阅第二个“timer”内部可观察对象，因为它已经处理了一个内部订阅(当“async”管道订阅“obs$”时最初创建的订阅)。

# 开关图

尽管并发参数是一个不错的解决方案，但大多数时候并不是你想要的。事实上，更好的解决方案是在点击按钮时取消之前的内部订阅。

那么你就是一个路克西男孩/女孩，因为这正是“开关地图”的用途。事实上,“mergeMap”和“switchMap”的区别在于,“switchMap”永远不会管理一个以上的内部订阅。当在外部可观察对象(在“商店”的情况下)上发出新的值时，“switchMap”从先前创建的内部订阅中取消订阅。所以让我们这样编辑我们的代码:

这将导致:

让我们再来看看发生了什么:

*   我们首先通过将“商店”观察值映射到计时器观察值来创建一个内部观察值。
*   我们使用角“异步”管道订阅这个内部可观察对象，这就是为什么我们看到计数器递增的原因。
*   当计数器达到 5 时，我们点击“增量”按钮
*   “存储”可观测值发出一个增量值(所以 1 是因为存储的初始值是 0)
*   此时,“obs$”可观测值接收到新值(1)。
*   由于已经创建了另一个内部订阅，**“switch map”将其取消订阅。**
*   最后，“switchMap”订阅了一个新的内部可观察对象，即每两秒钟发出一次的“计时器”。

这样，点击按钮后，计数器重置为 0，每 2 秒递增一次

# 结论

“mergeMap”是一个非常方便和强大的操作符，但是理解它可以维护多个内部订阅以及它可能导致一些内存泄漏(取决于用例)是非常重要的。大多数时候，为了一次只维护一个订阅，您真正想使用的操作符是“switchMap”。

> 如果你喜欢这篇文章，想要支持我，请不要犹豫，鼓掌或者请我喝杯咖啡:-)好吗

[![](img/6d60b235fcc46a4bd696b90e886419ee.png)](https://www.buymeacoffee.com/ssougnez)