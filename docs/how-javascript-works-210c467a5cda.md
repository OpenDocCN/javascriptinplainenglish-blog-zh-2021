# JavaScript 如何工作

> 原文：<https://javascript.plainenglish.io/how-javascript-works-210c467a5cda?source=collection_archive---------5----------------------->

## 了解我，了解 JavaScript——哈哈！

![](img/20bceed6d5608be363e55488850489ed.png)

Photo by [Tachina Lee](https://unsplash.com/@chne_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们都听过爱因斯坦的老习语:“如果你不能简单地解释它，你就不能很好地理解它。”。我已经使用 JavaScript 几年了，当被问及什么是 JavaScript 以及它是如何工作的时候？我的回答会是……嗯……混乱，坦白说是垃圾。

嗯，这是一种电脑编程语言，嗯，它允许你建立网站和应用程序。嗯，它在浏览器中工作，单线程，嗯，同步和异步，嗯，更多的行话…就这样了！

如果你和我在同一条船上，这篇文章是给你的。或者至少我希望如此。因为我发现，完美的答案是，**一个 JavaScript 程序和我们一样工作**。

如果你想知道更多，试试我，继续读下去。我希望这篇文章能给你提供一个有用的比喻来更好地理解 JavaScript 是如何工作的。

顺便说一下——这篇文章充满了 ABBA 歌曲的参考，我只能提前道歉。

# 最要紧的东西

![](img/9d49189fe93bdf9f6129722229a322f3.png)

Photo by [bruce mars](https://unsplash.com/@brucemars?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当你早上醒来时，你如何决定该做什么？你有一个现成的清单吗？或者你对周围的世界有什么反应？答案可能是两者兼而有之。

早上，我们的首要任务是对醒来的反应。清洁牙齿、洗澡和吃早餐都是我们在醒来时就已经设定好要做的事情。

这样，我们所做的大部分事情就是对‘T2’事件做出反应。JavaScript 程序也是如此。当 x 发生时，我们做 y。事件触发动作。

所有的 JavaScript 代码都是由一个事件触发的，尽管这并不总是显式的。当任务没有分配给事件时，它们会在 JavaScript 文件首次加载时运行。这相当于我们早上醒来，做好准备一天所需的任务。

对事件的反应通常被称为**异步**编程或非阻塞。毕竟，知道我们明天早上会刷牙并不妨碍我们现在做点什么。

那么，当事件发生时，JavaScript 是如何完成这些任务的呢？

# 我知道，我知道，我知道，我知道，我知道

![](img/4caffcceaf1ce8277ae10837fdf7816c.png)

Photo by [Eden Constantino](https://unsplash.com/@edenconstantin0?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有传言说，男人不能一心多用。尽管这可能是令人愤慨和诽谤性的，但像男人一样，JavaScript 程序一次只能做一件事。这样一来，人们就可以说是一心一意……而 JavaScript 据说是**单线程**。

与我们大多数人不同的是，JavaScript 程序在焦点上是坚定不移的。在这项任务完成之前，它不会进入新的领域。在这种方式下，JavaScript 被称为**同步**和阻塞。

使用之前的唤醒任务，我们不能在吃早餐的同时清洁牙齿。所以一项任务需要在另一项之前完成。

在 JavaScript 程序中，任务运行的顺序由**任务队列**管理。这个队列就像你的待办事项列表。像任何有序队列一样，第一个进来的任务是第一个出去的任务。因此，第一个任务将运行，然后下一个，以此类推。

每个单独任务的执行由**调用栈**管理。就像一堆文件一样，调用堆栈是先进后出的。为什么使用堆栈而不是队列？因为任务通常包含需要完成才能完成第一个任务的子任务。

要清洁牙齿，你需要把牙膏放在牙刷上，刷牙，然后吐出牙膏。只有实现了这些子任务，你才能完成刷牙这个第一任务。

一旦调用堆栈上的所有任务都已完成并且堆栈为空，任务队列就能够传递到下一个任务。

当你一次只能做一件事时，任务的大小和时间决定了你能做什么。JavaScript 程序也是如此。

(注意:从技术上来说，一个 JavaScript 程序可以使用 Web Workers 同时处理多个任务。这就相当于用一个助手来帮你。)

# 继续前进

![](img/4fc334a328579907a9a289ec80bb3be6.png)

Photo by [Ocean Ng](https://unsplash.com/@oceanng?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

随着分针滴答作响，我们完成了更多的工作。现在想象一下，分针绕着时钟越来越快，直到它变得模糊不清。您可以想象管理 JavaScript 的超级快时钟，称为**事件循环**。

这个时钟很特别，不仅仅是因为它超级快，还因为每当任务执行时它都会暂停。在大多数情况下，我们不会注意到任何冻结行为，因为 JavaScript 代码运行得非常快。如果我们这样做了，这是一个好迹象，表明我们有一个性能问题要解决。如果你的电脑完全死机，这意味着一个任务永远在运行，陷入了一个永无止境的循环。

一旦任务完成，这个特殊的时钟将重新启动，并评估任何新发生的事件。如果这些事件有关联的任务，它们将被添加到您的任务队列中。如此循环往复。因此得名事件循环。

当然，拥有一个单一的任务队列是有问题的。一些事件触发比其他事件更紧急的任务。幸运的是 JavaScript 可以做到这一点。

# 请你…优先考虑

![](img/8e5b01e9364387a30af6173f1df35d5c.png)

Photo by [Andrew Petrov](https://unsplash.com/@andrewwwpetrov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们的优先事项往往与我们对自己和他人的承诺联系在一起。通常情况下，它们都与截止日期相关联！当我们想强调我们对某件事的承诺是优先时，我们承诺。

承诺也存在于 JavaScript 中，反映了我们所做的承诺。我承诺做 y，如果 y 发生了做 x，如果 y 没有实现做 z。

当您在 JavaScript 程序中做出承诺时，该承诺的实现或失败会增加一个优先任务。这个优先级任务被称为**微任务**，并且有自己的任务队列。该队列使任务能够在标准任务队列中的下一个任务之前进行队列跳转和运行。就像我们的优先任务一样，只要我们有优先任务要做，我们就不能转移到其他任务上。每当现有的调用堆栈为空时，微任务就会运行。

如果你还在这里，你可能会问“这一切到底是怎么可能的？”就像我们一样，大脑让这一切成为可能。

# 了解我，了解你

![](img/9b6adeca50e6700647cc60cc2dccdcc4.png)

Photo by [Robina Weermeijer](https://unsplash.com/@averey?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们是谁，我们的记忆，我们的逻辑和我们的信仰都存在于我们的大脑中。我们的大脑通过解释来自神经元的电子/化学脉冲来理解我们周围的世界，神经元从我们的感官接收信息。

在 JavaScript 程序中，JavaScript 实现了与这些神经元相同的功能。来回传递信息。JavaScript 只是 JavaScript 大脑使用的一种语言。

“T2”浏览器“T3”(如 chrome、firefox)或包含“T6”JavaScript 引擎“T7”(node . js)的“T4”服务器“T5”就是大脑。浏览器中的 JavaScript 引擎通过一个称为编译的过程来解释 JavaScript。**编译**允许浏览器/服务器理解 JavaScript 并采取行动。该动作可以是将数据和动作分配给存储器或者执行任务。

就像我们有与外界互动的模式，比如口语。浏览器和服务器能够使用 API 与外部世界进行交互。API 只是一种共享语言，各方可以通过它进行交互。因此，浏览器能够与你的计算机或世界另一端的数据库进行交互，以建立网站。

浏览器(或服务器)使 JavaScript 程序成为可能。调用栈、todo 队列、事件循环、变量和回调都由这个 JavaScript 大脑管理。javascript 程序员只是简单地为大脑构建消息和模式来解释和采取行动。

# 结果

所以总结一下:

*   像我们一样，大多数任务来自对事件的反应。在 JavaScript 中，对事件的反应是异步和非阻塞的。
*   和我们一样，一个 JavaScript 程序使用“待办事项”列表来管理任务，一个是标准的“待办事项”列表(任务队列)，一个是优先级任务队列(微任务)。当某些事件发生时，任务被添加到这些队列中。
*   像我们(或男人)一样，JavaScript 程序一次专注于一件事(单线程)，尽管它可以使用助手(web workers)来执行并发任务。
*   不像我们，JavaScript 程序是坚定不移的，它不会放弃一项任务直到完成。通过这种方式，JavaScript 是同步和阻塞的。当调用堆栈为空时，任务完成。
*   像我们一样，时钟控制着一个 JavaScript 程序可以完成多少任务。JavaScript 时钟，即事件循环，不同于我们的时钟，因为它在每次执行任务时都会冻结。任务完成后，事件循环将检查发生了什么事件，并相应地将任务添加到任务队列中。
*   像我们一样，JavaScript 程序使用一种语言向大脑传递数据，从大脑传递数据，并在大脑内部传递数据。虽然我们有神经元，但是 JavaScript 程序使用 JavaScript。
*   像我们一样，大脑使这一切成为可能。它解释信息，管理内存，并使用多种共享语言中的一种与我们的环境进行交流。在 JavaScript 程序中，这个大脑是一个包含 JavaScript 引擎的浏览器(或服务器)。

# 继续继续

为了巩固你的知识，菲利普·罗伯特([https://www.youtube.com/watch?v=8aGhZQkoFbQ](https://www.youtube.com/watch?v=8aGhZQkoFbQ))和杰克·阿奇博尔德([https://www.youtube.com/watch?v=cCOL7MC4Pl0](https://www.youtube.com/watch?v=cCOL7MC4Pl0))的以下视频将是无价的。因此，与其在你的任务队列中增加一项任务，不如做出承诺，然后尽快抽出时间去关注它们。

如果你惊呼“SOS ”,因为 JavaScript 的工作方式与我们完全不同。你完全正确。

正如我们的工作方式更加复杂一样，JavaScript 也是如此。尽管如此，我希望这个简化的模型能够帮助您记住并解释 JavaScript 是如何工作的。

“这么久！”

## **感谢**

写这篇文章是为了帮助我更好地理解 JavaScript 是如何工作的，在我个人的探索中，我发现了许多非常有价值的资料。所以，我要感谢菲利普·罗伯茨的 YouTube 视频，杰克·阿奇博尔德的 YouTube 解释，凯尔·辛普森的《你不知道的 JavaScript》系列，迪米特里·格拉兹科夫的娱乐博客和无数其他来源。