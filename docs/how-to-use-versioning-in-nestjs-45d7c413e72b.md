# 如何在 NestJS 中使用版本控制

> 原文：<https://javascript.plainenglish.io/how-to-use-versioning-in-nestjs-45d7c413e72b?source=collection_archive---------1----------------------->

![](img/e6dd9e4aabd09f3d4d454f2d5d5b582f.png)

**更新(2021 年 7 月 24 日):本文被更新为使用最新版本的 NestJS 包。**

在开发 REST APIs 时，需要进行重大变更的情况并不少见，这可能会影响端点的契约或行为。

做出突破性改变的问题是消费者将会受到影响，无论他们是否需要快速改变他们的应用程序来解决你的突破性改变，或者有以前没有发生的意外行为。不管影响如何，如果不支持以前的版本，做出突破性的改变是不现实的。

这就是版本控制的由来。版本控制允许您拥有同时处于活动状态的不同版本的端点。它允许开发人员创建一个包含重大变更的新版本，同时仍然能够支持以前的版本。这使得消费者可以根据自己的时间表进行升级，总体上减少了麻烦。

NestJS 是一个用于构建 [Node.js](https://nodejs.org/en/) 服务器端应用程序的框架。在本文中，我不会涉及什么是 NestJS 以及为什么使用它的细节，但是我建议查看他们的[文档](https://docs.nestjs.com/)！

版本控制已经添加到 2021 年 7 月发布的 NestJS 的 v8 中，因此我们将在本文的示例中使用该版本。

在 NestJS 中，支持 3 种版本控制类型:

1.  `URI Versioning`:版本在请求的 URI 内传递
2.  `Header Versioning`:自定义请求头将指定版本
3.  `Media Type Versioning`:`Accept`请求头将指定版本

对于本文的重点，我们将使用`Media Type Versioning`。

## 设置 NestJS 应用程序

这一节将带您通过版本控制所需的设置来设置一个新的 NestJS 应用程序。

首先，确保您已经安装了 node v10.13.0 或更高版本，以及 npm，它应该与 node 一起自动安装。

接下来，我们将安装并使用 NestJS CLI 来生成新的应用程序。

```
$ npm i -g @nestjs/cli
$ nest new nest-versioning-demo
```

选择您喜欢的软件包管理器，并等待安装依赖项。

您可以使用以下命令启动该应用程序:

```
$ npm start
```

并使用以下命令验证它已经启动并正在运行:

```
$ curl localhost:3000
Hello World!
```

## 在 NestJS 应用程序中启用版本控制

为了使用版本控制，您必须在应用程序上启用该功能。这将启用整个应用程序的版本控制，包括所有控制器和路由。

更新您的`main.ts`文件以包含`enableVersioning(...)`函数调用:

```
import { VersioningType } from '@nestjs/common';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.enableVersioning({
    type: VersioningType.MEDIA_TYPE,
    key: 'v=',
  }); await app.listen(3000);
}bootstrap();
```

`enableVersioning`函数接受一个对象参数，该参数包含要使用的版本类型以及该类型所需的任何配置。

对于本文，我们将使用前面描述的媒体类型版本控制。我们可以使用`VersioningType`枚举(从`@nestjs/common`引入)来表明这一点。媒体类型版本控制需要一个额外的配置，`key`，它应该存在于`Accept`头中，作为我们应该用于版本的值的前缀。

对于本文，我们将使用键`v=`，我们的`Accept`标题将看起来像`Accept: application/json;v=1`或`Accept: application/json;v=2`。

## 添加版本化路径

在为我们的应用程序启用版本控制之后，下一步是添加一个版本控制的路由。

运行以下命令来生成新的控制器:

```
$ nest g controller Hello
```

文件生成后，更新`src/hello/hello.controller.ts`文件以包含以下方法:

```
import { Controller, Get } from '@nestjs/common';@Controller('hello')
export class HelloController {
  @Get()
  getHelloV1() {
    return 'Hello World V1!';
  } @Get()
  getHelloV2() {
    return 'Hello World V2!';
  }
}
```

如果我们现在运行应用程序并向`localhost:3000/hello`发出请求，我们将会看到响应`Hello World V1!`，而不管我们在`Accept`头中发送的版本。这是因为我们还没有告诉 NestJS 哪个版本应该使用哪个函数，所以默认为第一个。

要指定版本，我们有两个选项:

1.  指定整个控制器的版本
2.  指定特定路线/功能的版本

我们将从向路线添加一个版本开始。为此，我们使用`@Version`装饰器(从`@nestjs/common`导入)。更新`src/hello/hello.controller.ts`文件以包含功能的相应版本:

```
import { Controller, Get, Version } from '@nestjs/common';@Controller('hello')
export class HelloController {
  @Version('1')
  @Get()
  getHelloV1() {
    return 'Hello World V1!';
  } @Version('2')
  @Get()
  getHelloV2() {
    return 'Hello World V2!';
  }
}
```

现在，我们可以向两个版本化路由发出请求，并验证返回的响应:

```
$ curl localhost:3000/hello -H "Accept: application/json;v=1"
Hello World V1!
$ curl localhost:3000/hello -H "Accept: application/json;v=2"
Hello World V2!
```

就这样，我们有了一条版本化的路线！

**注意**:如果请求没有版本，或者版本没有匹配的路由，应用程序将响应 404 Not Found。

## 添加版本化控制器

除了将一个版本应用于特定的路由之外，我们还可以将一个版本应用于整个控制器和该控制器中的所有路由。

为此，我们将生成两个新的控制器:

```
$ nest g controller HolaV1
$ nest g controller HolaV2
```

文件生成后，我们将更新两个控制器以使用相同的`hola`路径，并添加它们各自的版本。

`src/hola-v1/hola-v1.controller.ts`:

```
import { Controller, Get } from '@nestjs/common';@Controller({
  path: 'hola',
  version: '1',
})
export class HolaV1Controller {
  @Get()
  getHola() {
    return 'Hola Mundo V1!';
  }
}
```

`src/hola-v2/hola-v2.controller.ts`:

```
import { Controller, Get } from '@nestjs/common';@Controller({
  path: 'hola',
  version: '2',
})
export class HolaV2Controller {
  @Get()
  getHola() {
    return 'Hola Mundo V2!';
  }
}
```

现在，我们可以向两个版本控制器发出请求，并验证返回的响应:

```
$ curl localhost:3000/hola -H "Accept: application/json;v=1"
Hola Mundo V1!
$ curl localhost:3000/hola -H "Accept: application/json;v=2"
Hola Mundo V2!
```

好了，我们现在有版本化的控制器了！

**增加版本中立路线**

对于不需要版本控制的场景，NestJS 有一个“版本中立”的模式，这表明不管请求中的版本是什么，或者如果请求中没有版本，都应该使用特定的函数。

**注意**:对于 URI 版本化，版本中立路由将没有包含在 URI 中的版本。因此，如果在版本中立路由上发送版本，NestJS 将无法匹配到 URI。

对于版本中立，我们将生成一个新的控制器:

```
$ nest g controller Health
```

为了表明控制器或路由是版本中立的，我们将使用从`@nestjs/common`导入的`VERSION_NEUTRAL`符号。我们还将向控制器添加一个 GET 路由:

```
import { Controller, Get, VERSION_NEUTRAL } from '@nestjs/common';@Controller({
  path: 'health',
  version: VERSION_NEUTRAL,
})
export class HealthController {
  @Get()
  getHealth() {
    return 'Healthy!';
  }
}
```

为了验证版本中立路线，我们可以在有版本和没有版本的情况下对其进行测试:

```
$ curl localhost:3000/health -H "Accept: application/json;v=1"
Healthy!
$ curl localhost:3000/health
Healthy!
```

现在我们也有了版本中立的路线！

## 结论

在本文中，我们展示了如何在 NestJS 应用程序上启用版本控制，并创建版本控制的路由、控制器和版本中立的控制器。

版本控制是 API 框架中一个非常有用的特性，可以对不断变化的需求做出反应，做出突破性的改变，同时仍然能够支持消费者可能使用的先前版本。NestJS 的这一新特性增加了将它用于 Node.js REST API 的许多理由。

我希望这篇文章对您使用 NestJS 的旅程有所帮助！

**注意:**你可以在 GitHub 上查看一个示例版本应用程序[。](https://github.com/rich-w-lee/nest-versioning-demo)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)