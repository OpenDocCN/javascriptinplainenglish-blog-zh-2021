# 面向前端开发人员的后端初学者入门

> 原文：<https://javascript.plainenglish.io/a-beginners-introduction-to-the-back-end-for-front-end-developers-c1c116014f64?source=collection_archive---------10----------------------->

## 全栈开发之旅。

![](img/1f3758de1912a03c8e393c2b763b4809.png)

Photo by [Grzegorz Walczak](https://unsplash.com/@grzegorzwalczak?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名前端开发人员，确定为后端使用哪种服务可能很困难。你们中的一些人会同意，不同服务的可用性使得找出最适合您的用例的服务变得更加困难，尤其是当您第一次尝试了解后端时。我想写这篇文章作为前端开发人员对后端的介绍，然后给出一些您可以在后端使用的解决方案的例子。

最简单地说，后端有两件事。一个存储数据的地方，一个访问数据的 API。作为一名前端工程师，你可能以前使用过 API。但是，在过渡到全栈模式的过程中，您必须在职业道路上建立自己的职业生涯。这就是这篇文章的由来。

首先，你需要一个数据库吗？我知道这听起来像是一个反问句。我知道您可能需要一个存储数据的地方，但这并不一定意味着您需要一个数据库。随着无代码或低代码工具的出现，您可能只需将数据放在 Google sheet 或 air table 中，然后使用自动生成的某种服务或 API 来获取这些数据就可以了。我的意思是，您的数据可以与代码共存吗？您可以将文件作为工作流的一部分提交到 get 存储库中吗？是的，你可以。您也许可以使用类似 markdown 的东西来存储您的文件，并在构建过程中呈现它们。

回到对数据库的需求，假设您确实需要一个数据库。有几个术语或事物你可能需要熟悉。在进入这篇文章的核心之前，我将快速浏览一下。

# 1.SQL 与非 SQL

最常用的两种数据库是 SQL 和非 SQL 数据库。如果你还不熟悉这些术语，我会给你一个简单的分类。SQL 数据库开始用于关系数据。考虑像 Medium 这样的博客平台。您可能有一个用户和帖子的表，这两个表之间存在关系。对于每个用户，您可能有许多不同的帖子，但是每个帖子只有一个用户。然后，这些关系使得通过查询查找数据的不同部分变得容易，为此您使用 SQL。

非 SQL 数据库通常是面向文档的。您拥有的不是表和行，而是文档和集合。例如，在 MongoDB 中，您有一个文档集合，每个文档都有一组包含一些数据的键值对。如果您有大量的集合要与小文档一起存储，这是一个很好的方法。你可能也听说过 GraphQL 和 Rest。这只是获取数据的两种不同方式。

# 2.认证和授权

身份验证验证我们的用户是谁，而授权控制他们拥有的访问类型。如果您正在构建任何具有用户管理特性的应用程序，您将需要了解更多关于这两个特性的知识。这种应用的好例子是博客平台、会员网站、电影流媒体平台，基本上是任何有用户的应用。

# 3.托管与自托管

如果您的数据库是托管的，这意味着它是由别人管理的。如果您是自托管的，这意味着您自己管理基础架构。一般来说，如果一个后端服务是开源的，有一些方法允许你自己托管它。对于前端开发人员，我可能会建议坚持使用托管服务，因为您需要担心或设置的基础架构较少。以这种方式起步并开始编码更容易。这类似于无服务器。

传统服务器一直在运行。在无服务器的情况下，只有当你在它们上面执行某些操作时，它们才会运行。这样，它们就具有成本效益。请记住，有权衡，但这是一个相当高层次的概述。作为一名前端工程师，您可能完全使用无服务器就可以了。

# 4.数据建模和数据规范化

数据建模是您可能需要熟悉的另一个术语。简而言之，数据建模描述了允许您在数据库中组织数据的方法。您可能还会看到数据库规范化，这是将数据组织到表和列中的方式。

现在我已经了解了基本术语，我希望您在决定特定的后端之前考虑一下抽象的层次。您希望在多大程度上控制该基础架构？你会自己开发后端吗？您是否正在尝试推出 SAS 产品？思考这些问题很重要，因为每种情况都是独特的，有多个提供者在做同样的事情。

如果你正在为自己构建一个项目或一个小型的 SAS 应用程序，我建议尝试一些新的东西，尝试一点点，因为你有这种奢侈和自由。如果你正在为你的日常工作做一些事情，你可能应该使用在行业中更好地被采用并且有更广泛的社区支持的东西。如果你需要快速的东西，那通常是你选择更高抽象层次的时候。那是什么意思？这意味着您不必为部分后端编写代码，因为有一些服务提供现成的代码。这意味着他们将负责自动生成 API，从而提供这种抽象，这样您自己就不必担心了。

假设你想要更高层次的东西，作为一个前端工程师你可能会这么做。我将触及一些更高层次的障碍，但首先，一些问题要考虑，你的后端需要建立在开源技术上吗？需要像 Google 或者 get hub 一样支持社交登录吗？您有现有的数据库吗？你正在寻找完全管理的东西吗？这些问题将有助于缩小我要调查的供应商的范围。

# 后端即服务

这是最高层次的抽象。通常，您将提供您的模式、设置您的表、进行您的数据建模，然后这些服务将为您自动生成代码的重要部分。这些解决方案包括:Firebase，MongoDB，Hasura，你懂的。我只看几个。让我们从 Firebase 开始。

Firebase 很棒。它拥有出色的开发者体验，如果你想快速构建一个应用，并且需要像 Google 或 GitHub 那样的社交登录，我会推荐它。你必须愿意牺牲一点灵活性，因为对于你的产品投入使用的时间来说，它不是开源的。值得一提的是，Firebase，特别是 Firestore 和如何存储数据，是一个非 SQL 数据库。如果您已经熟悉了 SQL，也许您已经熟悉了，那么您可能不想使用这种方法。

服务的第二个后端叫做 Hasura，它在一个盒子里提供了一个 graphQL API。使用他们的托管平台，您可以进入并使用 UI 来构建您的整个模式，然后它会自动为您更新所有 crud 操作，这样您就不必自己编写任何代码。如果你想使用 graphQL，你可以使用 Hasura。无论您喜欢这项技术，还是希望通过远程模式扩展现有模式，我都推荐使用 Hasura cloud。

# CMSs

CMS 代表内容管理系统。为了理解什么时候应该使用它们，你需要考虑几个问题。您正在处理图像还是文档存储？需要本地化数据吗？你想在帖子发布前预览吗？有了这样的用例，你可能会从 WordPress 开始。有了 WordPress，你就有了访问数据的 API。此外，它附带了 UI 来管理捆绑在一个应用程序中的数据，而不是 headless CMS，因为数据部分和管理部分之间是分离的。

无头 CMS 将提供允许您更新或管理该内容的 API，此外还有一个 web 应用程序，您的非技术用户可以在其中修改和更新数据，并有权访问该数据。这对于将这两部分的关注点分开来说是非常好的。过去，WordPress 存在一些安全漏洞，当存在紧密耦合时会暴露特定版本，这是人们转向无头 CMSs 的部分原因。此外，它们与大多数前端开发人员正在向的 JAMstack 范式更好地保持一致。

# 构建您的后端

您可以使用一些工具来简化这个过程。然而，它们要求你自己编写更多的代码。我不会向绝对的初学者推荐这些，但是当你通过初级阶段进入中级阶段时，你可以通过更裸机的方法学习很多东西，并了解其中一些东西是如何工作的。我通过做和建造东西学得最好，这是我对每个问我这方面问题的人的建议。

我认为您可能会考虑的三个服务是 AWS、Dynamo DB 和 Prisma。Prisma 很酷的一点是，你可以带来你的数据库或者创建一个新的数据库，它允许你对现有的数据库模式进行类型安全的访问。因此，无论你是使用 Postgres 还是任何基于 SQL 的数据库，Prisma 都能让你轻松访问和修改数据库中的数据。

如果你将使用 Prisma 并构建你自己的，你可能也将是自托管的。据我所知，没有“盒子里的 Prisma 解决方案”，这意味着您将在 AWS 或 DigitalOcean 等地方部署数据库和 API。

# 从头开始

这通常是更有经验的后端或全栈开发人员的归宿，因为他们希望完全控制后端和基础架构的每一部分。事实上，有完整的视频和课程致力于此。在这篇小文章中写他的水平是有害的，因为它包含了很多东西。这是一篇面向初学者和中间用户的文章，我相信我已经涵盖了大部分问题。

希望您现在对如何进入后端有了更好的理解。这更像是成为全栈开发人员的一个途径。它不会在一夜之间到来。和生活中的一切一样，这也需要你付出一些汗水。一步一步来，你很快就会成功。干杯。

*更多内容看*[***plain English . io***](http://plainenglish.io/)