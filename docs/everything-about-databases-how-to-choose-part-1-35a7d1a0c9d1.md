# 关于数据库的一切—第 1 部分:如何选择数据库？

> 原文：<https://javascript.plainenglish.io/everything-about-databases-how-to-choose-part-1-35a7d1a0c9d1?source=collection_archive---------12----------------------->

## 我们为什么需要数据库？

![](img/807a3a9bcc7f30e252ff3dbf4d8e6dd3.png)

Photo by [Jan Antonin Kolar](https://unsplash.com/@jankolar?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为什么不呢？在大多数项目中，我们使用数据库。本质上，为了保存任何数据，我们使用数据库。例如，为了让**注册**用户，我们必须将数据(用户的凭证)存储在某个地方。

其实不管是为了存储数据，**处理数据**，**人工智能**，**物联网**，你能想到的任何地方，开发者都在使用数据库。

## 最后，哪种数据库？

您有许多选择来选择数据库。这取决于你想存储什么和你的数据结构是什么样子。我们有两种类型的数据库， **SQL** 和 **NoSQL** (不只是 SQL)。在选择数据库之前，了解您的数据，提取您想要的结果，并了解您的操作符。

## 什么时候使用 SQL，什么时候使用 NoSQL？

如果你的数据非常结构化，使用 **SQL** ，如果不是，使用 **NoSQL** 。我再解释一下。

如果你需要在你的数据中有一个 **ACID** (原子性、一致性、隔离性、持久性)或者有**关系型**数据，最好选择 SQL。例如，假设你要在自动取款机上给别人转账。在这种数据中，交易是最重要的规则，因为你应该确保如果对方收到了钱，那么系统可以从第一方扣钱。

![](img/2fd8c9d156130e537f186c4aa59473f4.png)

正如我所说的，当你有像产品和类别这样的关系数据时，最好使用 SQL。例如，你正在创建一个**网店**，你有两个不同的类别，比如男人和女人，你的每个产品都与其中一个类别相关。看下面的表格。

如您所见，它们通过 category_id 相互连接，它们称之为外键，您可以通过 SQL 中的“join”命令创建一个关系。

这是一个学习如何创建连接的好例子，我推荐你看看这个链接:[**https://www.w3schools.com/sql/sql_join.asp**](https://www.w3schools.com/sql/sql_join.asp)

## SQL 数据库有多少种？

我们有很多数据库，如 **Mysql** 、 **Postgres** 、 **MSSQL** 、 **Oracle** 、 **MariaDB、**等。我们不能说哪一个比其他的好。在我看来，糟糕的开发会改变和影响最好的技术，让它变成最差的技术。所以不要花太多时间选择数据库。它们各有优缺点。我总是更喜欢 MySQL 或 Postgres(老实说，没有任何具体的原因)。正因为如此，我来解释这两个。在这里，我们将了解一些要点:

*   在阅读方面，MySQL 比 Postgres**快**。****
*   **MySQL 是最流行的 SQL 数据库。**
*   **Postgres 是一个面向对象的 T21 数据库。**
*   ****Postgres** 在写作上比 **MySQL** 快。**
*   **Postgres 是一个单线程数据库，但我的 MySQL 不是。**
*   ****Postgres** 在线管理面板是 **PgAdmin** 而对于 **MySQL** 是 **PHPMyAdmin****

**在本文中，我将继续讨论 Postgres。**

## **如何安装和使用 Postgres？**

**根据你的操作系统，有很多方法来安装它们。但是我推荐使用 docker 来运行它们。**

**此外，可以使用 docker-compose 一起运行 Postgres 和 PgAdmin**

**将其命名为 docker-compose.yml，然后通过 docker-compose 运行它**

```
docker-compose up -d
```

**太好了！现在，您已经使用 Postgres 和 pgAdmin 编辑了机器中的数据。在下一部分中，我将解释如何通过 Node.js 中的 [Sequelize](http://sequelize.org/) ORM 库连接到 Postgres。**

***更多内容请看*[*plain English . io*](http://plainenglish.io/)**