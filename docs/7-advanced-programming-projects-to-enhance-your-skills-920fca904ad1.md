# 7 个高级编程项目来提高你的技能

> 原文：<https://javascript.plainenglish.io/7-advanced-programming-projects-to-enhance-your-skills-920fca904ad1?source=collection_archive---------1----------------------->

## 超越平均水平，深化你的知识

![](img/b9baf8b97077c7adc0f917379eb3286f.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

没有人会因为什么都不做而变得更好。当然，这也适用于编程。我们开发人员需要不断挑战自己，跟上时代的步伐，提高我们的技能。这就是为什么接受复杂的项目对于程序员来说是重要的，以保持改进的动力，而不是陷入经验的停滞不前。

因为这些项目是有挑战性的，你不需要马上知道所有的事情。它们应该被视为一次旅行，在此期间，你可以学习新的概念，获得工作所需的技能。

这是[高级编程项目](https://medium.com/@nic-obert/list/advanced-programming-projects-85b9fa1bd147)系列的第三篇文章。如果你对这类文章感兴趣，我建议你去看看。

## 创造一种深奥的编程语言

一种深奥的编程语言，也称为 esolang，不适合在工业环境中使用。比喻通常是作为概念的证明或玩笑而产生的。最著名的例子之一是 [Brainfuck](https://en.wikipedia.org/wiki/Brainfuck) ，一种被设计成尽可能小的语言。

要创建一种新的深奥的编程语言，您将大致遇到这些步骤:

*   首先，你需要定义语言的句法和语法。你可以把它设计得简单、复杂或怪异，这完全取决于你。
*   定义它的行为。这包括考虑在给定的情况下，程序应该做什么。
*   最后，你需要实现它。这一步通常包括为特定的语言建立一个解释器或编译器。

如果您决定接手这个项目，请查看我的关于如何创建深奥的编程语言的系列文章:

[](/how-to-create-an-esoteric-programming-language-bf00f724795d) [## 如何创建一门深奥的编程语言

### 第 1 部分:认真定义笑话编程语言的基础。

javascript.plainenglish.io](/how-to-create-an-esoteric-programming-language-bf00f724795d) 

## 复古控制台仿真器

由于时间不够，我不再玩游戏了，但我过去喜欢启动我的[任天堂 DS Lite](https://en.wikipedia.org/wiki/Nintendo_DS_Lite) ，开始玩我手头的任何游戏。前一段时间我想再玩一次旧的[塞尔达传说标题](https://en.wikipedia.org/wiki/The_Legend_of_Zelda:_Phantom_Hourglass)，但是，不幸的是，我的主机不再工作了。这是我第一次尝试控制台模拟器，作为一个喜欢低级的程序员，我开始想知道它是如何工作的。

它原来是一个虚拟机，模拟物理控制台的行为，以便在特定控制台架构上运行的程序也可以通过仿真器执行。

接下这个项目会让你度过:

*   研究您想要模拟的特定控制台的体系结构。这就是为什么我建议复古，因为现代的控制台可能非常复杂，模仿它们可能需要比你的机器所能提供的更多的资源。此外，业余爱好者已经广泛研究了旧的架构，并且有关于其内部工作的在线指南，而公司不会将所有最新的系统细节公布于众。对于这样一个项目，我建议尝试 NES，因为它相对简单。想了解更多信息，建议你查看一下[本指南](https://wiki.nesdev.org/w/index.php?title=NES_reference_guide)。
*   通过虚拟机模拟控制台架构和行为。你必须实现所有的控制台 CPU 指令，寄存器，内存模块，最终的外围设备…
*   你还需要设计一个接口来发送控制器命令给程序。这通常是通过将用户输入值写入特定的存储器地址或寄存器以供程序处理来实现的。
*   最后，你需要实现一个可视界面，在屏幕上显示存储在[视频存储器](https://en.wikipedia.org/wiki/Video_RAM_(dual-ported_DRAM))中的任何内容。

这里有一个很棒的[指南](https://www.youtube.com/watch?v=F8kx56OZQhg)，教你如何从头开始构建一个 NES 模拟器。

## 客户端-服务器聊天应用程序

它不一定要成为下一个 WhatsApp 或 Discord，但它至少应该具备这两个关键特性:创建群组的能力和实时聊天的能力。

该项目将涉及:

*   处理到服务器的并发连接，因此线程和并发是必需的。
*   在所有连接的用户之间同步消息，并以正确的顺序保存它们，所有这些都考虑到连接延迟和相关问题。
*   管理组和消息的数据库，所以一些基本的 SQL 知识是必须的。我推荐阅读[这个](https://blog.discord.com/how-discord-stores-billions-of-messages-7fa6ec7ee4c7)故事来获得灵感。
*   您还需要创建一个最低限度可用的用户界面。每当有新消息可用时，这样的接口应该被动态地和自动地更新。

## 构建一个包管理器

软件包管理器是一个工具，可以让您安装、卸载、更新和管理软件包。软件包被定义为一个有组织的文件集合，这些文件组成一个程序、服务或信息，为一个更大的系统提供某些功能。

构建包管理器主要包括:

*   向托管包的服务器发出 HTTP 请求。
*   跟踪当前安装的软件包、它们在文件系统中的位置以及它们在数据库中的版本。
*   最终，您需要提升您的权限来写入受保护的文件夹。
*   锁定在安装或更新期间可能使用数据库和软件包管理器所需的其他资源的其他进程。这种行为可以通过[锁文件](https://fileinfo.com/extension/lock)来实现。

## 设计一个文件系统

你每天都在使用它，甚至没有注意到。它在涉及读写磁盘的每个操作中都至关重要。[文件系统](https://en.wikipedia.org/wiki/File_system)是一种用于组织、存储和从长期计算机内存中检索信息的方法和数据结构。

你可以从 [FAT 文件系统](https://en.wikipedia.org/wiki/File_Allocation_Table)家族中获得灵感，这是至今仍在使用的最简单的设计之一。一般来说，您必须:

*   设计系统文件分配表，该结构用于跟踪各种[数据簇的](https://en.wikipedia.org/wiki/Data_cluster)位置，它们是否已经被使用或不可用，以及其他信息。
*   设计[目录表](https://en.wikipedia.org/wiki/Design_of_the_FAT_file_system#Directory_table)，一个用来跟踪目录及其在内存中的内容位置的结构。
*   创建[工具](https://en.wikipedia.org/wiki/File_system#Utilities)来创建文件系统并与之交互。这些工具允许使用它们的程序在磁盘上创建、删除和搜索文件，而不用关心集群和数据是如何组织的。

## 制作一个游戏和一个玩这个游戏的人工智能

这里真正的困难不在于制作游戏，而在于开发人工智能代理来有效地玩游戏。你可以把它做得像 [Flappy Bird](https://en.wikipedia.org/wiki/Flappy_Bird) 或者 [Snake](https://en.wikipedia.org/wiki/Snake_(video_game_genre)) 一样简单，也可以做得更复杂 [RPG](https://en.wikipedia.org/wiki/Role-playing_game) 。

人工智能代理既可以是主角，也可以是你必须对抗的敌人。这样的代理应该根据上下文智能地行动，这意味着它必须知道它的周围环境和它的内部状态，例如健康和其他属性。

这个项目将带你度过:

*   显示实际的游戏并提供用户界面。您可能会决定使用简单的命令行或成熟的窗口。这可以通过使用大多数流行的编程语言都拥有的库或框架来实现，甚至可以通过自己编写渲染引擎来实现。
*   开发一个游戏，你可能需要一个合适的[引擎](https://en.wikipedia.org/wiki/Game_engine)。有很多很棒的游戏引擎，比如 [Unity](https://en.wikipedia.org/wiki/Unity_(game_engine)) 或者[虚幻引擎](https://en.wikipedia.org/wiki/Unreal_Engine)，但是如果你愿意，你可以自己编写代码。
*   显然，开发游戏。这一步完全取决于你的选择，但是你应该在设计的时候考虑到需要方便地访问 AI 代理所需要的所有信息。
*   实现人工智能代理。这一步也完全依赖于你创建的游戏。根据上下文，您可以决定使用[强化学习](https://en.wikipedia.org/wiki/Reinforcement_learning)和其他机器学习技术，或者自己编写算法。
*   如果你决定使用机器学习模型来实现人工智能代理，你也需要训练它。[在这里](https://oden.io/glossary/model-training/)您可以找到流程的简要概述。

## 构建一个编程语言编译器

[transpiler](https://en.wikipedia.org/wiki/Source-to-source_compiler) ，也称为源到源编译器，是将一种编程语言源代码翻译成另一种目标语言的程序，例如 [TypeScript](https://en.wikipedia.org/wiki/TypeScript) 被转换成 JavaScript。

正如你可能已经猜到的，它与传统的编译器非常相似，除了它最后不产生机器码，而是产生源代码。编程这样一个工具将带你通过:

*   [标记化](https://en.wikipedia.org/wiki/Lexical_analysis)输入的源代码。这个过程包括将不同的字符组合成小的有意义的单元，称为记号。例如算术运算符`+`和`-`、字符串、数字和标识符。
*   [生成的记号序列的语法分析](https://en.wikipedia.org/wiki/Parsing)。这个过程包括找出记号之间的关系，并通过一棵[抽象语法树](https://en.wikipedia.org/wiki/Abstract_syntax_tree)来表示它们。
*   最后，简化生成的语法树，使其既可以用来表示输入语言，也可以用来表示目标编程语言。这一步不是强制性的，但是当两种语言非常不同时，这一步就派上了用场。实现这一点的最简单的方法是递归地将每个操作树翻译成更简单的组件。例如，类定义可以简化为更通用的数据结构，如类似 C 的结构或数组。
*   将结果语法树转换成其自身的更高级表示。这意味着，如果目标语言允许用一种更习惯的方式来表达相同的行为，那么这种表达就会被翻译成更高级别的表达。一个简单的例子是将像`a = a + b`这样的赋值语句变成`a += b`。
*   最后，您必须将语法树展平为一系列标记。为了做到这一点，您必须考虑目标语言操作符的优先级，以及添加一些括号来强制执行正确的求值顺序的必要性。新生成的令牌序列现在必须被翻译成它们最终的字符串表示形式:目标源代码。

## 结论

总而言之，对于开发人员来说，为了继续改进，让自己面对复杂项目的挑战是至关重要的。就像你不会因为一遍又一遍地举起同样的重量而变得更强壮一样，你不会因为呆在舒适的泡泡里而学到任何新东西。

> 学习不是一个被动的过程:你不会提高你的知识，除非你让自己接触未知。

你可能不知道如何承担这些项目，这完全没关系。当我决定开始一个新的复杂项目时，我也没有:我的目标不是独自创造世界上最好的 transpiler，而是通过旅程来学习它是如何完成的。

我希望你喜欢这篇文章。如果你心中有任何其他伟大的项目，请在评论中分享。如果您想阅读更多关于高级编程项目的内容，请查看我下面的系列文章:

[](https://betterprogramming.pub/7-advanced-projects-to-improve-your-programming-skills-f05d7875104) [## 提高编程技能的 7 个高级项目

### 走出你的舒适区，提升你的技能

better 编程. pub](https://betterprogramming.pub/7-advanced-projects-to-improve-your-programming-skills-f05d7875104) 

**感谢阅读！**

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***