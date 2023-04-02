# RxJs 挑战:发现错误

> 原文：<https://javascript.plainenglish.io/rxjs-challenge-spot-the-mistake-fa4fbd163135?source=collection_archive---------2----------------------->

**我已经用 RxJs 流烧伤了自己(一点点),所以你不必这样做。欢迎来到 RxJs 上的这个简短的调试之旅，它触及了一些中级/高级流主题——无论您是否会看到错误的到来，这也是一个挑战。**

我们的团队在 Angular + Node.js 中工作。在适用的时候，我们使用适当的具有严重反应影响的 OO(RxJs)。我们是务实的程序员:快速完成工作，保持简短和可维护，我们不相信银弹:总是尝试使用最合适的解决方案。

我们在做游戏的后台逻辑。游戏可能会有一些机器人参与游戏。当游戏开始时(`start`事件)，我们将每隔 100 毫秒为机器人生成进度事件，直到`finish`事件。按照这些思路，实际的用例要复杂一些。

这里我将简化很多:主要代码在`ProgressGenerator`类中，只占其原始大小的一小部分。此外，在调试时，我在一个测试用例中工作，这不是特别方便，所以这里我们将有一个小的测试环境。

![](img/1e61ae1c710a26b0ad16fb818431a034.png)

# 1.初始方法

这是主要逻辑的第一个版本，这碰巧是我比较满意的第一个版本。很多东西都被省略了。

