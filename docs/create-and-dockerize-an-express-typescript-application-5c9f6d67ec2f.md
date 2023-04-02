# 创建一个 Express TypeScript 应用程序并对其进行分类

> 原文：<https://javascript.plainenglish.io/create-and-dockerize-an-express-typescript-application-5c9f6d67ec2f?source=collection_archive---------2----------------------->

## 快速应用程序的简易归档方法

![](img/5a4a0d542aa35567a33c3b13a54fa12e.png)

Photo by [Ian Taylor](https://unsplash.com/@carrier_lost?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你知道 [Node.js](https://nodejs.org/en/) ，你可能也知道非常流行的 web 框架 [Express](https://expressjs.com/) 。这是一个最小的、经过实战检验的 web 框架。另一方面， [TypeScript](https://www.typescriptlang.org/) 是一种基于 JavaScript 的开源语言。它已经很受欢迎，而且越来越受欢迎。TypeScript 增加的价值是类型定义。由于类型检查可以确保您的程序正确运行，并且所有有效的 JavaScript 代码也是类型脚本代码，因此许多开发人员认为类型脚本是 JavaScript 的更好替代方案。因此，结合这两种技术——Express 和 TypeScript，您可以轻松地构建一个可靠的应用程序。用它添加 Docker 将使您在部署时的生活变得轻松。

## 目录

*   创建一个 Express 和 TypeScript 应用程序
*   设置 tsconfig.json 文件
*   添加必要的脚本
*   将 Docker 添加到您的应用程序
*   用 Docker 运行应用程序
*   得到这个例子

# 创建一个 Express 和 TypeScript 应用程序

这是一种非常简单的技术。您可以使用与创建 JavaScript express 应用程序相同的技术。但是您需要添加一些额外的包来设置 TypeScript。在您的终端中运行以下命令:

```
$ mkdir express-typescript-docker
$ cd express-typescript-docker
~/express-typescript-docker $ npm init --yes
~/express-typescript-docker $ npm i express typescript ts-node nodemon
~/express-typescript-docker $ npm i --save-dev @types/express
~/express-typescript-docker $ tsc --init
```

*   **mkdir <文件夹名>将创建一个项目文件夹。**
*   使用**光盘<文件夹名称>进入**文件夹。
*   NPM**init–yes**将在项目目录中创建一个 package.json 文件。
*   **npm i** 将安装必要的包，如 **express** 、 **typescript** 、 **ts-node** 、 **nodemon** 和—**-save-dev**标志，用于在 **package.json** 的 **devDependencies** 部分添加依赖项。
*   TSC–init 将在您的项目目录中创建一个 tsconfig.json 文件。该文件表示 typescript 的编译器选项，这意味着该文件告诉 typescript 如何使用编译器。

# 设置 tsconfig.json 文件

您可以保留 tsconfig.json 的大部分属性，但是我们可能需要修改它的一些属性。我要改变的是，

在 compilerOptions 属性中，

*   将**目标**属性值更改为**“es 2015”**以指定 ECMAScript 版本。
*   将 **outDir** 值设置为**“构建”**。这是 typescript 编译器的输出目录。
*   将 **moduleResolution** 设置为**【节点】**。

并添加一个属性**,将**排除在**compile options**属性的同级和外部

```
"compilerOptions": {...}
"exclude": [
    "node_modules"
]
```

现在我们有了一个项目目录，并设置了必要的环境。让我们创建一个 **index.ts** 文件来编写我们的代码并创建一个服务器。

~/express-typescript-docker $ touch index . ts

用你最喜欢的代码编辑器打开它。我更喜欢 vs 代码。它是轻量级的，有很多有用的插件。在 index.ts 中，让我们编写一些代码。

```
import express from 'express';const app = express();const PORT = 3000;app.get('/', (req, res) => {res.send('Hello World!');});app.listen(PORT, () => {console.log(`Express server is listening at ${PORT}`);});
```

在 index.ts 文件中，我们创建了一个只有一个 GET 路由的基本 express 服务器。我希望你理解这一部分。

# 添加必要的脚本

现在要运行这个 **index.ts** 文件，让我们在 **package.json** 文件中添加一个脚本。如果您查看这个包，您可以看到一个名为 **scripts** 的属性部分。在这个部分中，您可以添加任意数量的必要脚本，并且可以使用**NPM run<script _ name>**来运行它们。让我们添加一个脚本 **start:dev** 。

```
"start:dev": "nodemon index.ts"
```

现在运行下面的命令来启动您的服务器。

```
~/express-typescript-docker $ npm run start:dev
```

它会在你的控制台上显示结果。

```
> express-typescript-docker@1.0.0 start:dev /home/sbr/express-typescript-docker
> nodemon index.ts[nodemon] 2.0.12
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: ts,json
[nodemon] starting `ts-node index.ts`
Express server is listening at 3000
```

你的服务器现在正在运行，你可以用 **localhost:3000** 连接它。打开浏览器，点击地址，你可以看到服务器发送的信息。

```
Hello World!
```

您可以添加另一个脚本来编译您的 typescript 代码。

```
"build": "tsc"
```

如果您运行这个脚本，您的项目将被编译，并且在您的项目目录中将创建一个新的目录构建。因此，您可以查看构建目录来查看编译后的代码。但这不是必须的。

# 将 Docker 添加到您的应用程序

现在我们有了一个用 express 和 typescript 构建的可运行的应用程序。所以现在我们可以专注于将 Docker 添加到我们的应用程序中，因为它将帮助我们部署应用程序。这相当容易。在您的根目录中创建一个 docker 文件，并将以下配置。

```
FROM node:latestWORKDIR /srv/appCOPY package*.json ./RUN npm installCOPY . .RUN npm run buildEXPOSE 3000CMD ["node", "build/index.js"]
```

使用以下命令在 Docker 文件所在的目录下创建一个. dockerignore 文件，这样可以防止本地模块和日志被复制到 Docker 映像上。

```
node_modules
npm-debug.log
```

# 用 docker 运行应用程序

现在运行下面的命令来构建 docker 映像。

```
docker build . -t express-typescript-docker
```

这个命令将准备一个最新的 docker 图像标签，因为我们没有指定任何标签。如果需要，您可以指定标签。

运行以下命令来运行 docker 容器。

```
docker run -p 3000:3000 -d express-typescript-docker:latest
```

使用-d 运行容器将在分离模式下运行容器。它将在后台运行容器。标志-p 将公共端口重定向到容器内部的私有端口。

打印应用程序的输出

```
# Get container Id
docker ps#Print application output
docker logs <container id># If you need to go inside the container
docker exec -it <container id> /bin/bash
```

希望你已经理解了程序和概念。如果你觉得这篇文章有帮助，请分享给你的朋友。您可能也喜欢这篇关于使用 [bull](https://www.npmjs.com/package/bull) 实现基于队列的作业管理器的文章。

这篇文章可能对你有帮助。等待你们的消息。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)