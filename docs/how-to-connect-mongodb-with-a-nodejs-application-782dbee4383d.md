# 如何将 MongoDB 与 Node.js 应用程序连接

> 原文：<https://javascript.plainenglish.io/how-to-connect-mongodb-with-a-nodejs-application-782dbee4383d?source=collection_archive---------3----------------------->

![](img/a5f5e1a2a6cd0f4c995d21918fda2c55.png)

Connecting MongoDB with a NodeJS Application

你有 MongoDB 数据库吗？是否要用 Node.js 管理此数据库？

在本快速入门指南中，我将向您介绍使用 MongoDB 和 Node.js 的基础知识。我们将从 Node.js 脚本建立到 MongoDB 数据库的连接，检索数据库列表，并将结果打印到您的控制台。

# 设置好一切

在我们开始之前，要求我们已经满足了使用 MongoDB 和 Node.js 的所有先决条件。

# 设置 Node.js

首先，我们需要确保你有 Node.js 的支持版本。如果你没有 Node.js 的支持版本，这里有一篇文章可以帮助你升级到最新版本。MongoDB 的最新版本需要 Node.js 版本 *4.0* 或更高版本。对于本文，我们将使用 Node.js 版本 *14.15.4* 。

# 安装 MongoDB Node.js 包

MongoDB Node.js 包允许您在 Node.js 应用程序中轻松地与 MongoDB 数据库交互并执行查询。该软件包是本快速入门指南所必需的。

如果您还没有安装 MongoDB Node.js 包，您可以通过执行以下命令来安装它:

```
*npm install mongodb*
```

运行该命令还将显示当前安装的软件包版本号。请参见 [MongoDB 兼容性](https://docs.mongodb.com/drivers/node/compatibility)文档，了解每个版本的 Node.js 需要哪个版本的 Node.js。

# 创建一个 MongoDB atlas 集群并加载数据

接下来您需要的是一个 MongoDB 数据库。如果您还没有数据库，可以使用 Atlas 创建一个。Atlas 是 MongoDB 的完全托管数据库服务，允许您随意创建和操作数据库。Atlas 帮助您创建一个集群，一组存储数据库副本的节点。

# 集群的连接信息

最后一步是让集群为连接做好准备。

在 Atlas 中，导航到您的集群并单击 connect 将会弹出客户端连接向导。向导将显示您当前的 IP 地址，并将其添加到 IP 访问列表中。如果您还没有创建 MongoDB 用户，可以在这里创建。请务必记下您的用户名和密码，因为稍后会用到它们。

接下来，向导将提示您选择一种连接方法。在这里，您必须选择“连接您的应用程序”,这将提示选择驱动程序版本。这将为您提供一个连接字符串，您需要复制该字符串以供以后使用。

# 从 Node.js 连接到您的数据库

现在一切都设置好了，是时候编写一个 Node.js 脚本来连接到您的数据库并列出集群中的所有数据库了。

# 导入 MongoClient

MongoDB 的模块导出 MongoClient，我们将使用它连接到我们的 MongoDB 数据库。我们将使用 MongoClient 的一个实例连接到一个集群，访问集群中的一个特定数据库，并关闭我们的连接。

```
const {MongoClient} = require(“mongodb”)
```

# 创建我们的主要功能

接下来，我们将创建一个 main()函数，它将允许我们连接到 MongoDB 集群，调用函数来查询数据库，并关闭我们的连接。

```
async function main() {// Code}
```

在 main 函数中，我们将为我们的连接 URL 创建一个常量实例。连接 URL 是包用来连接 MongoDB 数据库的一组指令。它指示包如何连接到 MongoDB 以及它应该如何表现。连接 URL 定义如下:

有关建立连接的更多信息，请访问官方文档。

快速入门指南的连接 URI 是您在上一节中在 Atlas 中复制的那个。粘贴时不要忘记用您在上一节中创建的凭证更新 *<用户名>* 和 *<密码>* 标签。该字符串还包括 *< dbname >* 标记，该标记应该用您希望在集群中访问的数据库的名称进行更新。

```
const uri = “mongodb+srv://<username>:<password>@<your-cluster-url>/test?retryWrites=true&w=majority”;
```

现在我们已经创建了我们的 URI，我们将创建我们的 MongoClient 的一个实例。

```
const client = new MongoClient(uri);
```

**注意:**当您运行这段代码时，您可能会收到一些关于 URL 字符串的反对警告。您可以通过将选项传递给 MongoClient 来删除它。参见 [Node.js MongoDB API 文档](https://mongodb.github.io/node-mongodb-native/3.6/api/MongoClient.html)获得更多帮助。

我们现在准备使用 MongoClient 建立到集群的连接。我们将使用 *client.connect()* 连接到我们的数据库。我们将使用 await 关键字来指示我们应该阻止进一步的代码执行，直到操作完成。

```
*await* client.connect();
```

我们现在可以与我们的数据库进行交互。对于本指南，我们将构建一个函数来打印集群中所有数据库的列表。通常的做法是使用逻辑名称来提高代码的可读性。现在让我们调用函数 *listDatabases()* 。

```
*await* listDatabases(client);
```

我们可以通过将代码包装在一个 try and catch 语句中来进一步改进代码。这将允许我们处理和处理任何意外的错误。我们还想确保我们的连接是安全的，所以我们将使用 finally 语句来结束我们的连接:

```
*try* {*await* client.connect();*await* listDatabases(client);}*catch* (e) {console.error(e);}*finally* {*await* client.close();}
```

现在我们已经准备好了主函数，我们需要调用它并将错误发送到控制台。将所有这些放在一起，我们的代码看起来像这样:

```
async function main(){const uri = “mongodb+srv://<username>:<password>@<your-cluster-url>/test?retryWrites=true&w=majority”;const client = new MongoClient(uri);*try* {*await* client.connect();*await* listDatabases(client);}*catch* (e) {console.error(e);}*finally* {*await* client.close();}}main.catch(console.error);
```

# 列出集群中的数据库

Node.js 允许我们创建不同的函数，以不同的方式操作我们的 MongoDB 集群。对于本快速入门指南，我们将创建一个 *listDatabases* 函数，该函数将列出集群中的所有数据库。在需要小心管理多个数据库的情况下，或者在一个数据库中的趋势可能与另一个数据库相关的数据分析中，这种功能非常有用。

我们的函数将检索集群中所有数据库的名称，并将它们打印到控制台:

```
async function listDatabases(client){databasesList = *await* client.db().admin().listDatabases();console.log(“Databases:”);databasesList.databases.forEach(db => console.log(` — ${db.name}`));};
```

# 执行您的代码

在执行代码之前，将脚本保存在文件中是很重要的。它可以被命名为任何东西，但是给你的文件起一个逻辑名是一个常见的惯例。为此，我将我的文件命名为“demo.js”。

可以通过在终端中运行命令行来执行该脚本:

```
*node demo.js*
```

终端将显示集群中所有数据库的名称。

# 最后的想法

今天，我们能够建立到 MongoDB 数据库的连接。我们能够编写 Node.js 脚本，检索集群中的数据库列表，并在控制台中查看结果。我们还理解了连接 URL 和它如何改变我们的连接行为，以及编写可以帮助查询我们的数据库的函数。

我希望这篇文章能帮助您理解连接 Node.js 和 MongoDB 的基础知识。要获得进一步的帮助，你可以访问 [MongoDB 的官方文档](https://docs.atlas.mongodb.com/connect-to-database-deployment/)，在那里他们给出了你在安装或连接数据库时可能遇到的任何问题的详细信息。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)