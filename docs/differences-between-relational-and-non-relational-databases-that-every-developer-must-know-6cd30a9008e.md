# 每个开发人员都必须知道的关系数据库和非关系数据库之间的区别

> 原文：<https://javascript.plainenglish.io/differences-between-relational-and-non-relational-databases-that-every-developer-must-know-6cd30a9008e?source=collection_archive---------5----------------------->

## 你应该为你的应用选择哪一个？

![](img/9ee10d34aec537faf5a52cc8a4455ca5.png)

Photo by [Tobias Fischer](https://unsplash.com/@tofi?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/database?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当我们谈到数据库时，脑海中会浮现出什么？存储文件的安全位置，以后可以根据需要访问这些文件。是的，数据库就是这样。Oracle 将数据库定义为通常以电子方式存储在计算机系统中的结构化信息或数据的有序集合。

通常，数据库系统中的数据被组织成表格、行和列。这些数据库也称为关系数据库。然而，当非 SQL 数据库在 21 世纪开始流行时，数据库的定义略有变化。非 SQL 数据库是一种存储和检索不由表格关系表示的数据的系统。

这就是为一个项目从这么多可供选择的数据库中选择一个数据库的难题所在。当然，答案与你将要从事的项目类型成正比。

但首先，我将尝试简单解释一下这两个数据库。

# 关系数据库

关系数据库，也称为关系数据库管理系统(RDBMS)或 **SQL 数据库**，以形成表格的行和列的形式保存数据，表格通过“*键*”或两种关系共享的信息相互关联。在关系数据库中，表中的一行被称为'*记录'*，表被称为'*关系【T9]. '*

它主要用于管理结构化数据，其中数据的各种实体和变量之间存在关系。

![](img/f506b2364e53f287747fe90df9feab05.png)

Photo by [Waldemar Brandt](https://unsplash.com/@waldemarbrandt67w?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/locker?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 优势

*   所有 RDBMS 都使用单一的标准语言。
*   它有一个预定义的模式，在许多用例中都很有用。
*   使用单一的统一语言(DDL)定义不同的职责，如开发人员、用户、DBA 等。
*   它遵循 ACID 原则(*原子性、一致性、隔离性和持久性*)，确保数据库和每个事务的整体稳定性、安全性和可预测性。
*   它在获取数据库记录时有着无与伦比的速度。

## 不足之处

*   它有一个复杂的互动程序。
*   当数据库变大时，很难对其进行扩展。
*   处理大数据的成本非常高，因为需要升级硬件来实现扩展。
*   它不支持 blobs 数据，如文件或图像。

## 关系数据库的一些例子

*   *甲骨文*
*   *微软 SQL server*
*   *PostgreSQL*
*   *MySQL*

# 非关系数据库

非关系数据库，也称为 **NoSQL 数据库**，提供了一种存储和检索非结构化数据或数据的机制，这些数据不像 SQL 数据库那样以表格关系表示。由于 NoSQL 数据库是为了解决 SQL 数据库的可伸缩性问题而设计的，所以它们是无模式的，并且基于分布式系统，这使得它们更容易伸缩和[分片](https://en.wikipedia.org/wiki/Shard_(database_architecture))。

它越来越受欢迎，因为它是大数据和实时应用程序的首选。因为它是无模式的，所以在创建 NoSQL 数据库之前要仔细设计数据结构。这使得它具有高度的可扩展性和灵活性，可以处理各种数据模型。

![](img/b2e1872b610e1489863213926063a78e.png)

Photo by [Pixabay](https://www.pexels.com/@pixabay?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/time-lapse-photography-of-blue-lights-373543/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

## 优势

*   它能够处理大数据。
*   它是无模式的，这使得它可以灵活地使用任何数据模型。
*   它构建在分布式系统上，可扩展性成本低，因为它不需要额外的硬件来扩展。
*   它不支持 blobs 数据，如文件或图像。
*   由于它们的低成本和高可伸缩性，小型企业使用它们。

## 不足之处

*   NoSQL 的优势是以宽松的酸性特征为代价的。因此，NoSQL 只能保证最终的一致性，这可能会导致数据丢失。
*   与 SQL 数据库相比，它没有一个成熟的社区。
*   由于没有类似 SQL 的标准语言，学习不同 no SQL 数据库的 API 很困难。

## 不同类型&非关系数据库的一些例子

非关系数据库被分为四类:

1.  **列:**这些数据库类似于关系数据库，除了它们是以列而不是行存储和排列的宽列数据表。这些数据库可以比关系数据库更快地查询大量数据。例子: *Cassandra，Google BigTable 等。*
2.  文档:这些数据库将数据存储为文档，如 JSON、YAML 或 XML。每个文档都使用一个唯一的键来寻址。这些数据库还提供了一个 API 和查询语言，用于根据内容检索文档。例子: *MongoDB，CouchDB 等。*
3.  **键-值:**这些数据库将数据存储为字典或散列，其中键是字符串，值可以是字符串、数组、集合等。例子: *Redis，DynamoDB 等。*
4.  **图形:**这些数据库以创建图形的节点和边的形式存储数据。实体由节点表示，而实体之间的关系由边表示。例子: *AllegroGraph，Titan 等。*

# 哪个数据库比较好？

如果您正在开发一个将管理大量结构化、半结构化和非结构化数据的应用程序，并且该应用程序的主要优先级是可伸缩性和性能，那么应该使用 *NoSQL 数据库*。

如果您希望您的数据事务是持久的和高度安全的，并且您希望存储大量的结构化数据，并且还希望使用 SQL 来使用复杂的查询来检索信息，那么应该使用一个 *SQL 数据库。*

*如果你喜欢读这篇文章，你可能也会发现下面的文章值得你花时间去读。*

[](https://blog.devgenius.io/5-superb-github-repos-that-every-java-developer-must-know-about-29402a5072f1) [## 每个 Java 开发人员都必须知道的 5 个极好的 GitHub Repos

### 关于高性能、广泛使用、企业首选的编程语言的一切。

blog.devgenius.io](https://blog.devgenius.io/5-superb-github-repos-that-every-java-developer-must-know-about-29402a5072f1) [](https://blog.devgenius.io/7-insanely-bizarre-programming-languages-that-exist-in-the-world-b25fc847e47) [## 世界上存在的 7 种疯狂怪异的编程语言

### 这个列表包含了有史以来最不实用的编程语言。

blog.devgenius.io](https://blog.devgenius.io/7-insanely-bizarre-programming-languages-that-exist-in-the-world-b25fc847e47) 

您可能还会找到下面的目录，来自*The practical Programmer*，他们在那里出版了"*关于经典和前沿主题的实用书籍和学习资源，以帮助您实践您的技能并加速您的职业生涯。*”

 [## 媒体实用程序员书籍目录

medium.com](https://medium.com/pragmatic-programmers/directory-of-pragmatic-programmer-books-on-medium-6a5cbadbd4b4) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)