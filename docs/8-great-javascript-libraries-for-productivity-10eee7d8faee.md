# 提高生产力的 10 大 JavaScript 库

> 原文：<https://javascript.plainenglish.io/8-great-javascript-libraries-for-productivity-10eee7d8faee?source=collection_archive---------15----------------------->

用几行代码提高您的工作效率！

![](img/075b82e35d8e54dfb02a74c4a9966558.png)

Photo by [Jexo](https://unsplash.com/@jexo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Javascript 已经存在很长时间了。从一开始，它就演变成了一种你可以做任何事情的语言。如今，我们创建了服务器端代码、前端代码、移动应用程序代码等等。

许多这些不同的利基市场可以以这样或那样的方式使用 NPM。**而且大多数包甚至可以在没有任何包管理器的情况下使用**。这里是我以前在不同项目中使用过的一些很棒的库的一个小列表。

# Nodemon

[Nodemon](https://www.npmjs.com/package/nodemon) 是一个可以帮助服务器开发的库。当任何更改被保存后，它会自动重启你的服务器(或其他项目)。

它足够聪明，知道你什么时候保存前端文件，如 CSS，或者如果你更新后端文件，需要重新启动。它只会在需要时尝试重新启动。

有时，刷新浏览器就足以看到应用于项目的更改。在这种情况下，Nodemon 很可能不会重启您的项目。

它的易于安装性和在项目过程中节省的时间使它成为每个项目的必备工具。

# UUID

UUID 是一种独特的识别标准，可用于多种数据库和其他语言。PostgreSQL 甚至有一个 UUID 类型，您可以使用它作为 ID。它增加了不可猜测的安全性。

它很容易使用，每次我需要数据库的唯一值时都会使用它。图书馆的 ID 符合 UUID 标准。

# Axios

[Axios](https://github.com/axios/axios) 是所有 HTTP 请求问题的解决方案。它是一个基于 promise 的 HTTP 客户端，简化了从 API 请求数据的过程。

您可以根据需要输入尽可能少的信息，也可以根据需要输入尽可能多的信息。每当我不需要添加参数时，我喜欢省略它们，在 Axios 中这是可能的。

# 洛达什

Lodash 是一个实用程序库，提供了大量处理字符串、数字、数组和对象的函数。*我最近写了一篇关于这个库的博文，你可以在这里找到*[](https://medium.com/codex/introduction-to-lodash-one-of-the-greatest-utility-libraries-6f28fcd5a3a6)*。这是一个很棒的库，因为它有大量的函数和一个惊人的文档站点。*

***我强烈建议至少查看一下这个库及其文档**。它有针对高度特殊问题的函数，也有很多针对常见问题的函数，比如展平数组。*

# *国际光子*

*Luxon 是一个现代的日期和时间操作库。如果你曾经处理过日期和时间，你会知道使用一个合适的库是成功的一半。尤其是当你被多个时区所困扰的时候。*

*在某种意义上，Luxon 是 Moment 的更年轻、更现代的版本，Moment 是另一个著名的日期和时间操作库。然而 **Luxon 使用** `**Intl**` **对象，而 Moment 使用** `**Date**` **对象**。*

# *骗子*

*Faker 是我在构建项目的早期测试阶段使用的一个库。它是一个库，可以方便地将真实的测试数据添加到应用程序中。*

*Faker 的优势肯定在于你可以添加的不同数据的数量。所有数据仅用于测试目的，不应用于生产。你可以添加各种地址、邮件、姓名、**甚至比特币地址**和车辆制造商！*

*如果你厌倦了到处看到 Lorem Ipsum，你可能想看看这个。*

# *Dotenv*

*Dotenv 是一个库，用来确保你的应用程序是安全的。提高安全性的一种方法是使用环境变量。这就是这个库的用途，也是使用最多的库之一。*

*您可以用应用程序的所有环境变量创建一个`.dotenv`文件。确保永远不要提交这些，因为它们应该是特定于环境的，或者只在一台 PC 上工作以获得最大的安全性。*

# *猫鼬*

*当您使用 MongoDB 数据库时，mongose 是一个很好的库。这是一个对象建模库，使使用 Mongo 和 Javascript 变得尽可能容易。*

*几乎所有的 Mongo 和 Javascript 教程都以这个库为特色，而不是默认的 MongoDB 库，因为它很简单，大多数开发人员都离不开它。*

# *领域*

*Realm 在用于数据库开发的形式上类似于 Mongoose。我只在手机应用程序开发中使用过 Realm，一旦它被设置好，它就像一个魔咒一样工作。*

*对于 React 原生开发来说，没有太多真正好的数据库选项，我认为 Realm 肯定能在一定程度上填补这个角色。它的数据库非常类似于 Mongoose，我认为它运行在 MongoDB 上。*

# *盖茨比*

*[Gatsby](https://www.gatsbyjs.com/) 是一个静态的服务器渲染的网站库。它类似于 NextJS，虽然它目前缺乏一些功能，但我认为开发人员的体验优于我尝试过的任何东西。*

*它使用 React 和 GraphQL 为中小型网站创建了一个非常好的技术栈。它对从营销到博客的任何事情都有好处。*

# *结论*

*这些只是我过去用过的一些库。作为一名开发人员，您可能每天都会遇到新的库，并且很容易过度使用它。*

*我喜欢使用尽可能少的库，我只使用较大的库或适用于某些问题的库。*

*非常感谢您的阅读，祝您度过美好的一天。*

**更多内容尽在*[***plain English . io***](http://plainenglish.io/)*