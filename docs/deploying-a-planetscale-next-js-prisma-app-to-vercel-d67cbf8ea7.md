# 将 PlanetScale，Next.js & Prisma 应用程序部署到 Vercel

> 原文：<https://javascript.plainenglish.io/deploying-a-planetscale-next-js-prisma-app-to-vercel-d67cbf8ea7?source=collection_archive---------18----------------------->

![](img/5e3da88d3f0b34600c88ea311b2e449d.png)

# 介绍

当探索无服务器数据库解决方案时，目前只有少数几种能够很好地匹配。你可以使用传统的 DBaaS 平台，比如 Amazon RDS 或 Heroku，但是如果不使用像 [PgBouncer](https://www.pgbouncer.org/) 这样的工具来使用某种连接池，你会发现你的数据库会很快耗尽其连接限制，并由于[无服务器限制](https://www.prisma.io/docs/guides/performance-and-optimization/connection-management#the-serverless-challenge)而关闭你的整个应用。如果有一个数据库解决方案可以与 Prisma 无缝集成，并且根本不用担心管理并发连接的问题就好了！输入[行星标度](https://planetscale.com/)。

# 什么是 PlanetScale？

基于 [Vitess](https://vitess.io/) ，PlanetScale 是一个新的 DBaaS 平台，它允许您在几秒钟内启动数据库，而完全不用担心连接管理。Vitess 是支持许多超大规模网站的相同技术，这些网站需要关键的正常运行时间、性能和可扩展性。PlanetScale 还引入了一些非常酷的概念，比如数据库分支(类似于 Git 分支逻辑)，因此您的数据库迁移是无缝和无阻塞的。

在本文中，我们将介绍如何创建一个全新的**next . js****Prisma**应用程序，使用[新发布的连接字符串选项](https://planetscale.com/blog/connect-any-mysql-client-to-planetscale-using-connection-strings)将其连接到 **PlanetScale** ，使用 PlanetScale 非阻塞模式更改工作流发出一个简单的部署请求，然后使用 **Vercel** 将其部署到生产环境中。

# 设置

# 行星尺度

在我们开始之前，请在 [PlanetScale](https://planetscale.com/) 注册一个账户。一旦注册完毕，下载 [PlanetScale CLI](https://planetscale.com/cli) ，这对于本地连接到我们的数据库、创建新的数据库分支，以及[在我们使用 Prisma 对我们的模式](https://docs.planetscale.com/tutorials/automatic-prisma-migrations)进行更改时发出部署请求非常重要。

从您的仪表板，点击“创建数据库”按钮，输入一个数据库名称(我将命名为我的教程-数据库)，选择一个地区，并取消选择启动教程数据库选项。

在无服务器应用程序中，为了减少延迟，选择尽可能靠近应用程序部署位置的数据库区域非常重要。在我的例子中，我的 Vercel 应用程序和 PlanetScale 数据库都在美国西部。

太棒了。一旦创建了数据库，请转到设置页面并启用**自动复制迁移数据**，每当我们合并[部署请求](https://planetscale.com/blog/non-blocking-schema-changes)时，它会将我们的 Prisma 模式迁移存储在一个名为 **_prisma_migrations** 的表中。

![](img/81642de3a7f40d69cb3237239a143930.png)

厉害！回到您的数据库仪表板，您应该看到这个视图。

![](img/e6d3567056da14afa8638d9981f8bab5.png)

现在，我们已经设置了数据库，并启用了复制 Prisma 迁移数据选项，接下来点击仪表板右上角的**连接**按钮，并为您的**主**分支生成一个新密码。

![](img/e7e1f8cd75da72e7d69c8d903924f775.png)

使用下拉菜单，选择 **Prisma** 格式，并确保将这些连接详细信息安全地保存在某个地方，因为 PlanetScale 会在初始生成后隐藏您的密码。(如果您放错了这些凭据，您可以随时生成一个新密码，并删除放错的密码)。这些是我们将在部署期间在 Vercel 上的 Prisma `DATABASE_URL`环境变量中使用的细节。

由于 Prisma 迁移遵循 PlanetScales 非阻塞模式迁移工作流，我们将需要从我们的主数据库分支**创建两个额外的分支，以便处理这些模式更改。这可以通过 **PlanetScale CLI** 轻松完成。**

在您选择的终端中发出以下命令，登录 PlanetScale CLI:

```
pscale auth login
```

现在我们已经通过了身份验证，让我们创建另外两个**开发分支**:

```
pscale branch create tutorial-db initial-setup 
pscale branch create tutorial-db shadow
```

在两个单独的终端中，使用以下命令连接到每个数据库分支:

```
pscale connect tutorial-db initial-setup --port 3309pscale connect tutorial-db shadow --port 3310
```

# Next.js & Prisma

现在我们已经建立并运行了数据库和数据库分支，是时候初始化我们的 **Next.js** 和 **Prisma** 应用程序了。

使用以下命令启动一个新的 Next.js 项目:

```
npx create-next-app planetscale-prisma-next
```

`cd`进入新项目目录，并使用以下命令初始化 Prisma:

```
npx prisma init
```

像这样修改项目根目录下的`.env`文件:

```
DATABASE_URL="mysql://root@127.0.0.1:3309/tutorial-db" SHADOW_DATABASE_URL="mysql://root@127.0.0.1:3310/tutorial-db"
```

为了确保平台兼容性，我们还需要对我们生成的`prisma`文件夹中的`schema.prisma`文件进行一些特定于行星尺度的调整。编辑我们的数据源并生成以启用 **planetScaleMode** ，包含我们的 **shadowDatabaseUrl** ，并将 **planetScaleMode** 添加到我们的 previewFeatures 数组中。

```
datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
  shadowDatabaseUrl = env("SHADOW_DATABASE_URL")
  planetScaleMode = true
}

generator client {
  provider = "prisma-client-js"
  previewFeatures = ["planetScaleMode"]
}
```

出于本教程的考虑，我们将为一篇**文章**创建一个简单的 Prisma 模型，我们将通过一个无服务器函数和 **Prisma 客户端**检索该模型。我们不会深入到 UI 中，因为我们要做的只是演示如何设置和部署。因此，在编辑模式后，我们将手动向数据库中输入一些数据。将以下内容添加到我们的`schema.prisma`文件中:

```
datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
  shadowDatabaseUrl = env("SHADOW_DATABASE_URL")
  planetScaleMode = true
}

generator client {
  provider = "prisma-client-js"
  previewFeatures = ["planetScaleMode"]
}

model Post {
  id        Int      @default(autoincrement()) @id
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  title     String   @db.VarChar(255)
  content   String
}
```

现在我们有了模式设置，让我们生成我们的第一个 Prisma 迁移！

```
npx prisma migrate dev --name init
```

如果一切顺利，我们应该在终端上看到一条成功消息，以及项目中的一个新的`migrations`文件夹。现在，是时候打开一个 deploy-request，将这些更改带到我们的主数据库分支。

```
pscale deploy-request create tutorial-db initial-setup
```

呜哇！我们刚刚创建了第一个 **PlanetScale 部署请求**。如果我们返回到我们的仪表板，并导航到我们的部署请求选项卡，我们应该看到一个针对我们的模式更改的打开的部署请求。

![](img/53ee2f91e366b0ab21d6829a633d75d6.png)

单击**Add changes to deploy queue**按钮，如果一切顺利，我们的更改将被部署到主数据库分支！

现在我们已经更新了我们的主分支，接下来关闭已经连接到 PlanetScale 的两个终端，让我们重新运行一个命令，在端口 3309 上打开到我们的**主**分支的连接，这样我们就可以向我们的数据库添加一个 **Post** 记录。

```
pscale connect tutorial-db main --port 3309
```

让我们在项目中打开一个新的终端并运行`npx prisma studio`,这样我们就可以打开 Prisma 的 web GUI，允许我们向 PlanetScale 数据库添加一个新的 Post 记录。点击工具栏上的**添加记录**，输入您想要的任何样本数据。

![](img/a92030f8e0c024f71cd513043106ed5a.png)

既然我们已经建立了数据库，我们的模式已经部署到我们的主分支，并且一个示例帖子已经添加到我们的数据库，现在是时候建立一个**无服务器函数**来检索我们所有的帖子了。

由于我们处理的是一个**无服务器**应用程序，我们希望避免在每个后续请求中实例化一个新的 **Prisma 客户端**来保留连接，所以让我们在项目的根目录下创建一个名为`lib`的新文件夹和一个名为`prisma.js`的文件，这样我们就可以导出一个可重用的 Prisma 客户端。

```
import { PrismaClient } from '@prisma/client'

const prisma = global.prisma || new PrismaClient();

if (process.env.NODE_ENV === "development") global.prisma = prisma;

export default prisma
```

接下来，让我们在`pages/api`中的`api`文件夹内创建一个名为`posts.js`的新文件，包括以下内容:

```
import prisma from "../../lib/prisma";

export default async function assetHandler(req, res) {
    const { method } = req;

    switch (method) {
        case "GET":
            try {   
                const posts = await prisma.post.findMany();
                res.status(200).json(posts);
            } catch(e) {
                console.error("Request error", e);
                res.status(500).json({ error: "Error fetching posts" });
            }
            break;
        default:
            res.setHeader("Allow", ["GET"]);
            res.status(405).end(`Method ${method} Not Allowed`);
            break;
    }
}
```

现在，如果我们访问`http://localhost:3000/api/posts`，我们应该会看到从我们的 PlanetScale 数据库中获取的帖子记录！

# 部署

由于我们正在部署到 **Vercel** ，请确保您已经注册并连接了您的 Github 帐户。将文件提交到 Github 后，选择 Vercel 上的**新项目**选项，向下滚动到**环境变量**部分。

使用您之前为我们的主分支保存的**连接字符串细节**，用您之前保存的连接字符串为我们的`DATABASE_URL`创建一个新的环境变量。

由于 Vercel 使用特定的 Linux 发行版，我们需要确保编辑我们的连接字符串以指向正确的证书位置，即`/etc/pki/tls/certs/ca-bundle.crt`。

您的连接字符串环境变量应该类似于:

`mysql://YOUR_USER:************@YOUR_HOST/tutorial-db?sslmode=require&sslcert=/etc/pki/tls/certs/ca-bundle.crt`

继续并点击部署！

一旦部署了应用程序，如果您导航到同一个`/api/posts`端点，您应该会看到返回的数据。

恭喜您，您已经成功将一个使用 **PlanetScale** 作为数据库的 **Next.js Prisma** 应用程序部署到 **Vercel** ！

# 包裹

我希望这篇文章对那些希望将 PlanetScale 集成到他们的技术堆栈中，并使用 Vercel 将其部署到生产环境中的开发人员有所帮助。PlanetScale 提供的开发者体验棒极了，他们的支持也是无与伦比的(特别感谢 [Nick Van Wiggeren](https://twitter.com/NickVanWig) 帮助我解决了写这篇文章时遇到的一个问题)。

如果你想看看这个演示使用的代码，请点击这里的库。

感谢阅读！

*最初发布于 2021 年 8 月 16 日*[*https://David parks . dev*](https://davidparks.dev/blog/planetscale-deployment-with-prisma/)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)