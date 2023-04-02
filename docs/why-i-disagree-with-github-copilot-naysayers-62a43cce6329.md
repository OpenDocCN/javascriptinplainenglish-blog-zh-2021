# 为什么我不同意 GitHub Copilot 唱反调

> 原文：<https://javascript.plainenglish.io/why-i-disagree-with-github-copilot-naysayers-62a43cce6329?source=collection_archive---------10----------------------->

![](img/3206a0d74d379709daabccb0fbec24fc.png)

Modified screenshot from Github Copilot [homepage](https://copilot.github.com)

今天我在读 Medium，看到了几篇文章，讲的是如何避免使用 GitHubs 新的 Copilot 功能。对于一个总是热衷于尝试新事物的行业来说，我很惊讶地看到对 GitHub 团队目前正在开发的新技术的技术预览有如此多的负面评价。

在读了几篇这样的文章并给了他们一些思考后，我想我应该写下我自己对这件事的看法。

在开始之前，作为参考，我阅读了以下文章:

*   [你应该避免 GitHub Copilot 而选择“单飞”的 6 个理由](https://betterprogramming.pub/6-reasons-why-you-should-avoid-github-copilot-and-fly-solo-instead-8a948665433f)
*   4 [我对 GitHub 副驾驶的担忧](https://betterprogramming.pub/4-concerns-about-github-copilot-b9214d5416fa)
*   [如果你使用 GitHub 的人工智能副驾驶，你可能会被起诉](https://medium.com/geekculture/githubs-ai-copilot-might-get-you-sued-if-you-use-it-c1cade1ea229)

# 技术预览

我必须指出的第一点是，当前版本的 GitHub Copilot 是一个技术预览版。引用常见问题:

> **GitHub Copilot 有多好？**
> 
> 我们最近对一组 Python 函数进行了基准测试，这些函数在开源 repos 中有很好的测试覆盖率。我们把函数体清空，让 GitHub Copilot 来填充。该模型在第一次尝试中有 43%的正确率，在允许尝试 10 次的情况下有 57%的正确率。而且它一直在变得越来越聪明。
> 
> [https://copilot . github . com/# FAQ-how-do-I-get-the-most-out-of-github-copilot](https://copilot.github.com/#faq-how-do-i-get-the-most-out-of-github-copilot)

我对此的理解是，GitHub 已经在内部测试中尽可能多地使用了该工具，他们需要真正的用户来使用该工具并给予反馈。他们需要该工具，以便能够向真正的开发人员学习，以及他们如何调整自己的工作流程来利用 copilot。

我的期望是，在这一点上，它不会是完美的，它会有问题，但 Github 的团队将努力解决这些问题。

# 许可法律问题

这些帖子的一个共同主题是，您使用 GitHub Copilot 编写的代码可能会导致以后的法律问题。

GitHub Copilot 的工作方式是，根据您已经编写的代码或您写的注释，为您提供单行或整个功能的建议。它会推断出你的意图，然后根据从大量公共代码中获得的信息提出建议。

这里的问题在于副驾驶如何知道该建议什么。引用 Githubs 自己的常见问题:

> GitHub Copilot 由 OpenAI Codex 提供支持，OpenAI 创建了一个新的 AI 系统。它已经接受了一系列英语和来自公开来源的源代码的培训，包括 GitHub 上的公共存储库中的代码。
> 
> [https://copilot . github . com/# FAQ-what-data-has-github-copilot-trained-on](https://copilot.github.com/#faq-what-data-has-github-copilot-been-trained-on)

在另一个常见问题中，他们解释并证明了为什么他们认为这是最好的数据集。

> 在公开可用的数据上训练机器学习模型被认为是整个机器学习社区的公平使用。这些模型从公众的集体智慧中获得洞察力和准确性。但这是一个新的空间，我们渴望与开发者就这些话题展开讨论，并引领行业为训练人工智能模型设定适当的标准。
> 
> [https://copilot . github . com/# FAQ-why-was-github-copilot-trained-on-data-from-public-available-sources](https://copilot.github.com/#faq-why-was-github-copilot-trained-on-data-from-publicly-available-sources)

这里的问题在于，没有关于许可代码的许可证的信息。因此，完全有理由假设他们包含了不允许以这种方式使用的授权代码。

为了帮助我们理解常见的开源许可，我们可以使用 https://choosealicense.com/licenses/[的许可摘要。由此我们可以看出，使用某些许可证的代码可能存在一些灰色地带，特别是 GPL 许可证集通常被视为更具限制性的开源许可证之一，它要求使用它的代码也在同一许可证下发布。](https://choosealicense.com/licenses/)

Nat Friedman 在推特上回应了这些担忧，他说:

[https://twitter.com/natfriedman/status/1409914420579344385](https://twitter.com/natfriedman/status/1409914420579344385)

他认为使用公共数据是合理使用的观点很有意思，就像我们看一下韦氏词典对合理使用的定义一样。该定义如下:

> 一种法律原则，认为可以不经版权所有者的许可而使用部分受版权保护的材料，只要这种使用是公平合理的，不会严重损害材料的价值，也不会减少所有人合理预期的利润
> 
> [https://www.merriam-webster.com/dictionary/fair%20use](https://www.merriam-webster.com/dictionary/fair%20use)

如果我们应用这个定义，问题可能在于企业有时会双重许可他们的软件应用程序，既有支持开源的 GPL 许可，也有销售给客户的商业许可。在这种情况下，使用 Copilot 生产的竞争产品可能会意外地使用 GPL 许可版本中的代码，然后继续“减少所有者合理预期的利润”。因此，这将违反合理使用。

考虑到这一点，我可以从中理解为什么人们会担心。我希望随着该工具在 GitHub 的技术预览版中发布，他们将会解决这些问题。我很乐意看到将源数据集限制在您能够遵守的许可范围内的能力。

与此同时，与其说这让我完全放弃使用 Copilot，不如说我会选择对我从 StackOverflow 或我使用的开放源代码库中复制的代码应用同样的谨慎。也就是花时间检查编写的代码，想想我是如何编写的，不要依赖它来编写应用程序的大部分内容。

# 暴露你的代码

我看到的另一个问题是，它暴露了您为分析而编写的代码，因为它们继续改进允许应用程序工作的模型。

如果我们再看看 GitHub 在他们的常见问题中对此有什么要说的:

> **GitHub Copilot 收集的数据是如何使用的？**
> 
> 为了生成建议，GitHub Copilot 会将您正在编辑的部分文件传输给服务。这个上下文用来为你综合建议。GitHub Copilot 还会记录建议是被接受还是被拒绝。这种遥测技术用于改进人工智能系统的未来版本，以便 GitHub Copilot 能够在未来为所有用户提供更好的建议。未来，我们将为用户提供控制遥测技术使用方式的选项。更多关于我们使用遥测技术的信息可以在[这里](https://github.co/copilot-telemetry-about)找到。
> 
> [https://copilot . github . com/# FAQ-how-is-the-data-github-copilot-collection-use](https://copilot.github.com/#faq-how-is-the-data-that-github-copilot-collects-used)
> 
> **传输的数据安全吗？**
> 
> 所有数据都被安全地传输和存储。在需要知道的基础上，遥测技术的访问严格限于个人。对收集到的源代码的检查将主要是自动的，当人们阅读时**特别是为了改进模型或检测滥用。**
> 
> [https://copilot . github . com/# FAQ-is-the-transfer-data-safe](https://copilot.github.com/#faq-is-the-transmitted-data-secure)

我用粗体突出显示的主要关注领域是，人类可能会带着改进模型的目的阅读代码。这里的问题是，如果你的代码是在一个保密项目中，甚至可能被一个非保密协议(NDA)所覆盖，你可能会因为以这种方式暴露你的代码而将自己置于危险之中。虽然不是故意的，但是手动检查日志以改进模型的人可能会偶然看到一些机密的东西。

GitHub 自己试图向您保证，他们收集的数据纯粹用于改进用于生成代码的模型。在常见问题解答中，他们说了以下内容:

> 我的私有代码会被其他用户共享吗？
> 
> 不。我们使用遥测数据，包括关于用户接受或拒绝哪些建议的信息，来改进模型。在为其他用户生成代码时，我们不会引用您的私有代码。
> 
> [https://copilot . github . com/# FAQ-will-my-private-code-to-shared-other-users](https://copilot.github.com/#faq-will-my-private-code-be-shared-with-other-users)

理解这一点很重要，因为这样你就可以与你的管理团队或与你有 NDA 关系的人就该工具、它提供的好处及其工作原理进行对话。

此外，目前 GitHub Copilot 仅使用当前文件作为您试图实现的内容的背景，因此不太可能有足够的内容被披露给他们以发现任何机密。

就我自己的使用而言，我写的大部分代码都不是机密的，也没有被 NDA 覆盖。即使在我的工作中，我在需要其他系统的上下文来理解它做什么的系统上工作，所以我不担心我与 GitHub 共享的一点点上下文，以使我能够利用 Copilot。

# 概括起来

虽然我不会建议你在试用 GitHub Copilot 时放弃所有的谨慎，但我会建议你实事求是地看待它，这是一项令人兴奋的技术的技术预览。

它既不是你作为工程师的替代品，也不是另一个人配对的替代品。以我目前的经验来看，这更像是我们在咨询 docs 或 StackOverflow 时所做的迭代。特别是，当第一次使用 JavaScript 库时，Copilot 帮助我编写了初始代码，否则我会花很多时间查阅文档。

考虑到这一点，我鼓励您注册技术预览版并尝试一下，首先在一些个人项目中使用它，看看它是如何工作的，并形成您对它的想法。

最后，我想补充一个免责声明，我既不是律师，也不是代码许可证方面的专家。我只是一个开发者，根据我所做的研究来分享我的观点。因此，我鼓励你做你自己的研究来消除你的任何顾虑。

*更多内容看*[***plain English . io***](http://plainenglish.io)