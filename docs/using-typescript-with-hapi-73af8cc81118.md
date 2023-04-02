# 将 TypeScript 与 hapi 一起使用

> 原文：<https://javascript.plainenglish.io/using-typescript-with-hapi-73af8cc81118?source=collection_archive---------10----------------------->

最近一直在用 [hapi](https://hapi.dev) ，决定同时开始用 TypeScript。当我看的时候，虽然似乎没有太多的一起使用它们。以下是我学到的。

我将假设您对 JavaScript 有一定程度的熟悉，并对什么是 TypeScript 有基本的了解。

如果不是这样，我肯定会推荐阅读 MDN JavaScript 教程，然后是 5 分钟的脚本介绍。

我选择在下面的例子中使用[纱线](https://yarnpkg.com/)；如果您使用的是 [npm](https://docs.npmjs.com/) ，只需将`yarn add`改为`npm install`。

我已经包括了你需要什么来启动和运行系统，并试图在我们进行的过程中进行解释，但这篇文章不会深入到任何特定的点。我试着在我们进行的过程中加入相关的链接，但是如果我遗漏了什么，一定要让我知道，我会试着做得更好。

## 创建初始服务器

## 行政事务

第一件事——创建一个项目目录和`package.json`文件。然后安装 [hapi](https://hapi.dev/) 用于生产，因为我们知道我们会需要它。

```
$ mkdir hapi_typescript
$ cd hapi_typescript
$ yarn init -y
$ yarn add @hapi/hapi
```

我们还需要更多的开发包。这里我们添加了 TypeScript 系统本身，以及 hapi 和 node 的类型定义。

如果不安装它们，TypeScript 就不知道 Node 或 hapi 的任何类型细节，所以它会抱怨一些实际上并不是问题的东西。

我们希望能够看到实际的问题，并从使用 Node 和 hapi 的类型安全中受益。这篇文章中的类型定义都来自于[确定类型的](https://definitelytyped.org/)。

```
$ yarn add -D typescript @types/hapi__hapi @types/node
$ yarn add -D nodemon npm-run-all
```

接下来，我们必须用 TypeScript 选项创建一个`tsconfig.json`文件。最简单的办法就是让`tsc`为我们做这件事。(`tsc`是 TypeScript 编译器可执行文件。)

```
$ npx tsc --init
```

对于这个基本系统，我们将只调整两个选项— `outDir`(编译后的 JavaScript 放在哪里)和`rootDir`(源代码放在哪里):

```
"outDir": "./lib",
    "rootDir": "./src",
```

管理的最后一点——我们将把这些脚本添加到`package.json` 文件中，以便于开发。

`dev:tsc`在[监视模式](https://www.typescriptlang.org/docs/handbook/compiler-options.html)下启动编译器，这意味着它会监视任何更改并自动重建。

`dev:serve`使用`[nodemon](https://nodemon.io/)`在 JavaScript 改变时自动重新加载服务器。

`dev`使用`[npm-run-all](https://github.com/mysticatea/npm-run-all)`同时运行两个命令，所以你不必打开两个终端。

```
 "scripts": {
        "dev:tsc": "tsc --watch -p .",
        "dev:serve": "nodemon -e js -w lib lib/main.js",
        "dev": "run-p dev:*"
    }
```

## 代码！

对——现在我们终于可以做一些编码了！我们将把包含服务器安装代码的文件与实际启动它的文件分开。当我们开始添加测试时，它会有回报的。

注意变量的类型声明和函数的返回类型。如果你打算使用 TypeScript，你也可以从编译器捕捉类型错误中受益…

`src/server.ts`:

```
'use strict';

import Hapi from "@hapi/hapi";
import { Server } from "@hapi/hapi";

export let server: Server;

export const init = async function(): Promise<Server> {
    server = Hapi.server({
        port: process.env.PORT || 4000,
        host: '0.0.0.0'
    });

	// Routes will go here

    return server;
};

export const start = async function (): Promise<void> {
    console.log(`Listening on ${server.settings.host}:${server.settings.port}`);
    return server.start();
};

process.on('unhandledRejection', (err) => {
    console.error("unhandledRejection");
    console.error(err);
    process.exit(1);
});
```

`src/main.ts`:

```
import { init, start } from "./server";

init().then(() => start());
```

## 给它一个旋转

与其在这里使用`yarn dev`，不如让我们单独尝试这些阶段。

```
$ yarn dev:tsc
[19:54:59] Starting compilation in watch mode...

[19:55:00] Found 0 errors. Watching for file changes.
```

嗯，看起来很有希望。Ctrl-C 退出并启动服务器:

```
$ yarn dev:serve
yarn run v1.22.10
$ nodemon -e js -w lib lib/main.js
[nodemon] 2.0.7
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): lib/**/*
[nodemon] watching extensions: js
[nodemon] starting `node lib/main.js`
Starting server, listening on 0.0.0.0:4000
```

它还活着！是**活着**！

## 下一步

嗯；它还活着，但并没有做多少有用的事情。让我们听一个请求并发送一个回复。

## 试验

因为我们正在添加功能，所以让我们添加一个测试。(出于通常的原因，测试是好的；这不是说服你需要他们的地方。)

## 设置

我们将在`test`保留我们的。我们将使用`[chai](https://www.chaijs.com/)`和`[mocha](https://mochajs.org/)`来运行它们；因为我们使用的是 TypeScript，所以我们还想从 DefinitelyTyped 添加相关的类型注释。

```
$ mkdir test
$ yarn add -D chai mocha @types/chai @types/mocha
```

最后，我们将使用`ts-node`来直接运行它们，而不是将它们编译成 JavaScript。

```
$ yarn add -D ts-node
```

我们需要稍微调整一下`tsconfig.json`，告诉`tsc`不要尝试构建测试。将此添加到`compilerOptions`对象的末尾。

```
"exclude": [
    "test"
]
```

对于最后一点管理，我们将把这个脚本添加到`package.json`中，以便于运行测试。

```
"test": "NODE_ENV=test mocha -r ts-node/register test/**/*.test.ts"
```

## 实际测试代码！

最后，是时候添加我们的第一个测试了！

`test/index.test.ts`:

```
import { Server } from "@hapi/hapi";
import { describe, it, beforeEach, afterEach } from "mocha";
import { expect } from "chai";

import { init } from "../src/server";

describe("smoke test", async () => {
    let server: Server;

    beforeEach((done) => {
        init().then(s => { server = s; done(); });
    })
    afterEach((done) => {
        server.stop().then(() => done());
    });

    it("index responds", async () => {
        const res = await server.inject({
            method: "get",
            url: "/"
        });
        expect(res.statusCode).to.equal(200);
        expect(res.result).to.equal("Hello! Nice to have met you.");
    });
})
```

首先是导入我们将要使用的各种类型。然后我们从`server.ts`文件中导入`init`函数。

在每次测试之前，`beforeEach`函数会创建一个干净的服务器对象，`afterEach`函数会对其进行清理。分离服务器代码现在有了回报——我们可以初始化测试中使用的服务器，而实际上没有启动它的开销。

测试本身利用了 hapi `inject`方法，调用服务器代码，而实际上不必进行 HTTP 调用。在这里，我们要走的是`/`路线；您可以看到测试期望调用成功，并带有一条很好的小消息。

当然，我们还没有写那个代码，所以如果我们运行它…

```
0 passing (37ms)
  1 failing

  1) smoke test
       index responds:

      AssertionError: expected 404 to equal 200
      + expected - actual

      -404
      +200

      at hapi-typescript/test/index.test.ts:22:35
      [trace continues]
```

不出所料，失败了。让我们解决这个问题。

## 服务器代码

我们现在回到`server.ts`了。第一件事是修改文件顶部的类型导入，以包含`Request`类型:

```
import { Request, Server } from "@hapi/hapi";
```

我们将需要它来执行`index`函数，该函数为我们进行实际的回复。在这种情况下，它只是返回一个字符串，所以我们将它声明为返回类型。声明`request`的类型可以确保我们不使用该对象上不存在的任何属性或方法。

```
function index(request: Request): string {
    console.log("Processing request", request.info.id);
    return "Hello! Nice to have met you.";
}
```

最后，我们需要在`init()`函数中连接路线，在前面代码中的注释指出了这一点。

```
 server.route({
        method: "GET",
        path: "/",
        handler: index
    });
```

现在，如果我们进行测试…

```
smoke test
    ✓ index responds

  1 passing (33ms)

✨  Done in 2.25s.
```

万岁！幸福随之而来！

这是在同一个文件中定义的一条路线。下一篇文章将从另一个文件导入路径(通过适当的测试)，但是我认为这篇文章已经足够长了！