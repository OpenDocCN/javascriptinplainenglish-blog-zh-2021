# 如何用 Node.js 构建 Google Firestore 的数据库助手类

> 原文：<https://javascript.plainenglish.io/how-to-build-a-database-helper-class-for-google-firestore-with-node-js-1e0c4a8e168a?source=collection_archive---------1----------------------->

![](img/c5da1683fabb3cb32d7e974bcc726739.png)

抽象数据库操作可能具有挑战性。

我想分享我构建的数据库助手类，以便在 Node.js API 中与 Google Firestore 交互。

以下示例假设您已经安装并连接了 Firestore。

**不带类的初始设置**

如果我们以此作为管理数据库中用户的初始设置，那么一切都会很好。

理想情况下，我们需要一个支持以下内容的类:

1.  任何集合的可重用数据库功能。
2.  类型安全。
3.  一次只允许使用一个数据库连接。

我们最重要的目标是减少在应用程序的其他部分实现类似交互所需的重复代码。

我将在下面提供完整的示例类，然后是初始设置的更新版本。

**数据库类助手**

上面的类抽象了我的应用程序需要的所有数据库交互。Typescript 泛型和联合类型有助于使函数尽可能安全。

这个类也遵循单例设计模式，这意味着一次只能使用一个数据库连接。

如果需要进行独特的数据库交互，我们可以使用`db`变量与 firestore 进行交互，就像我们之前所做的那样。

**更新数据库功能**

有了这个类，您可以减少应用程序中样板文件的数量，而不会牺牲启用定制函数的能力。

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。****