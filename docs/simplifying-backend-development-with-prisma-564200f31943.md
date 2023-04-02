# 使用 Prisma 简化后端开发

> 原文：<https://javascript.plainenglish.io/simplifying-backend-development-with-prisma-564200f31943?source=collection_archive---------7----------------------->

![](img/8c7e59fc24702e0137d8f8ec9caefa60.png)

Photo by [Peter Gombos](https://unsplash.com/@pepegombos?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@pepegombos?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

如果您是在 Node.js 生态系统中工作的后端或全栈开发人员，您可能使用过不同的数据库访问工具。

如果您正在使用 MySQL 之类的 SQL 数据库，您可能会熟悉 [*ORM* (对象关系映射器)](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping)库，如 [Sequelize](https://sequelize.org/) 、 [Typeorm](https://typeorm.io/) 、*查询构建器*如 [Knex](http://knexjs.org/) 或本地数据库驱动程序如 [mysql](https://github.com/mysqljs/mysql) ，它们将有助于*编写原始 SQL 查询*。

这些工具或方法各有利弊。

我发现在这些工具中, [Prisma](https://www.prisma.io/?utm_source=Prisma%20Ambassador&utm_medium=Blog%20post&utm_campaign=Prisma%20AP%20Pasindu%20Dilshan) 对开发者更友好。

在这篇文章中，我将向初学者介绍 Prisma，并让您了解我们如何开发灵活且可伸缩的后端。

# Prisma 是什么？

> **Prisma 是开源的下一代 ORM，可以让你轻松管理&与数据库的交互。**

![](img/b3d6f036a51983409b020b77e7e1abe8.png)

Visit [Prisma.io](https://www.prisma.io/?utm_source=Prisma%20Ambassador&utm_medium=Blog%20post&utm_campaign=Prisma%20AP%20Pasindu%20Dilshan)

当前的 Prisma 版本由 3 个主要部分组成

1.  Prisma Migrate:一个必要的数据库模式迁移工具。
2.  Prisma Client:一个自动生成的类型安全的查询生成器。
3.  Prisma Studio:数据库数据的可视化编辑器。

没有进一步的解释，让我们开始构建一些东西，这样 Prisma 背后的想法将更加明显。

# 让我们开始吧

我们将考虑一个非常基本的博客文章场景，其中用户创建了一篇博客文章。

![](img/a17a2255fedaede9f79c1d36e10fc812.png)

Entity Relationship Diagram (ERD)

*   为了简单起见，只有两个实体:用户和帖子。
*   所有数据都将存储在 MySQL 数据库中。
*   为了简单起见，也放弃了诸如认证之类的特性。

最后将构建一个用于数据库查询的最小类型脚本。

如果你需要在你的开发环境中设置 MySQL 的指南，请查看 Prisma 的数据指南。

[](https://www.prisma.io/dataguide/mysql/5-ways-to-host-mysql) [## 托管 MySQL 数据库的 5 种方法| Prisma 的数据指南

### 有很多方法可以让 MySQL 服务器为您的项目运行。您可以安装和管理一个…

www.prisma.io](https://www.prisma.io/dataguide/mysql/5-ways-to-host-mysql) 

您在这里找到的所有代码都可以在下面的库中找到。对于本文中涉及的每个主题，它都分为不同的分支。

[](https://github.com/Pasi-D/Prisma-Starter) [## PASI-D/Prisma-启动器

### 一个简单的项目旨在展示使用 Prisma ◭先决条件的简单性，如果你没有安装节点…

github.com](https://github.com/Pasi-D/Prisma-Starter) 

我们将从一个简单的 Typescript 脚本开始&首先安装 Prisma。你可以在[***0-Initial-Script***](https://github.com/Pasi-D/Prisma-Starter/tree/0-Initial-Script)分支中找到起始代码。

# 1.设置 Prisma

首先，我们需要安装 Prisma 作为开发依赖项，这样我们就可以在项目中使用 Prisma CLI 命令。

```
$ npm install prisma --save-dev
```

您现在可以在目录中调用 Prisma CLI，方法是在它前面加上 [*npx*](https://docs.npmjs.com/cli/v7/commands/npx) 。让我们用下面的命令初始化 Prisma 模式文件。

```
$ npx prisma init
```

![](img/04da5e89f96b0d43eaae5ca5829cbb80.png)

这将创建一个带有***schema . Prisma***文件和*的 Prisma 目录。env* 文件。

你可以移动这个*。env* 文件到根目录，即与 *package.json* 相同的级别。

## 等等，什么是 Prisma 模式？

> risma 模式是 Prisma 设置中的主要配置文件。它是数据库模式和应用程序模型的真实来源。

您可以使用 Prisma 模式，

*   生成正确的数据源客户端代码(Prisma 客户端)。这充当了数据的查询构建器。
*   生成迁移以更新数据库模式。

![](img/5522b04d4316e7cc66971ff687e32ae1.png)

How our Prisma.schema will look like in the end

Prisma 模式由以下部分组成

1.  数据源:定义与数据源的连接。
2.  生成器:根据数据模型定义客户端需要生成的内容。
3.  数据模型定义:您的应用模型

*生成的默认模式使用 PostgreSQL 作为* ***提供者*** *。所以，要做的第一件事是切换到“mysql”。*

```
datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}
```

为了连接到我们的数据库， ***url*** 字段需要更改。你可以[将其设置为一个环境变量](https://www.prisma.io/docs/concepts/more/environment-variables)，而不是硬编码。

这需要以下面的通用格式来指定。

```
DATABASE_URL=mysql://USER:PASSWORD@HOST:PORT/DATABASE
```

# 2.使用迁移创建数据库模式

> **使用**[**Prisma Migrate**](https://www.prisma.io/docs/concepts/components/prisma-migrate/)**您可以使您的 Prisma 模式与您的数据库模式保持同步。它还可以帮助您维护数据库中的现有数据。**

让我们开始改变 Prisma 模式以适应我们的场景。我们可以开始编写我们的数据模型。

```
model User {
  id        Int     @id @default(autoincrement()) 
  username  String  @unique 
  email     String  @unique 
  posts     Post[] 
}model Post { 
  id        Int     @id @default(autoincrement()) 
  title     String 
  content   String? 
  authorId  Int 
  author    User?   @relation(fields: [authorId], references: [id]) 
}
```

如果这个模型看起来有点乏味&很难理解它将如何映射到我们的数据库模式，下面的可视化表示将会帮助你。

![](img/62988b56ae7be0af6a0193e1702692e5.png)

Mapping between Prisma Schema & Database Entities(Tables)

我们的 Prisma 模式有几个属性来表示表字段应该是什么样子。

*   @id —主键
*   @unique —唯一键
*   @default —默认值
*   @relation —两个表之间的关系

您可以在 Prisma 模式参考的[属性部分找到更多详细信息。](https://www.prisma.io/docs/reference/api-reference/prisma-schema-reference/#attributes)

为了产生迁移，

```
$ npx prisma migrate dev --name init
```

这份遗嘱，

1.  为此迁移生成 SQL 迁移文件。
2.  对数据库运行生成的迁移文件。
3.  生成 Prisma 客户端，如果不可用，在 *package.json* 依赖列表中更新。

如果您需要对数据库模式进行更改，您只需对 Prisma 模式进行相应的更改，然后运行 Prisma migration 命令。

如果你使用过 [TypeORM](https://typeorm.io/) ，这个过程可能会很熟悉。TypeORM 还可以根据您所做的模式更改自动生成迁移文件。不同之处在于，在 TypeORM 中，你需要管理单独的模型文件，这些文件与迁移文件相映射。使用 Prisma，您只需修改 Prisma 模式文件中的模型。

![](img/418040c77e2316efcb0772de600930aa.png)

Comparison between Prisma & Other ORMs in terms of Migration

我们将在以后的文章中更深入地探讨使用 Prisma 进行数据库迁移。

Prisma 还有几个改变游戏规则的人🚀

# 3.数据库自省

> **Prisma 能够为现有的数据库模式生成 Prisma 模式的数据模型。这是用** [**自省**](https://www.prisma.io/docs/concepts/components/introspection) **完成的。**

假设您不想使用 Prisma 迁移&您正在使用普通 SQL 或任何其他迁移工具进行迁移。使用 Prisma，您可以重新检查您的数据库并重新生成 Prisma 模式，然后在您的 Prisma 客户端中反映这些变化(我们将在前面看到)。

![](img/25aa84f15879d7778ce6e17e5f735572.png)

[If for some reasons, you can not or do not want to use Prisma Migrate, you can still use introspection to update your Prisma schema from your database schema.](https://www.prisma.io/docs/concepts/overview/what-is-prisma#sql-migrations-and-introspection)

> 通过这种方式，你可以逐步将 Prisma 应用到现有的应用程序中，而无需做出巨大的妥协。

# 4.Prisma 客户端

> [**Prisma 客户端**](https://www.prisma.io/docs/concepts/components/prisma-client) **在编写您的应用程序逻辑中起着关键作用。这是一个自动生成的类型安全查询生成器。**

如果 Prisma client 不在你的 package.json 依赖列表中，最好安装 *@prisma/client* 包作为依赖。

```
npm install @prisma/client
```

每当 prisma 模式被修改时，您需要调用***Prisma generate***来反映您的 Prisma 客户端中的那些变化。

让我们在 ***app.ts*** 中进行数据查询的修改。

*(附言:在你的控制台* ***npm 运行*** *将运行脚本)*

首先，您需要导入生成的 Prisma 客户端并创建一个 Prisma 对象。

```
import { PrismaClient } from "@prisma/client";const prisma = new PrismaClient();
```

创建用户记录

If your IDE has **IntelliSense,** code completion will be there.

![](img/6012839ee856ac82662ed86d4c3446f5.png)

All types are auto-generated based on the shape of model(s).

要创建多个帖子

创建具有帖子的用户

Its really easy to interpret & understand this query as you write the code.

查询所有用户。

通过电子邮件找到用户，但只需要用户名和文章标题。

There is 100% type-safety in using Prisma client. This is awesome for developer experience 😀

> 因为类型是基于我们在 Prisma schema 中定义的数据模型自动生成的，所以从编写应用程序逻辑到管理代码库的每个方面都变得容易得多。我们根本不需要编写任何样板代码。

# 5.种子数据

在某些情况下，一旦我们创建了数据库模式，我们就需要用要处理的记录更新一些数据库表。要做到这一点，我们可以播种我们的数据库。
Prisma 具有集成的播种功能。

![](img/f4016747df876bedc01f2c485cff1085.png)

Prisma db seed is still in preview

[目前](https://github.com/prisma/prisma/releases/tag/2.25.0)，这仍然是一个预览功能&，不建议在生产环境中使用。

这将在即将发布的 Prisma 版本中完全可用。

现在要做的是，首先我们需要[*ts-node*](https://www.npmjs.com/package/ts-node)&[节点类型](https://www.npmjs.com/package/@types/node)作为 dev 依赖项。

```
npm install ts-node @types/node --save-dev
```

我们需要如下修改 package.json 脚本。

种子文件需要与 Prisma 架构文件位于同一位置。下面给出一个例子。

为了播种这些数据，

```
$ npx prisma db seed — preview-feature
```

# 6.Prisma 工作室

![](img/918eda20950e6fdeda295365cd567160.png)

Data stored can be visualized with Prisma Studio

Prisma studio 是数据库中数据的可视化工作室。

你可以运行它，

```
$ npx prisma studio
```

通过这种方式，你可能不需要集成一个数据库管理工具，例如 [phpMyAdmin](https://www.phpmyadmin.net/) 来可视化你的数据。

# 结论

Prisma 有很多 ORM 的特性，这无疑让开发人员的生活变得更加轻松。

除了我们已经讨论过的，还有许多更强大的特性将会在未来加入。对 MongoDB & SQL Server 的支持，模式可视化只是其中的一小部分。您可以在 [Prisma Roadmap](https://www.notion.so/prismaio/Prisma-Roadmap-50766227b779464ab98899accb98295f) 查看未来计划。Prisma 还拥有来自全球各地的蓬勃发展的开发人员社区。

希望这篇文章能帮助你理解 Prisma 的基本流程&为什么它是后端开发的一个如此强大的工具。如果您有任何问题或反馈，请在下面评论。

感谢阅读！

*更多内容看*[***plain English . io***](http://plainenglish.io)