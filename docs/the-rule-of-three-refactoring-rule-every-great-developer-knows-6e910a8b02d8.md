# 伟大的开发人员应该知道的一条重构规则

> 原文：<https://javascript.plainenglish.io/the-rule-of-three-refactoring-rule-every-great-developer-knows-6e910a8b02d8?source=collection_archive---------14----------------------->

## 学习规则，变得更擅长重构

![](img/d7cb16c9d6e810e47ba1c00c05f4d6d0.png)

Photo by [olia danilevich](https://www.pexels.com/@olia-danilevich?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/man-sitting-in-front-of-three-computers-4974915/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

假设你写了两次完全相同的代码。你是一个优秀的开发人员，看到这是重复的代码。考虑到 DRY，你进行重构。

但这是正确的方式吗？你让代码更容易维护了吗？这个场景的衡量标准是什么？

让我们进入细节。

# 等等。

这是规则。等等。等待更多的复制。

也被称为“三法则”。或者“什么都写两遍”。

你经常看到相同的代码，三次或更多次？。重构。进行抽象。如果不是，就让它保持原样。

> “三振出局，你重构”——尼古拉斯·卡洛

接受小复制。没那么糟糕。错误的抽象比复制更糟糕。

> **复用代码时，复制一次，第三次只抽象**。—三原则

不等待的代价是一个糟糕的抽象概念。您没有足够的泛型来提取。两个用例是不够的。你需要两个以上，然后你可以做抽象。

# 为什么错误的抽象不好？

糟糕的抽象会导致糟糕的代码。不要为了抽象而添加抽象。这导致了糟糕的代码质量。

有多少次你不得不添加一个新的条件到现有的实现中？这就产生了混乱的代码，难以测试，难以维护。

以下是桑迪·梅斯如何看待糟糕的抽象。您可以自己推断代码质量问题。

Sandi Metz 说得很完美，所以我在这里重复一下。复制比抽象要好。

1.  程序员 A 看到了重复。
2.  程序员 A 提取复制并给它一个名字。
3.  *这创造了一种新的抽象。它可能是一个新的方法，甚至可能是一个新的类。*
4.  程序员 A 用新的抽象替换了复制。
5.  *啊，代码是完美的。程序员快乐地小跑而去。*
6.  时光流逝。
7.  一个新的需求出现了，当前的抽象几乎是完美的。
8.  程序员 B 的任务是实现这个需求。
9.  *程序员 B 觉得保留现有的抽象是义不容辞的，但由于每个案例的抽象并不完全相同，他们修改代码以接受一个参数，然后添加逻辑以根据该参数的值有条件地做正确的事情。*
10.  *曾经的通用抽象现在在不同的情况下表现不同。*
11.  另一个新的要求来了。
    *程序员 X.
    另一个附加参数。
    又一个新的条件句。
    循环直到代码变得不可理解。*
12.  你出现在这个故事中，你的生活发生了戏剧性的变化。—桑迪·梅茨

# 维护糟糕的抽象的代价是什么？

> *最快的前进方式是后退——桑迪·梅斯*

不要维护不好的抽象。重新做每件事。把代码放回客户端。你会看到复制并不是“如此复制”，它毕竟是不同的。

我们作为开发人员，不喜欢删除代码。我们生来就有这种感觉。我们遭受[沉没成本谬误](https://en.wikipedia.org/wiki/Sunk_cost#Loss_aversion_and_the_sunk_cost_fallacy)。失去的时间，开发人员的自负，以及其他阻碍我们改变的愚蠢想法。必要时我们需要减少损失。

重新引入重复，去除不良抽象。这是这个故事的重点。

# 三分律

[](https://understandlegacycode.com/blog/refactoring-rule-of-three/) [## 不要让干净的代码更难维护，使用规则三

### "你如何证明遵循干净的代码实践来编写更多的代码是合理的？"这是我现在看到有人问的问题，而且…

understandlegacycode.com](https://understandlegacycode.com/blog/refactoring-rule-of-three/) [](https://andrewbrookins.com/technology/the-rule-of-three/) [## 三的法则——安德鲁·布鲁金斯

### 许多程序员渴望在开发过程的早期创建可重用的组件。我知道我有！那么为什么…

andrewbrookins.com](https://andrewbrookins.com/technology/the-rule-of-three/) [](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction) [## 错误的抽象——桑迪·梅茨

### 我一直在思考“错误抽象”的后果我的 RailsConf 2014“所有小事”讲座…

sandimetz.com](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction) 

相关文章:

[](https://levelup.gitconnected.com/what-is-a-specification-pattern-460b32bfbf7b) [## 什么是规格模式？

### 用规格模式解开代码

levelup.gitconnected.com](https://levelup.gitconnected.com/what-is-a-specification-pattern-460b32bfbf7b) [](https://medium.com/dev-genius/how-to-avoid-anemic-domain-model-59775c639678) [## 如何避免贫血的域名模型？

### 如何处理业务逻辑，并避免贫血的领域模型。

medium.com](https://medium.com/dev-genius/how-to-avoid-anemic-domain-model-59775c639678) [](https://levelup.gitconnected.com/how-to-develop-better-program-structure-3a57f48bf971) [## 如何开发更好的程序结构？

### 改善程序结构的几个简单技巧

levelup.gitconnected.com](https://levelup.gitconnected.com/how-to-develop-better-program-structure-3a57f48bf971)