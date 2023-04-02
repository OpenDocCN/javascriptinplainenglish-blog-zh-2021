# 如何在 NestJS 中执行原始 PostgreSQL 查询

> 原文：<https://javascript.plainenglish.io/how-to-execute-raw-postgresql-queries-in-nestjs-1967a0cb950b?source=collection_archive---------1----------------------->

![](img/ff755726e98754f2ff5e657b5fff5e91.png)

Photo by [Caspar Camille Rubin](https://unsplash.com/@casparrubin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

[正式的 NestJS 文档](https://docs.nestjs.com/techniques/database)有很多例子展示了如何使用 ORM 框架，比如 [TypeORM](https://typeorm.io/) 与数据库集成。但是，如果您不想使用 ORM，而是希望在没有 ORM 开销的情况下对数据库执行原始查询，该怎么办？

本教程将为您提供一个如何做到这一点的示例。在本教程中，我们将编写一个模块，负责在 PostgreSQL 数据库上执行 SQL 查询。

# 所需依赖项

为此，我们需要安装一个库，它将允许我们与 PostgreSQL 数据库接口。 [node-postgres](https://node-postgres.com/) 是事实上的标准库，所以让我们安装它:

```
npm install pg
```

由于 NestJS 使用 TypeScript，我们还可以为节点后缀安装 TypeScript 定义:

```
npm install @types/pg --save-dev
```

# 配置文件

数据库配置通常存储在外部配置文件中，对于不同的环境，您通常会有不同的文件。出于本教程的目的，我们将把我们的数据库设置存储在一个简单的`.env`文件中:

Sample .env file

如果我们使用 NestJS 的内置`ConfigModule`的话，读取这个文件应该不成问题。我们将在我们的`AppModule`导入该模块，并使其全球化:

Configuration of the ConfigModule in the root AppModule. Note the *isGlobal* and *envFilePath* properties.

[使模块全局化](https://docs.nestjs.com/modules#global-modules)并不常见，除非您真的计划在大多数应用程序模块中使用它们。阅读配置是一项常见任务，因此使`ConfigModule`全球化是有意义的。这样，我们不必在每个应用程序模块中显式导入它。另一个配置属性`envFilePath`，是我们的`.env`文件的路径。

配置并导入`ConfigModule`后，我们现在可以在整个应用程序中使用`ConfigService`从我们的配置文件中检索值。例如，在我们的情况下，`configService.get('POSTGRES_USER')`将返回`my-user`。

# 数据库模块

现在，让我们创建一个专用模块，它将是我们数据库集成功能的容器。

Empty DatabaseModule

该模块的目的是连接到数据库，并公开一个在数据库上执行查询的服务。

从 NestJS 应用程序连接到数据库的推荐方式是通过[数据库池](https://node-postgres.com/features/pooling)。数据库池只是一个 node-postgres 对象，负责管理到 PostgreSQL 数据库的连接。

由于我们将把这个池注入到我们的数据库服务中，我们可以使用一个[工厂提供者](https://docs.nestjs.com/fundamentals/custom-providers#factory-providers-usefactory)来创建它。工厂提供者允许我们使用依赖注入来注入其他提供者，比如`ConfigService`。

Creating a Pool instance using a factory provider

在上面的代码片段中，我们在模块的`providers`数组中定义了我们的提供者，将其命名为`DATABASE_POOL`，并告诉 NestJS 向我们的工厂注入一个`ConfigService`实例，这样我们就可以用来自`.env`文件的配置来初始化池对象。

现在让我们创建一个用于执行查询的数据库服务。`executeQuery`方法现在是空白的，我们将名为`DATABASE_POOL`的池对象注入到服务中。我们还创建了一个 [NestJS logger](https://docs.nestjs.com/techniques/logger#using-the-logger-for-application-logging) 的实例，这样我们就可以在数据库查询发生时记录它们。

Injecting database pool to our DatabaseService

现在我们需要从我们的`DatabaseModule`中导出这个`DatabaseService`，这样其他应用程序模块就可以使用它:

Exporting DatabaseService

我们现在可以完成`executeQuery`方法，该方法将调用`pool.query()`在数据库上执行查询:

Implementing the executeQuery method

该方法很简单:它接受查询文本、可选参数，并返回结果行集。

# 最后:清理

在执行第一个查询之前，我们在`DatabaseModule`中初始化的数据库池不会进行任何连接。发生这种情况时，会创建一个新的连接客户端，并在池处于活动状态时保存在池中。如果应用程序关闭，该池会突然关闭，而不会进行任何清理。

为了解决这个问题，我们可以使用 NestJS 生命周期挂钩并对终止信号做出反应。监听终止信号[确实会消耗更多的资源](https://docs.nestjs.com/fundamentals/lifecycle-events#application-shutdown)，所以这是 NestJS 的一个可选特性。可以使用应用程序实例的`enableShutdownHooks()`方法来启用它。

Enabling shutdown hooks

启用关闭挂钩后，我们可以在`DatabaseModule`中写入实际的关闭挂钩。

Implementing shutdown hook

我们使用一个[模块引用](https://docs.nestjs.com/fundamentals/module-ref)从模块上下文中检索我们的池对象的实例，然后调用它的`end()`方法来断开所有活动客户端。由于该方法返回一个承诺，NestJS 将在关闭序列中等待，直到承诺被解析或拒绝。

# 包扎

感谢阅读。我希望这个教程对你有用。在 NestJS 中，直接与数据库交互可能不是很常见的用例，但是当您希望对执行的查询有更多的控制时，它有时会很有用。如果你遇到任何问题，请在评论中告诉我。