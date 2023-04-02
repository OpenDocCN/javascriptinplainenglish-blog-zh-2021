# 构建 2021 年 Web 应用的关键技术基础

> 原文：<https://javascript.plainenglish.io/key-technology-fundamentals-to-build-your-web-app-in-2021-af6da3efce30?source=collection_archive---------21----------------------->

## 2021 年构建现代网站和移动应用需要熟悉的技术。

随着整个世界都处于疫情模式，很多人一直在质疑他们的“一个收入来源”在过去的两个月里，我有八个非技术类的同事、朋友和家人来找我，问我有没有一个想法，想从技术的角度得到发展方向。

在向八个不同的人解释了八次基本原理之后，我开始意识到，仅仅是谷歌搜索“如何建立一个应用程序或网站”就会产生数十亿条结果，这使得找出下一步该做什么成为一项令人生畏的艰巨任务。

对于任何想开始自己的业余生活、付钱给开发人员制作网站/应用程序，或者只是想了解技术如何工作的人来说，这里有一个网站和移动应用程序如何构建的基本框架结构，以及一个可以考虑的不同技术的列表。

![](img/aef3fa79fbccab0396f040ab562f33ff.png)

Photo by [Tobias Fischer](https://unsplash.com/@tofi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> **注:**本文仅关注技术。它的意图并不是暗示所有的想法都可行。我对此的建议是——在辞掉全职工作之前，做一些市场调查，验证一些东西。

## 故障

当我们加载一个网站或应用程序时，技术看起来非常简单。事实上，有很多部分连接在一起提供一种体验。这些部分可以从根本上分为:

**前端层**——在这里我们创建用户如何与我们的想法互动。我们希望提供最好的视觉体验*，从加载应用程序到他们关闭它(以及这之间的一切)。*

***集成层** —这可以看作是我们创建的一系列高速公路，以便数据可以在我们的前端层和后端(数据)层之间传递。这里，我们还考虑了优化和安全性。该层通常表示为一种形式的 [API](https://en.wikipedia.org/wiki/API) 。*

***后端层** —也被认为是数据层。这是我们存储捕获的所有信息以及我们想要显示或更改的信息的地方。通常，我们创建我们的结构，以便只有我们的集成层可以与我们的数据层对话，其他的什么也不能。这通常是以数据库的形式完成的。*

*现在我们已经了解了几乎任何网站/手机 app 的基本骨架结构，接下来我们来看看一些常见的技术。*

## *要考虑的技术*

*技术永远在变化，这篇文章不会永远相关。因此，在我写这篇文章的时候(2021 年初)，这里有一些很容易掌握并且值得用来构建应用程序的关键技术。*

***前端层(网站/移动应用)***

*![](img/c39dc9c4e81374ba4c329e2110b73fdb.png)*

*Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

***React/React-Native—**React 和 React-Native 是 JavaScript 中实现的两种常见“框架”。网上有大量的教程，从根本上来说，这两者的概念是相同的，它们都是琐碎的。React 主要用于构建 web 应用和渐进式 Web 应用(PWA——充当移动应用的网站)。React-Native 用于创建 iOS 和 Android 移动应用程序。它真的很受欢迎，因为它提供了学习 Java(或 Android 的 Kotlin)和 Swift(或 iOS 的 Objective-C)的替代选择。*

***Expo —** 最初主要是作为 React-Native 之上的一个额外抽象，防止任何人与 Java 或 Objective C 进行交互(有时 React-Native 需要这样做)。它现在已经发展到适应 web 开发和 PWA 开发。该平台在社区中得到了很好的支持，使得开发前端应用程序变得更加容易。基本上，你仍然需要写 JavaScript。*

***Angular/Ionic—**Angular 是用 JavaScript 构建的一个不同的框架，它提供了构建现代网站和 pwa 的能力，Ionic 的编写类似于 Angular，但专注于开发混合的 iOS 和 Android 应用。*

> ***我的建议**:从 React 开始。*

## *集成层*

*![](img/8f0fc02f9f1822f1613ec2ce414716d2.png)*

*Photo by [israel palacio](https://unsplash.com/@othentikisra?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

***Express —** 用 JavaScript 编写的一个轻量级框架。有大量关于从哪里开始的教程和大量的例子。当试图连接到不同的数据源时，它非常灵活，并且对安全性等重要的事情有很多支持。*

***。这是微软支持的一项技术。这有点棘手，尤其是当你刚开始开发的时候。启动虚拟项目也很棘手。然而，如果你对编码有所了解，我建议你使用。NET 来构建 API，因为它更完整，允许更复杂的操作(然而，这些也可以在 Express 中重现)。***

> ***我的建议**:从快递开始。*

## *后端层*

*![](img/582c53bd3cc0ae51f2302bc4be64c86c.png)*

*Photo by [benjamin lehman](https://unsplash.com/@benjaminlehman?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*

***Postgres—**Postgres 是世界上最强大的开源数据库技术之一，开箱即用。它与 Express 和。NET 和任何其他集成框架。Postgres 强制实施关系数据结构，但是以后的版本也可以开始促进 NoSQL 结构。无论您是新手还是资深开发人员，我都会考虑使用 Postgres，而不是其他大多数数据库技术。*

***Firebase Firestore —** 谷歌来拯救。Firestore 是谷歌利用 NoSQL 数据库，但也提供整体云产品。Firestore 真的很容易设置，并附带了许多简单的教程来理解 NoSQL 的概念并开始使用(上面提到的许多技术)。如果你想快速入门，免费层是一个很好的起点。如果应用程序/网站开始运行良好，你的使用次数增加，请注意——众所周知，谷歌收费很高。*

***MongoDB**——MongoDB 也是一个 NoSQL 结构，是一个非常强大的免费后端数据库。理解事物是如何被托管的，数据库是如何构建的，以及在哪里容易看到数据，确实需要一些时间。一旦你掌握了窍门，它会变得非常强大。*

> ***我的建议:**尝试 Firestore，但选择 Postgres。*

> ***注:**文中使用了一点行话。如果你不确定某样东西是什么意思，或者想对提到的技术做更多的研究，请谷歌一下。这将有助于十倍完善搜索。*

*从头开始学习任何新技术总是具有挑战性。但是，如果你有了下一个伟大的想法，并正在考虑开始旅程，这一切都是值得的！*

*如果你正在和开发者交谈，并且需要一些帮助来理解他们在说什么或者他们在使用什么技术，请随意发表评论。我很乐意尽我所能提供任何建议。*

**更多内容请看*[*plain English . io*](http://plainenglish.io/)*