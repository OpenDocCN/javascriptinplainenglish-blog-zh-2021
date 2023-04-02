# 使用 NestJS 开始您的新项目

> 原文：<https://javascript.plainenglish.io/starting-your-new-project-with-nestjs-in-2021-df997815c740?source=collection_archive---------4----------------------->

在过去的几年里，主要是由于 Node.js，JavaScript 开始被用于创建服务器端应用程序。至于前端方面，我们已经看到一些好的框架出现并整合它们自己，比如 Angular、React 和 Vue.js。

![](img/22566791fe7b760f16653013b87401e2.png)

用于 Node.js 的后端库和框架也出现了，其中最流行的仍然是 Express。别误会，我喜欢快递。到目前为止，我已经用它工作了至少五年。Express 非常灵活且易于使用，在生产新的 API 时可以节省数小时的编码时间。

但是表达架构是一个主要问题。在 Express to code 中，有如此多的选择可以让你以不同的方式实现类似的结果。这开始成为培训新团队成员并让他们管理项目的一个难题。早期的学生更难理解为什么有些人用一种方式设计代码，而与此同时，其他人遵循完全不同的架构。

我们怎样才能有一个更标准的可伸缩的架构，在企业中也能毫无问题地运行呢？试图解决这个问题是 NestJS 出现的地方，你猜怎么着？它默认使用 Express，在引擎盖下。

> 如果你习惯于使用 Express，尝试 NestJS 将会是一个尽可能简单的体验。

NestJS 是一个**开源**框架，旨在允许您使用 TypeScript 的能力创建可伸缩的服务器端应用程序。它还使用了面向对象编程、函数式编程和函数式反应编程的概念。

至于 REST 开发，NestJS 为您内置了一切，例如:

