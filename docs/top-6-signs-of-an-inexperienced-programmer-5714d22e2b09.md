# 缺乏经验的程序员的 6 大标志

> 原文：<https://javascript.plainenglish.io/top-6-signs-of-an-inexperienced-programmer-5714d22e2b09?source=collection_archive---------9----------------------->

## 这些迹象表明，缺乏经验是不言自明的

![](img/6bc4d25d47a79e4eb541fbc60633a827.png)

Photo by [KoolShooters](https://www.pexels.com/@kool-shooters?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/young-man-sleeping-beside-a-yellow-tv-6976097/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

在软件工程中，你会发现有人说经验等于在这个行业中工作的总年限。这不是真的。

有时你会遇到年轻的开发人员，他们比有五年经验的开发人员写出更好的代码。一些有多年经验的开发人员编写代码和行为的方式就像他们刚刚开始做他们的工作一样。

当你读到他们写的代码时。您会注意到他们没有遵循文档，创建了一个大的拉请求，并且犯了许多只有没有经验的开发人员才会犯的错误。

这是六个主要的标志，可以帮助你识别这些没有经验的开发人员。

```
· [1\. Write too many unnecessary comments](#7d6d)
· [2\. Getting offended during code review](#2053)
· [3\. Large pull request](#4ab6)
· [4\. Difficult to communicate with](#8474)
· [5\. They write long comments](#0a56)
· [6\. They copy others code without understanding](#87bb)
· [Summary](#35cb)
```

# 1.写太多不必要的评论

注释的目的是增加代码的价值并解释正确的逻辑。但是没有经验的开发人员用他们无用的注释使代码库变得复杂。

这些开发者写的评论都是浪费时间。当其他开发人员看到这些评论时。看起来，如果没有注释，代码应该很容易阅读。

那些书面的注释在代码库中并不重要。所有没有经验的程序员写的评论都是多余的。

注释被添加到代码库中，以使其更具可读性。如果你的代码写得很好，你不需要写注释来解释每一行代码。

举个小例子:

```
a++; // Increasing the value of the variable a
```

没有经验的开发人员为不言自明的代码编写注释。即使是前几天才开始学习编码的开发者，也知道增量运算符的作用是什么。

冗余代码注释的另一个例子:

```
/* setting the value of the integer myDogs to 3 */int myDogs = 3;
```

# 2.在代码评审过程中被冒犯

对于初学者来说，代码评审是一个由一个或多个人验证源代码的活动。在代码审查期间，除了代码作者之外，至少要有一个人参与到这个过程中。

一个没有经验的开发人员认为找出开发人员犯的所有错误是代码审查人员的职责。写完代码后，他们甚至懒得检查一次。

在他们写完代码后，他们将发出拉请求。如果他们习惯于至少检查一次错误，就不要发出拉请求。他们肯定会在代码中发现一些错误模式。

作为开发人员，我们一次又一次地犯同样的错误。如果我们能自己找到那些重复的错误。代码审查者将不必发现同样的错误。

如果代码评审员在开发人员的代码中发现同样的错误。他们认为开发商不重视他们的时间。他们有点恼火。这导致代码评审者对代码进行苛刻的评论。

一旦开发人员读到评审人员的那些苛刻的评论。他们被冒犯了。从那时起，没有经验的开发人员开始讨厌他们的代码审查人员。

即使在代码审查者出错的情况下。一个没有经验的开发人员试图报复代码审查者。没有经验的开发人员在这种情况下表现出他们的智慧。

作为一名开发人员，即使您收到了来自审查者的消息，如:

```
"This is complicated and confusing."
```

而不是问类似这样的后续问题:

```
"Tell me what is so confusing about the code. Everything is simple."
```

开发人员应该问:

```
"Can you suggest what kind of changes would help?"
```

没有经验的开发人员会制造不必要的麻烦。当开发人员愿意做出改变时，评审人员肯定会建议一些他们会从中受益的东西。

# 3.大型拉取请求

代码审查者讨厌大的拉请求。对于代码评审者来说，小的拉取请求更容易提供反馈。代码评审员不想评审 1000 行代码变更。

理想情况下，他们喜欢少于 100 行的变化。在某些情况下，它可以超过 100 行，达到 250–300 行。但是超过 300 行的代码更改会惹恼评审者。

我总是发现没有经验的开发人员提出大量的拉请求。不仅仅是初级开发者，还有高级开发者。

这些没有经验的开发人员宁愿默默工作一个多星期，也不寻求反馈。在他们完成对代码的大修改后，他们会发出一个拉请求。

当代码审查者看到如此大的拉请求时。你会经常发现评审员要求这些开发人员把它分成更小的部分。

这些程序员经常会说，他们试图用一个大的拉请求来实现一个单一的改变。他们试图让评审者相信他们正在尝试应用单一责任原则。

但实际上，他们是在用单一责任原则的名义自救。

如果他们对自己诚实，他们知道他们可以把一个大的改变分成几个部分。尽管如此，他们还是喜欢发出大量的拉取请求，只是为了增加评审者的工作量。

如果你是一个做大量拉取请求的开发人员。你得把它分成几个小部分。您应该制作一个清单，向审阅者发送一个小的拉请求，而不是发出一个大的拉请求。

# 4.难以沟通

缺乏经验的开发人员过于自信，认为他们了解他们技术栈的一切。由于他们过于自信，他们不愿意学习任何新的东西。

无论是初学者还是工作了几年的程序员，你都可以观察到这种行为。他们充满了自我和傲慢。

最近完成学位的开发人员很少是自以为是的。他们打击了整个团队的士气。他们不愿意放弃他们在大学里学到的一些糟糕的编码实践。

这些新手不接受，作为一个专业开发人员，不能像大学时那样编码。这让他们更加傲慢，同时，他们的沟通能力也很差。

他们喜欢打断高级开发人员的谈话。当他们打断时，他们表现出自我中心。没有一个开发者愿意在向你解释某件事情的时候被打断。

这些没有经验的程序员喜欢打断别人，让别人觉得自己无足轻重。

我观察过没有经验的开发者做伪听。他们只是在交谈时看起来很专注，但实际上他们在想别的事情。

你会遇到有四年经验，仍然很难沟通的程序员。我们应该停止称那些开发者为有经验的开发者。他们应该被称为没有经验的开发者。

# 5.他们写很长的评论

无论你是通过完成学位、参加训练营还是通过在线课程学习编程。这些都告诉我们，你需要对你的代码进行注释。

我们被告知代码注释直接关系到代码的质量。这意味着评论的数量越多，你的代码质量就越高。此外，我们被教导相信注释使代码可读。

作为学生，我们因为没有在代码上写注释而受到惩罚。大多数没有经验的开发者把评论看得太重了，以至于他们写评论来解释评论。

没有一个程序员指望看 5 行注释就能理解 1 行注释的意思。程序员浪费了宝贵的时间去阅读这样的评论。

有了冗长的注释，代码库变得很难阅读。

没有经验的开发人员会添加很长的注释，因为他们觉得自己的代码很复杂。没有人能不看评论就理解代码。他们添加了很长的注释来消除读者的困惑。

举个例子，我发现了一个又长又搞笑的评论:

```
/** You may think you know what the following code does.* But you don't. Trust me.* Fiddle with it, and you'll spend many a sleepless* night cursing the moment you thought you'd be clever* enough to "optimize" the code below.* Now close this file and go play with something else.*/
```

如果你是一个发现你的代码需要长注释的开发者。与其添加注释，不如通过重构来提高代码的可读性。你不应该不断添加更多层令人困惑的文字。

你应该尽可能保持你的评论简短，不要写太长的评论。

# 6.他们在不理解的情况下复制别人的代码

没有经验的开发人员习惯等到最后几个小时才完成任务。随着最后期限的临近，他们开始恐慌。在最后几个小时里，他们试图完成他们的工作。

在那几个小时里，他们试图在网上搜索代码。一旦他们找到一个代码，他们会对代码做一些小的修改，这样他们就不会被发现。他们并没有试图去理解他们将要使用的代码。

他们只是将修改后的代码复制并粘贴到代码库中。有了复制的代码，他们可以按时完成工作。他们不理解复制代码可能产生的后果。

这种复制的代码会导致整个系统的安全缺陷。没有经验的程序员认为，既然代码运行良好，代码就不会发生太多事情。

复制的代码可能会导致代码许可问题。这可能导致垃圾收集。因为复制的代码将包含一些您的应用程序永远不需要的额外代码行。

如果你是一个盲目从 web 上复制粘贴代码的开发者。你应该首先试着理解代码是做什么的，并正确地阅读它。在你阅读和理解它之前，你不应该复制和粘贴它。

# 摘要

1.  他们写不必要的评论。
2.  他们在代码审查期间被冒犯了。
3.  他们创建了一个大的拉取请求。
4.  他们很傲慢，很难沟通。
5.  他们写评论解释评论。
6.  他们在不理解代码的情况下复制和粘贴代码。

# 想联系作者？

加入一个人人社区，欣赏与科技相关的文章。我们讨论最新的技术和独特的见解。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***