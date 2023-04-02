# 如何处理 Sequelize 中的数据库死锁

> 原文：<https://javascript.plainenglish.io/how-to-handle-database-deadlock-in-sequelize-6bee46e9ed99?source=collection_archive---------2----------------------->

![](img/8588ee72d1a48b3ea29a52ebe4ad5a86.png)

Photo by [Tim Gouw](https://unsplash.com/@punttim?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

欢迎来到另一个新故事。在这个故事中，我将分享我处理 [SQL 死锁](https://www.sentryone.com/sql-server/sql-deadlock)场景的经验。这个故事有四个部分:

*   您可能遇到的死锁情况的类型
*   解决僵局的方法
*   示例代码
*   一些帮助我解决问题的有用资源

**事不宜迟，我们开始吧**。

# 您可能遇到的死锁情况的类型

首先，在庞大而复杂的软件系统中，遇到数据库(DB)死锁是很常见的，尤其是当您的应用程序频繁更新相同的 DB 记录时。

我根据频率将死锁场景分为两种不同的类型:

*   每次在同一行代码出现**的死锁错误**
*   在同一行代码中偶然出现的死锁错误

# **解决僵局的方法**

**有两种方法可以解决死锁。**

*   ****确定死锁发生的位置并解决它**。这适用于第一种情况，因为每次都会发生死锁，所以您没有其他选择。通常，您可以在代码级别解决这个问题。**
*   ****死锁发生时的重试策略。**这适用于第二种情况，在这种情况下,**您几乎不知道它为什么会发生，并且具有不一致的发生模式**。最后但同样重要的是，这个场景也需要花费大量的时间和精力来调试。所以实施重试策略是最好的解决方法。**

**另外，根据 MySQL [文档](https://dev.mysql.com/doc/refman/8.0/en/innodb-deadlocks-handling.html)，**

> **[死锁](https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_deadlock)是事务数据库中的一个经典问题，但它们并不危险，除非它们非常频繁，以至于您根本无法运行某些事务。通常，您必须编写自己的应用程序，以便在事务因死锁而回滚时，它们总是准备好重新发出事务。— [MySQL 文档](https://dev.mysql.com/doc/refman/8.0/en/innodb-deadlocks-handling.html)**

**通俗地说，如果发生死锁，只需重试一次。在下一节，我将分享当死锁发生时如何在 Sequelize 中实现重试。**

# **Sequelize 中的示例代码**

**现在，我将使用[序列表单](https://sequelize.org/)设置重试策略。事实上，这很容易设置。在初始化序列库时定义重试策略。**

**下面是完整的代码。主要焦点是`retry`对象。`retry`对象是重试策略的配置。**

*   **`**match**`:由一组错误组成。如果匹配，数据库事务将再次重试，直到达到最大尝试次数。我使用 regex `/Deadlock/i`来确保事务只在死锁发生时重试。**
*   **`**max**`:最大重试次数。**
*   **`**backOffBase**`:初始退避持续时间。**
*   **`**backOffExponent**` **:** 每次重试退避增加的指数。**

# **其他有用的资源**

## **指数补偿计算器**

**您可以使用下面的指数补偿计算器获得更多信息以及每个信息之间的间隔。**

 **[## 指数补偿计算器

### 一个在线指数补偿计算器。输入间隔(秒)、最大重试次数和指数速率。想象一下…

exponentialbackoffcalculator.com](http://exponentialbackoffcalculator.com/)** 

## **承诺重试库**

**这是用来实现他们的重试策略的库序列。请参考 [**承诺重试**](https://www.npmjs.com/package/retry-as-promised) 了解您可以在`retry`对象中设置的所有配置。**

**最后但同样重要的是，Sequelize 中还有一个关于重试事务的很棒的帖子。请参考下面的链接。**

**[](https://dev.to/anonyma/how-to-retry-transactions-in-sequelize-5h5c) [## 如何在 Sequelize 中重试事务

### 您可能会得到类似“SequelizeDatabaseError:试图获取锁时发现死锁；尝试重新启动…

开发到](https://dev.to/anonyma/how-to-retry-transactions-in-sequelize-5h5c)** 

# **结论**

**在这个故事中，我分享了死锁场景的类型以及如何使用 Sequelize ORM 实现重试策略。**

**感谢阅读。**

***更多内容请看*[***plain English . io***](http://plainenglish.io/)**