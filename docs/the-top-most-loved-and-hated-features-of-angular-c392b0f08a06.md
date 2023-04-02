# 人们喜欢(和讨厌)棱角分明的什么

> 原文：<https://javascript.plainenglish.io/the-top-most-loved-and-hated-features-of-angular-c392b0f08a06?source=collection_archive---------4----------------------->

## Angular 最受欢迎和最受讨厌的特性:一个社区分享它对这个问题的想法

![](img/1bc59115a4ec673c08b81b4c2a318022.png)

自 2014 年问世以来， [Angular](https://angular.io) 一直是一个有争议的框架。推开它的前身 [AngularJS](https://angularjs.org) ，就像一个没有悔意的恶霸，它的存在被预言为优越，社区被迫接受它，不管我们喜欢与否。谷歌团队认为解决 AngularJS 的核心问题是必不可少的，但我们当时并不知道这需要完全重写我们心爱的 1.0 版本。我们会喜欢 Angular 的新功能还是完全讨厌它们？这仍有待观察，也是我思考的一个问题，即使在框架已经成熟的今天。

# 背景

当新的和改进的 Angular 看起来像什么的问题隐约出现时，当正式的 [2.0 版本](https://en.wikipedia.org/wiki/Angular_(web_framework)#Version_2)发布时，我屏住了呼吸。对该框架的接受程度不一，AngularJS 社区也存在分歧。一些人继续使用不太理想的框架，希望继续得到支持，而另一些人则不情愿地过渡到 Angular。有些人甚至完全跳槽，转投最近的竞争对手 React。

React 总是把自己表现为一个库，这是应该的，而不是像 Angular 这样的完整框架。然而，两者之间的争论是众所周知的，比较似乎永无止境。每年都有无数的文章讨论哪个更好，结果总是一样的。**看情况**。

Angular 被吹捧为更适合更复杂的企业应用程序，而 React 则被认为非常适合需要最少启动时间的较小应用程序。它们非常不同，但是它们的目的是一样的:创建 web 应用程序。随着 web 应用程序的不断需求，Google 框架和脸书图书馆通常是标准化解决方案的默认选择。Vue.js、Svelte 和其他各种公司偶尔会被提及，但没有一家是成熟的或有相同类型的公司支持。

Angular 2.0 发布已经快 5 年了，关于开发人员喜欢或者更讨厌这个框架的什么，仍然存在激烈的争论。下面记录的是根据一直受欢迎的社交新闻平台 [Reddit](https://www.reddit.com) 中的 [Angular 社区](https://www.reddit.com/r/Angular2)的好评和批评的功能列表。这些开发人员热情、敏锐，不容小觑。如果你想参加，请带上你的 A-game。

# 最受喜爱

讨论[线程](https://www.reddit.com/r/Angular2/comments/o6c6j3/what_is_your_favorite_thing_about_angular)中最喜欢的 Angular 特性与最不喜欢的特性相比显得苍白无力。不管怎样，仍然有相当数量的功能被列为受欢迎的。以下是获得 **10 张以上**选票的候选人，按降序排列:

*   以打字打的文件
*   RxJS
*   固执己见的结构
*   硬币指示器 （coin-levelindicator 的缩写）命令行界面（Command Line Interface for batch scripting）
*   高薪工作——很确定这是个玩笑，但却是真的
*   表格*
*   反应形式*

★最热门的评论是 **eyeslandic_1981** 分享的前四个心爱的选项。

# 最讨厌

最讨厌的特性的[线程](https://www.reddit.com/r/Angular2/comments/o7n3vu/what_is_your_least_favorite_thing_about_angular)比崇拜的线程**多 5 倍**。用户自由分享他们对流行的谷歌框架的不满，并在近 200 条评论中进行了大量投票。以下是不喜欢类别中按降序排列的拥有 **10 张以上选票**的功能。

*   第三方 npm 包缺乏类型脚本支持
*   由于缺乏经验的开发人员缺乏理解，RxJS 被误用
*   更改检测需要进一步配置
*   糟糕的文档
*   模板中不鼓励的功能和使用时的不良性能
*   单个组件不支持多个模板**
*   NgModules
*   反应形式*
*   不支持同一元素中的 ngIf 和 ngFor
*   大包装尺寸
*   错误的第三方软件包支持
*   mat-对话框

★置顶评论去了 **rattkinoid** 分享了最讨厌的缺少类型脚本支持的第三方 npm 包选项。

**用户又爱又恨
**通过一个提示/技巧解决*

# 争议最多的

正如单个星号所指出的，用户列出的一些喜欢或讨厌的原因引发了额外的辩论。以下是引发更多枝节话题的几个。

*   反应形式
*   HTTP 观察点
*   RxJS
*   NgModules

其中大部分是由于它们的复杂性和难以操作，但是一些用户在通过最初的学习曲线后表现出了欣赏的迹象。

由于 HTTP observables 返回 observables 而不是承诺的默认行为，它受到了大量的讨论和激烈的争论。支持承诺的用户认为这是“发射一次”行为更合理的选择。我发现自己在这个问题上摇摆不定，但更多的是由于确定哪些方法表现出这种单一发出行为的不直观性(例如 HttpClient.get，MatDialog.afterClosed)。如果这一点变得更加明显，可能通过智能感知，它可以帮助防止开发人员不知道该行为的任何多余的取消订阅。

# 提示和技巧

讨论的一个偶然副作用是启发用户一些技巧和窍门。这些帮助平息了 Angular 的一些抱怨。这些是获得高票数的。

## **1)** 不能对同一组件使用不同的模板

**提示/技巧**:在 templateUrl 中使用 if/else 逻辑。

```
templateUrl: environment.mobile 
             ? ‘foo-bar.component.mobile.html’ 
             : ‘foo-bar.component.html’
```

在我写这篇文章的时候，T4 获得了 70 票，一个大声喊出来的人来到了 kqadem 分享这个技巧。

## 2)需要使用 ngOnChanges 对输入变化做出反应

**提示/技巧**:改为在输入上使用 set 方法。

这个建议归功于 **pauly-815** 。这就是我，所以说多了感觉怪怪的。很高兴投稿。

# 结论

讨论主题的目的是激发对话，并发现 Angular 当前的利弊。今天，有几个竞争选项，包括 React(带附加组件)、Vue.js、Svelte、Vanilla JS(针对讨厌框架的人)以及许多其他选项。即便如此，Angular 开发人员仍然坚持选择留在框架中，至少现在是这样。

考虑到框架和库在 JavaScript 世界中来来去去的速度，Angular 的长寿潜力可能会因为围绕它的不满而受到质疑。令人欣慰的是，尽管提到了许多问题，但社区似乎很有弹性，能够忍受框架的不完美。谁能说五年后 Angular 是否还会存在？嗯，也许谷歌可以，但在那之前，按下 Angular devs。我们的社区生机勃勃。

**如果你喜欢这个，你可能也会喜欢:**

[](/how-to-find-out-if-someone-really-knows-angular-4bd335f8d180) [## 如何发现某人是否真的了解 Angular

### 5 个高级面试问题

javascript.plainenglish.io](/how-to-find-out-if-someone-really-knows-angular-4bd335f8d180) 

*更多内容看* [***说白了. io***](http://plainenglish.io/)