我创建了一些绿色的基本测试，然后我继续进行面向流的测试。([大理石检测](https://rxjs.dev/guide/testing/marble-testing)，真的很厉害！)而下一个测试就破了。

> **挑战:**试着找出上面代码中的错误！哪里会破？为什么呢？以及如何修复？

## 运行示例

我主要是在一个不太方便的测试用例中工作，所以对于本文，我创建了这个小的测试运行器。它发出一个`start`事件，然后在 500ms 内发出一个`finish` 事件；它再次等待 500 毫秒，最后执行拆卸。

我们预计在`start`和`finish`事件之间的每 100 毫秒`progress$`会触发一次。

省略了`loadProgressGenerator`。简而言之，它加载了存储库中提供的 5 个示例之一。在此阅读[完整源代码](https://github.com/igabesz/rxjs-challenge/blob/master/src/run-example.ts)。

## 第一次尝试的结果

剧透:不是我预想的那样。

```
Starting
p 0
p 1
p 2
p 3
Finished -- no "p" logs expected below this
p 4
p 5
p 6
p 7
p 8
Teardown
```

时间间隔应该在`Finished`日志之后停止——然而它没有。出事了。这意味着…调试时间！🎉

> **挑战**:如果你已经明白了一切，那么恭喜你！(很高兴是你。)如果没有，试着在笑点之前搞清楚发生了什么。

![](img/2c2da86ac75a286be91426be8391ce16.png)

Best friend during debugging and showering.

# 2.排除故障

我没有立即意识到这个错误，所以我添加了 2 个调试订阅和 2 个 *tap* 操作符，来看看到底发生了什么:

以下是包含调试消息的日志:

```
Starting
p 0
p 1
p 2
p 3
Finished -- no "p" logs expected below this
startEnded 1
p 4
p 5
p 6
p 7
p 8
Teardown
destroyed!
```

看起来`startEnded 1`被正确地发射了，然而`startEnded 2`和`startEnded TAP`却没有。这就是为什么在`finish`事件上没有完成间隔的原因。

这是相同的可观测性，对吗？后面几种情况为什么不火？而为什么音程只有`destroyed$`流完成？(正如`*destroyed!*`消息告诉我们的)。

I didn’t like this.

首先，我试图排除所有我能想到的愚蠢错误。然后我开始责怪 RxJs，因为他们一定破坏了他们的测试工具或者其他什么……是的，当然，总是库的创建者有错。(是时候做一个快速的现实检查了。)

## RxJs 中间材料

让我们退后一点。是时候回到一些 RxJs 的基础知识了。

> **亮点 1** :一个可观察的只是一个蓝图，直到有人真正订阅。

是的，我们知道这一点，无论如何这都不是问题。我们继续吧。

默认情况下，每个 RxJs 订阅都构建自己的从流源到订阅的操作符管道。例如，如果可观察对象中有一个生成随机数的操作符，那么两个相同的订阅将会不同。这可能有点违背直觉，尤其是当你使用局部/成员变量时，比如这里的`this.startEnded$`流。

> **高亮 2** :默认情况下，每个订阅都建立自己的运营商管道。

您可以对此进行调整(`share`操作符即将推出),但这是经验法则。

让我们添加第三个反应智慧的金块。它是关于[热点观察](https://luukgruijs.medium.com/understanding-hot-vs-cold-observables-62d04cf92e03)。冷观察点发送相同的数据，而不管订阅时间。但是对于热点观察，如果你订阅得太晚，你很容易迟到。

> **亮点三**:订阅一个热门可观察到的东西取决于你订阅的时间。

你猜怎么着:T8 是一个热门的观测对象。

## 真正的原因

有了这个，你就有了把这些碎片拼在一起的一切。那么让我们继续讨论结论。或者说，笑点。

因此第一个调试订阅是在构造函数时创建的。它接收`start`和`finish`事件。`pairwise`第一次发射需要 2 个输入——注意，它在第一次输入时不发射任何东西。但在这种情况下，是可以的；这种订阅效果很好。

但是第二个订阅内置在`onStart`调用中——第三个订阅隐藏在`takeUntil(this.startEnded$)`操作符中。这两个都是在`start`事件之后构建的——它们只接收`finish`事件，并且它们管道中的`pairwise`操作符开始等待下一个事件。但这并没有发生。

所以 TL；DR:第二个订阅和`takeUntil(this.startEnded$)`错过了`start`事件，因此它们没有正确地检测到 Started 状态的结束。

# 固定的；不变的

最后，我明白了问题所在。由于第一个订阅工作正常，我们只需确保`startEnded$`上的每个订阅都使用相同的操作符管道，对吗？因此，解决方案就在操作员的手边:`share`。

最后，我得到了期待已久的结果:

```
Starting
p 0
p 1
p 2
p 3
Finished -- no "p" logs expected below this
startEnded 1
startEnded 2
startEnded TAP
Teardown
```

发出`finish`事件时，时间间隔正常停止。我们只需要清理调试的东西。

但我们仍然没有在这篇文章的结尾。前面肯定有剧情转折！

Beware! Plot twist ahead!

# 仍未修复

我删除了调试行，下面的输出再次出现:

```
Starting
p 0
p 1
p 2
p 3
Finished -- no "p" logs expected below this
p 4
p 5
p 6
p 7
p 8
Teardown
```

我不是很开心。

> **挑战**:为什么又破了？

之前的尝试之所以成功，只是因为构造函数中的调试订阅。没有订阅，就没有人及时创建管道，我们又回到了起点:订阅发生得太晚，它错过了`start`事件，因此它不会检测到`start → finish`转换。

## 糟糕的解决方案

那就让我们保留虚拟订阅吧，不是吗？添加一个适当的拆卸，(`takeUntil(this.destroyed$)`)，也可能是一行谦虚的评论。是的，我们可以这样做，悄悄地埋一颗快乐的小地雷，作为给未来的你的礼物。

A happy little landmine and Future You

务实与马虎相去甚远。务实的程序员非常讨厌糟糕的解决方案。"你爱公义，恨恶邪恶。"

所以还是找个合适的解决办法吧。

# 合适的解决方案

几分钟后，我得出了这个结论。它更短，使用的操作符更少，比原来的更简单。

最后，我看到了正确的输出:

```
Starting
p 0
p 1
p 2
p 3
Finished -- no "p" logs expected below this
Teardown
```

我很高兴。

Me rejoicing.

# 外卖食品

我又一次被溪流灼伤了。然而，这里我们有这篇文章；而这些记忆很难忘记。如果到目前为止您已经阅读了这篇文章，那么您可能已经为自己节省了几分钟的调试时间。如果你知道答案，恭喜你！请在评论中分享你的烧伤痕迹。当然是象征性的。

我最重要的几点:

*   溪流可能很脏。(尽管对于许多用例来说，它们仍然比命令式的混乱要好。)
*   默认情况下，每个订阅都会构建自己的操作员管道。这并不直观，尤其是当你将 Observable +管道保存在一个局部/成员变量中的时候。
*   当你动态订阅热门节目时要小心:确保你不会迟到。
*   不要为未来的你埋下快乐的小地雷。
*   也测试你的面向流的代码。使用[大理石测试](https://rxjs.dev/guide/testing/marble-testing)。

# 密码

强制 GitHub 链接来了:【https://github.com/igabesz/rxjs-challenge】
T3

*更多内容请看*[***plain English . io***](http://plainenglish.io/)