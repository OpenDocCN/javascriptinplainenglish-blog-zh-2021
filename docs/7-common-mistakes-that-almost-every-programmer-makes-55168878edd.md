# 几乎每个程序员都会犯的 7 个常见错误

> 原文：<https://javascript.plainenglish.io/7-common-mistakes-that-almost-every-programmer-makes-55168878edd?source=collection_archive---------15----------------------->

## 编程错误

## 我将告诉你几乎每个人在编程中都会犯的错误，以及为什么和如何避免它们。

![](img/3802cc78a2aa82a6600dea1812b84af1.png)

Photo by [NeONBRAND](https://unsplash.com/@neonbrand?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/mistakes?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我希望我以前读过这篇文章，因为相信我，它会节省你大量的时间和精力。你编程有多好并不重要。大多数程序员，甚至是专家，每天都在犯这些错误，却没有意识到。我试着在里面放了很多信息，我希望你会喜欢阅读它。

# 1.一解问题

就像你往一个方向想，解决方案却在完全不同的地方。例如，你正在解决几个关于 [Codewars](http://seekoapp.io/618544560f73250008ae53e2) 的问题，并且想要找到达到最终结果的最佳方式。通常的程序员会使用他已经知道的方法，例如，函数需要得到一个未排序的列表并返回排序的列表。对于这个问题，初学者将使用通常的线性排序算法，直到有一个包含 100 万个项目的列表(一些社交媒体或其他东西的数据库)才出现问题。如果我们以你的计算机一秒钟进行 1000 次运算的速度来计算，这意味着你需要大约 1000 秒来排序这个列表，而*认为*是*的一部分*，尤其是对于那些想在你的网站上获得一些价值的用户来说。

在这种情况下，有一些不同的方法来解决问题:您可以使用快速排序算法等。这只是一个例子，还有许多其他的情况，通过使用“列表生成器”来节省用户的时间，而不是你自己的时间(如果有毫秒的差异)，这将成倍地增加可读性，并且只需要几笔代码。

> "你需要了解解决问题的几种方法，才能正确地完成你的工作。"

# 2.从头开始构建一切

如果你认为你会坐下来，打开你的代码编辑器，然后开始编码，过一会儿，你会从头开始构建一个完整的应用程序，然后我可以告诉你，没有人这样做(这需要大量的时间和精力)。除了需要实践的初学者，比如你正在构建一个简单的项目，比如一个计算器，以了解它是如何工作的。因为对于您想要的几乎任何东西，最好使用别人已经编写好的代码。想写一个函数返回数字 X 的阶乘？幸运的是，在[栈溢出](https://stackoverflow.com/)上有大量的库、框架和代码，你可以很容易地复制和粘贴。**但是**不明白是什么就不要做，因为我前面说过，对于初学者来说，这是唯一的练习方法。

例如，如果你是一名 web 开发人员，那么对你来说最好的方法就是使用 [Boostrap](https://getbootstrap.com/) 或[materialiecss](https://materializecss.com/)，在那里你需要花几分钟弄清楚如何构建任何你想要的东西并开始做。

> “你不需要自己写代码。你需要找到已经发明的解决方案。”

# 3.独自工作

单打独斗是大多数程序员最愚蠢的一面。我的意思是，当你试图建立某种应用程序时，你试图自己做所有的事情，但你需要明白，没有人能知道所有的事情，如果你做设计，编写应用程序本身，营销，那么你可能会在这些步骤中的一个失败。最好创建一个团队，并赋予他们各自的角色。我已经在论坛和 Discord 服务器上找到了我的合作伙伴。我和我的团队目前正在寻找一个可以帮助我们建立新项目和方向的人，如果你想了解更多，那么就加我 Discord: MarkFusion#2903

## 优点:

1.  项目的每一步都将是高水平的。
2.  一切都会变得更快。
3.  提升你的技能(即使你没有和某人一起工作，如果你想创造伟大的东西，你将来肯定会的)。

## 缺点:

1.  你必须管理一切，分析下一步该做什么(如果你是领导)。
2.  利润将由所有员工分享。

> "与他人合作会提升你的技能，你的产品也会很棒."

# 4.没有正确使用 Git

如果你想在一家公司工作，或者只是为了向他人展示你的作品，将你的项目上传/提交到 GitHub 或其他类似的平台上是非常重要的。因为这个重要性，你应该做好每一件事。例如，你写了一些有趣的代码并想要提交它。你需要考虑一下，如果你的代码不可读，谁会去读它。你需要选择优化，而不是顺其自然。为了提高可读性，您需要:

1.  在解释这段代码如何工作的地方使用注释(同样，您可以使用注释来编写您想要在下一个代码块中添加的内容)。
2.  以匹配文档中描述的样式指南(对于 Python，是 PIP8)。
3.  尽可能地优化你的代码。

> "总是考虑别人会如何阅读你的代码，这很重要."

# 5.将所有内容放在一个函数中

一个函数只需要做一件事，你不需要在一个函数中放几个动作或者迭代。将它们分开会更容易和更好，你会知道每个函数做什么，剩下的就是实现它了。当你使用一个函数来处理所有事情时，你可能需要使用像“**和**，或者“**或者**这样的操作，这不是很好。此外，它将更具可读性，正如我们已经知道的，它对其他编码人员更好。

> "你需要写一个只有一个目的的函数."

# 6.选择正确的目标

不要想着开发一个一开始就能杀死脸书的应用程序，也不要想着从中能赚多少钱，因为在这方面它可能会是一个巨大的失败。我的意思是，如果你刚刚开始学习，那么选择一个类似于“ *Learn Discord.py library”的目标，为 Discord 制作一个会播放音乐的机器人*。或者，如果你已经在 IT 领域工作了一段时间，那么你就不需要考虑你将从这个项目中赚到多少钱。如果金钱是你的目标，那么你所做的一切都只是为了赚钱，你不会考虑如何更好地构建你的应用程序，或者想办法让你的设计更漂亮。

> "选择正确的目标可以节省你大量的时间和精力."

# 7.学习间隔时间太长

如果你决定学习编程语言或一个新的框架，那么你必须持之以恒。突出你学习这个新特性的时间，或者制定一个每日目标，比如“*花 1 小时学习 Django* ”。换句话说，如果你不是一成不变的，那么你会学习一些新的东西，休息一周，然后忘记你最近学的几乎所有东西，用很少的知识重新开始。

> “尽可能保持一致。”

# 结论

这是几乎每个程序员都会犯的 7 个非常常见的错误，你应该避免它们。你可能不同意我的观点，特别是关于功能和单独工作，我很高兴在下面的评论中与你谈论这个话题。我希望你喜欢读这篇文章。:)

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)