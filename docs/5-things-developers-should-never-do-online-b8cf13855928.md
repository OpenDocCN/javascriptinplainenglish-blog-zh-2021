# 开发者永远不要在网上做的 5 件事

> 原文：<https://javascript.plainenglish.io/5-things-developers-should-never-do-online-b8cf13855928?source=collection_archive---------16----------------------->

## 开发人员不应该在线执行的活动。

![](img/e12a2d4b3ef424c25a0df98bb9fe3d46.png)

Photo by [Grianghraf](https://unsplash.com/@grianghraf?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

程序员每天都在使用谷歌，如果任何开发人员说他没有，那么他或她在撒谎。

对于 GitHub 和 StackOverflow 这样的网站以及 Medium 这样的博客网站，几乎每个程序员都必须每天访问这些网站。

当我们中的一些人搜索编码课程和问题的解决方案时，一些人搜索以探索和扩展他们的编码知识。

尽管如此，使用谷歌已经成为开发阶段的一个重要部分。

然而，许多开发人员仍然不知道如何&搜索什么来获得他们需要的答案和结果。

在这篇博客中，我将讨论开发者不应该谷歌的 6 件事:

## #1.搜索整个错误消息

永远不要搜索完整的错误消息。

您需要阅读错误，并且只搜索错误消息的相关部分。

通常，有一个`.message()`方法，您可以调用它来获得一个人类可读的错误，然后您可以使用它来搜索。

```
<script>
    try {
         allert("A computer science portal");
        }
     catch(err) {
         document.write(err.message);
        }
</script>
```

在这里你会得到“allert 未定义”的错误信息，这是简单的阅读和理解。

然而，很多时候错误信息是非常全面的，可能看起来很吓人。但幸运的是，阅读它们非常容易，它们实际上帮助我们调试。

这里有一个错误，你不需要完全放入你的谷歌搜索栏。

```
Exception in thread "main" java.lang.NullPointerException
        at com.example.myproject.Book.getTitle(Book.java:16)
        at  com.example.myproject.Author.getTitles(Author.java:25)
        at com.example.myproject.Bootstrap.main(Bootstrap.java:14)
```

你可以看到问题出现在第一行，即`java.lang.NullPointerException`，你只需要在线搜索该部分。

其余的错误称为堆栈跟踪。你可以在这里了解更多关于[的信息。](https://stackoverflow.com/questions/3988788/what-is-a-stack-trace-and-how-can-i-use-it-to-debug-my-application-errors)

## #2.搜索窍门和技巧

寻找更快完成工作的捷径总是受欢迎的，然而大多数开发人员遵循任何在线可用的提示和技巧。

对于只有你会管理的小规模项目来说可能没问题。

> 然而，对于大型项目或涉及其他成员的项目，坚持众所周知的实践和结构是明智的。

就个人而言，我喜欢寻找有用的技巧来帮助我更快地构建东西，我甚至写了几篇关于它们的博客，但是使用过时的技巧和我在网上遇到的每一个技巧都有很多缺点。

其中一些缺点是网络兼容性问题，不可读的代码，有时性能可能会受到影响。

因此，你永远不要专门去寻找解决复杂问题的技巧和捷径。

## #3.安装不必要的 NPM 软件包

网上有数以百万计的 npm 软件包，其中也包括许多荒谬和不必要的软件包。

安装对您的项目几乎没有帮助的不必要的包可能弊大于利。

这些包已经多次破坏了 JavaScript 项目。我最近遇到的是去年对“is-promise”库的臭名昭著的更新。

> 如果你能在 Node.js 中做一些事情，你的 npm 包也能做到。它实际上获得了对您的环境的完全访问权。

因此，在安装未知的软件包时要小心，并且[总是检查漏洞。](https://medium.com/@nodepractices/were-under-attack-23-node-js-security-best-practices-e33c146cb87d)

事实上，[在我最近的博客中，我已经报道了一些这些荒谬的软件包。](/7-ridiculous-npm-packages-you-wont-believe-exist-4bf1ac8c884d)

## #4.跟踪网上的每一个趋势

我们都记得 Deno 是如何被誉为 Node.js 的替代品的，但是这些天我们几乎看不到任何关于 Deno 的讨论，除非你专门搜索它。

仅仅因为一个框架在媒体上被谈论了很多，并不意味着如果你没有尽快学习它，你就会被排除在外。

这种 FOMO(害怕错过)在技术社区很常见，尤其是在新来者中。

只学习你真正觉得对你和你的工作相关和有用的技术。

了解不同的栈和语言仍然是好的，但是深入到你遇到的任何东西都会导致迷失和适得其反。

> 精通那些真正有益于你工作的技术，比成为一个万事通、一无所知的大师要好。

那么，你如何知道你的学习之旅应该是什么样的呢？

通常有经验丰富的人在网上免费制作的开发者路线图，你可以用来作为规划学习的参考。

对于 web 开发，我发现 GitHub 上的[开发者路线图非常有用。](https://github.com/kamranahmedse/developer-roadmap)

## #5.教程地狱&堆积课程

毫无疑问，如今互联网是学习新技能或新特质的绝佳场所。

然而，我们经常最终买了很多课程，然后当我们不能完成它们时感到不知所措和紧张。

这可能会导致所谓的“教程地狱”，当你一个接一个地连续观看教程时，你会认为自己在学习新技能。

然而，一旦你开始建立一些真实的东西，并把这些新学到的技能用上，你就会意识到你几乎什么都不记得了。

包括我在内的大多数初级开发人员都至少有一次有意或无意地陷入了教程地狱。

当你想学习新的东西时，你不应该直接搜索深入的综合课程，而是先在 YouTube 这样的平台上浏览一下。

例如，几周前我想学习另一种语言，但我没有购买完整的课程，而是在 YouTube 上学习了基础知识和用法，并意识到它与我并不相关。

## 最后的想法…

使用和了解网络是开发阶段的关键部分。

无论是寻找应用程序崩溃的原因，还是学习一门新语言，开发人员都积极地依赖互联网来完成工作。

然而，有一些我们经常倾向于在网上做的事情在本质上是适得其反的，在这篇博客中，我强调了其中的一些。

如果你喜欢读这篇文章，考虑使用[我的推荐链接](https://medium.com/@anuragkanoria/membership)，这样你就可以通过点击[这里](https://medium.com/@anuragkanoria/membership)无限制地访问我的博客以及其他作者的博客。

我写了一个[类似的博客，探索更好地搜索的技巧，](/5-google-search-techniques-to-quickly-find-solutions-answers-532974c2a196)，你可能会发现有帮助。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)