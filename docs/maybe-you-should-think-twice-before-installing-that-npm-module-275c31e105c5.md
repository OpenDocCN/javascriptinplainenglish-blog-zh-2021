# 也许你在安装 NPM 模块之前应该三思？

> 原文：<https://javascript.plainenglish.io/maybe-you-should-think-twice-before-installing-that-npm-module-275c31e105c5?source=collection_archive---------23----------------------->

NPM 库中的 NPM 模块提供了很多功能，但是应该谨慎使用。

![](img/45c2756e2ecdf792f9eaaf599b80e260.png)

Image courtesy of Marcus Kauffman on Unsplash

*原载于*[*https://fek . io*](https://fek.io/blog/maybe-you-should-think-twice-before-installing-that-npm-module/)*。*

被称为“左垫启示”的事件已经过去五年多了。2016 年 3 月，一名 NPM 用户从 NPM 库中删除了他们的模块“左补”，导致任何具有该依赖性的 [Node.js](https://nodejs.org) 应用程序中断。

这为 Node.js 社区敲响了警钟，并在此事件后对 [NPM](https://www.npmjs.com/) 进行了一些更改，以防止这种情况再次发生。

# 到底发生了什么

一家名为 [Kik](https://www.kik.com/) 的公司开发了一个 messenger 应用程序，它想和 NPM 的另一个用户[Azer kou Lu](https://www.kodfabrik.com/)使用同一个名为“Kik”的模块。他们给 Koç ulu 先生发了一封来自专利律师的电子邮件，要求他放弃名为“kik”的模块。科祖卢拒绝透露模块的名称。然后 Kik 带着商标申请去了 NPM，让他们使用这个模块，他们最终照做了。

在失去模块名称后，Koç ulu 先生决定取消出版他在 NPM 的所有 250 个其他模块。其中一个模块被用于数千个项目，包括 [Babel.js](https://www.npmjs.com/package/@babel/runtime) 。当他取消出版“左垫”，它基本上打破了互联网。这是因为很多项目依赖于 NPM，更不用说模块也有它们的依赖关系。你最终会得到这些巨大的依赖树结构，有时有 10 层之深。如果您想可视化这个，只需在您的模块目录中运行`npm list`。

这是由当时只有 11 行的模块造成的。

时任 NPM 首席技术官的劳里·沃斯采取了前所未有的举措，取消了一个模块的发布。作为一家公司，NPM 还相当年轻，以前从未遇到过这种情况。他们对他们的系统进行了更改，以防止用户在模块存在依赖关系的情况下取消发布该模块，从而防止此类事件再次发生。

这里有一些真实事件的帖子；

 [## 关于互联网断裂的讨论

### 大家好，我是 Kik 的信使主管。我不希望这是我在媒体上的第一篇文章，但是开源…

medium.com](https://medium.com/@mproberts/a-discussion-about-the-breaking-of-the-internet-3d4d2a83aa4d)  [## 我刚刚解放了我的模块——阿泽·科丘鲁的日记

### 几周前，一位专利律师给我发了一封电子邮件，要求我不要公开 NPM 的“kik”模块。我的回答是“不”,而且…

kodfabrik.com](https://kodfabrik.com/journal/i-ve-just-liberated-my-modules) [](https://www.davidhaney.io/npm-left-pad-have-we-forgotten-how-to-program/) [## NPM 和左垫:我们忘记了如何编程吗？

### 好了，开发者们，是时候进行一次严肃的谈话了。正如你可能已经意识到的，本周做出反应，巴别塔，和一个…

www.davidhaney.io](https://www.davidhaney.io/npm-left-pad-have-we-forgotten-how-to-program/) [](https://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm) [## npm 博客存档:kik，left-pad 和 npm

### 本周早些时候，许多 npm 用户遭遇了中断，因为许多项目都直接或…

blog.npmjs.org](https://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm) 

# 反思 NPM 模块

Node 的一个优点也可能是一个弱点，即能够随心所欲地使用任何功能。

![](img/a6e3ced3828e157c6d28495c0652ea95.png)

在安装任何 NPM 模块之前，你应该先问问自己，我真的需要包括这个模块吗？一个很好的例子就是 [moment.js](https://momentjs.com/) 。Moment 主要用于处理 JavaScript 中的日期对象。它还可以格式化日期和获取日期部分。

```
const year = moment().format('YYYY');
```

您也可以通过在 JavaScript 中对 date 对象调用`getYear()`函数来完成同样的事情。

```
const year = new Date().getYear();
```

# 本地回购

许多较大的组织现在预先批准哪些 NPM 模块可以用于一个项目。有些使用本地回购协议，这样他们的开发人员只能在他们的应用程序中使用预先批准的模块。

NPM 也提供 NPM 的本地版本，所以你可以为你的组织运行它。

# 德诺的方法

如果你不熟悉 [Deno](https://deno.land/) ，它是 Node.js 的发明者 Ryan Dahl 的替代 JavaScript 运行时，Ryan 在创建 Deno 时做的事情之一就是重新思考他如何在 Node 中做某些事情。

Node.js 没有标准库。当 Ryan 创建 Deno 时，他还确保它包含一个标准的模块库，您可以使用它而不必安装第三方模块。

Deno 还允许开发人员直接从源代码导入模块，因此不需要包管理器。你可以简单地在你的应用程序中使用`import 'https://github.com/someuser/mymodule/main/src.js'`，Deno 会在你的系统中缓存这个模块。

Deno 还有一个依赖检查器，可以用来评估你的依赖。只需运行`deno info`，Deno 就会运行它的 inspector。

# 研究您的模块

在你`npm install`任何你以前没有用过的模块之前，看一下源代码。NPM 上的大多数模块都是开源的，或者有许可证，你可以在那里查看源代码。**看出处！**

另一件要看的事情是模块使用的依赖关系。您应该关注的一件事是这些依赖关系存在了多长时间，是否存在任何安全问题。NPM 提供了一个安全审计，你可以在你的模块上执行。

`nome audit`将生成包含任何漏洞的报告。您还可以使用`npm audit fix`来解决模块中的任何漏洞。

# 结论

NPM 可以为您的节点应用程序添加大量额外的功能，但是您应该只在需要尚未提供的特定功能时使用它。尽可能考虑编写自己的模块。

NPM 上的大多数模块都是开源项目，大多数也在 [Github](https://github.com) 上。如果你发现一个现有的模块有问题，考虑做一个 pull 请求来回馈这个了不起的社区。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)