*   [控制器](https://docs.nestjs.com/controllers)
*   [中间件](https://docs.nestjs.com/middleware)
*   [服务](https://docs.nestjs.com/providers#services)
*   [配置模块](https://docs.nestjs.com/techniques/configuration)
*   [认证](https://docs.nestjs.com/security/authentication)

它还提供了一个 CLI，允许您按照它们的架构创建您的框架。也就是说，您可以轻松地创建一个简单的新控制器，只需一行代码，例如:

```
nest g co name_of_your_controller
```

您也可能会想——但是如果我使用 GraphQL 呢？NestJS 有一个内置模块可以满足您的所有需求，您可以选择将其编程为 CodeFirst 策略或经典的 SchemaFirst 策略。

至于测试，NestJS 还提供了一个内置的[模块](https://docs.nestjs.com/fundamentals/testing)，它非常容易配置和使用，在引擎盖下使用 Jest 和 Supertest。

## 第一步样本

用 NestJS 启动一个项目超级简单。显然，它需要一些关于 Node.js、TypeScript 和 REST/GraphQL 的知识。

> 不管你用的是什么技术，你的背景知识越多，事情就越容易。

首先，你需要确保你已经安装了 [Node.js](https://nodejs.org/en/) 。然后，在终端中键入:

```
npm i -g @nestjs/cli
```

这个命令安装 nest cli，它允许您在他们的客户端的帮助下开始开发。要启动一个嵌套项目，可以运行以下命令

```
nest new my-first-nest-project
```

该命令将为您的项目启动一个脚手架，并要求您在 yarn 或 npm 之间进行选择。在这个例子中，我们将选择纱线而不是 npm。

```
We will scaffold your app in a few seconds..CREATE my-first-nest-project/.eslintrc.js (666 bytes)CREATE my-first-nest-project/.prettierrc (51 bytes)CREATE my-first-nest-project/README.md (3339 bytes)CREATE my-first-nest-project/nest-cli.json (64 bytes)CREATE my-first-nest-project/package.json (1973 bytes)CREATE my-first-nest-project/tsconfig.build.json (97 bytes)CREATE my-first-nest-project/tsconfig.json (339 bytes)CREATE my-first-nest-project/src/app.controller.spec.ts (617 bytes)CREATE my-first-nest-project/src/app.controller.ts (274 bytes)CREATE my-first-nest-project/src/app.module.ts (249 bytes)CREATE my-first-nest-project/src/app.service.ts (142 bytes)CREATE my-first-nest-project/src/main.ts (208 bytes)CREATE my-first-nest-project/test/app.e2e-spec.ts (630 bytes)CREATE my-first-nest-project/test/jest-e2e.json (183 bytes)? **Which package manager would you ❤️  to use?**npm❯ yarn
```

一旦完成，你将拥有一个名为 *my-first-nest-project 的文件夹。*打开文件夹，输入`yarn start`

```
$ nest start[Nest] 73358   - 01/12/2021, 11:57:45 AM   [NestFactory] Starting Nest application...[Nest] 73358   - 01/12/2021, 11:57:45 AM   [InstanceLoader] AppModule dependencies initialized +46ms[Nest] 73358   - 01/12/2021, 11:57:45 AM   [RoutesResolver] AppController {}: +5ms[Nest] 73358   - 01/12/2021, 11:57:45 AM   [RouterExplorer] Mapped {, GET} route +2ms[Nest] 73358   - 01/12/2021, 11:57:45 AM   [NestApplication] Nest application successfully started +1ms
```

就是这样。您有了第一个使用为您配置的模块和控制器的脚手架，所有的基本架构都准备好了。默认情况下，它在端口 3000 启动服务器。您可以在本地主机的浏览器中打开它，如[*http://localhost:3000*](http://localhost:3000/)*/，或者使用 curl:*

```
my-first-nest-project % curl localhost:3000Hello World!**%**
```

很酷，对吧？现在让我们检查代码结构。有几个配置文件我们在本文中没有深入研究，比如 nest-cli.json、tsconfig.json 等，但是有一个非常重要的文件值得编写，那就是 **src** 文件夹及其文件:

```
src/app.controller.spec.ts
src/app.controller.ts
src/app.module.ts
src/app.service.ts
main.ts
```

基本的 nest 生态系统分为模块、控制器和服务:

*   Module 是一个带有@Module 注释的类，它提供元信息来组织应用程序结构

```
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

*   控制器负责处理 HTTP 请求并向客户端返回响应

```
import { Controller, ***Get*** } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```

*   服务负责处理业务逻辑，负责数据存储和检索以及注入依赖关系

```
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

*main.ts* 文件是应用程序的主入口。这里声明了哪个将是应用程序的主模块，以及服务器将运行哪个端口。

```
import { ***NestFactory*** } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await ***NestFactory***.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

Nest 环境已经配置为对所有名称中包含. spec.ts 的文件运行单元测试。这将在自动化单元测试时帮助你。

```
import { Test, TestingModule } from '@nestjs/testing';
import { AppController } from './app.controller';
import { AppService } from './app.service';

***describe***('AppController', () => {
  let appController: AppController;

  ***beforeEach***(async () => {
    const app: TestingModule = await Test.*createTestingModule*({
      controllers: [AppController],
      providers: [AppService],
    }).compile();

    appController = app.get<AppController>(AppController);
  });

  ***describe***('root', () => {
    ***it***('should return "Hello World!"', () => {
      ***expect***(appController.getHello()).toBe('Hello World!');
    });
  });
});
```

要运行单元测试，只需运行以下:*纱线运行测试*

```
yarn run test**yarn run v1.22.4**$ jest**PASS ** src/**app.controller.spec.ts**AppControllerroot✓ should return "Hello World!" (10 ms)**Test Suites: 1 passed**, 1 total**Tests:       1 passed**, 1 total**Snapshots:** 0 total**Time:**        1.196 s, estimated 3 sRan all test suites.✨  Done in 2.31s.
```

在 *test* 文件夹中，我们会发现一个文件，其模式名包含*e2e-规格. ts* 。这个文件负责在 nest 生态系统中运行 e2e 测试。他们在引擎盖下使用*超级测试*，如果你熟悉它，你会很容易理解:

```
import { Test, TestingModule } from '@nestjs/testing';
import { INestApplication } from '@nestjs/common';
import * as request from 'supertest';
import { AppModule } from './../src/app.module';

***describe***('AppController (e2e)', () => {
  let app: INestApplication;

  ***beforeEach***(async () => {
    const moduleFixture: TestingModule = await Test.*createTestingModule*({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  });

  ***it***('/ (GET)', () => {
    return request(app.getHttpServer())
      .get('/')
      .expect(200)
      .expect('Hello World!');
  });
});
```

要运行 e2e 测试，您可以使用:*纱线运行测试:e2e*

```
yarn run test:e2e**yarn run v1.22.4**$ jest --config ./test/jest-e2e.json**PASS ** test/**app.e2e-spec.ts**AppController (e2e)✓ / (GET) (349 ms)**Test Suites: 1 passed**, 1 total**Tests:       1 passed**, 1 total**Snapshots:** 0 total**Time:**        1.574 s, estimated 3 sRan all test suites.✨  Done in 2.63s.
```

NestJS 生态系统非常大，我希望这些介绍性的步骤有助于您看到它的潜力。有几家大公司在他们的软件开发栈中采用 NestJS，比如 [Autodesk](https://www.autodesk.com/) 、 [Adidas](https://www.adidas.com) 、 [Decathlon](https://www.decathlon.com/) 以及其他几家公司。这使得它成为您学习的下一个健壮框架的有价值的候选对象。

NestJS [文档](https://docs.nestjs.com/)非常广泛，有几个特性很难一次全部讲述。关于我以前的文章中关于用 Express 构建 API 的基础知识的更新，我的下一篇文章将教你创建相同的 API，但是使用 NestJS。对于那些想要深入研究 Node.js 及其框架的人来说，掌握使用这两种框架进行构建的知识将是很好的培训。

与此同时，我正在制作 NestJS 系列。强烈推荐我之前的[系列](https://medium.com/@makinhs/another-expressjs-api-tutorial-for-2020-part-01-hello-world-969d3280d4c0)开始。我相信在 2021 年知道这些仍然很重要，因为你永远不知道你什么时候会和一个同样使用 Express 的团队一起工作。此外，请记住，NestJS 在引擎盖下使用 Express，这使您的学习双赢。

[](https://medium.com/@makinhs/another-expressjs-api-tutorial-for-2020-part-01-hello-world-969d3280d4c0) [## 2020 年的另一个 ExpressJS API 教程，第 1 部分— hello world

### 嘿，我在这里提出一些关于如何在 2020 年使用 ExpressJS 构建 API 的简短的书面教程。

medium.com](https://medium.com/@makinhs/another-expressjs-api-tutorial-for-2020-part-01-hello-world-969d3280d4c0) 

如果这篇文章对你有用，请随意鼓掌。这有助于我理解内容是否相关，并激励我继续写作。如果你有任何疑问或问题，或者如果你觉得我犯了什么错误，请随意评论。所有这些都有助于我提高写作水平。

下一篇文章再见。

[](https://makinhs.medium.com/creating-a-rest-api-series-with-nestjs-part-01-scaffolding-and-basic-cli-usage-30ace19c5bb8) [## 使用 NestJS 创建 REST API 系列—第 1 部分—搭建和基本 CLI 用法

### 欢迎回来！在这个迷你系列文章中，我将指导您如何使用 NestJS 框架构建 REST API

makinhs.medium.com](https://makinhs.medium.com/creating-a-rest-api-series-with-nestjs-part-01-scaffolding-and-basic-cli-usage-30ace19c5bb8) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)