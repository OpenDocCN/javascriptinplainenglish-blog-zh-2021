# 带有 TypeScript 的 Node.js 初学者指南

> 原文：<https://javascript.plainenglish.io/beginners-guide-to-node-js-with-typescript-26e4a46ccbc5?source=collection_archive---------6----------------------->

时不时的要不要摆弄一些特定的脚本？或者您是否愿意在不使用任何提供现成 TypeScript 的框架的情况下开始一个新项目？这篇文章可能对你有用。

![](img/e0ec269c7930c50d528b715242a717d8.png)

Foto de [Karolina Grabowska](https://www.pexels.com/pt-br/@karolina-grabowska?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) no [Pexels](https://www.pexels.com/pt-br/foto/anonimo-apartamento-caixa-bau-4506270/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

欢迎回来。在本文中，我将编写设置 TypeScript 项目的基础知识。如果您碰巧还停留在过去，没有使用任何已经提供了现成框架的框架，那么这篇文章将对您有用。

但是为什么要写这个呢？基本上是为了写一些内容，把我的 CLI 付诸行动，以及练习编码的重要性，你可以做的乐趣。同时，在工作中，你应该多加练习。

所以，今天，这将是我练习的操场。

让我们开始吧:

要启动 TypeScript 项目，您需要安装 Node.js 和 npm 包(或 yarn)。TypeScript 需要以某种方式进行转换或解释，通常我们可以这样做:

*   您使用创建**/*的编译器来“构建”您的类型脚本代码。js“构建”文件
*   您可以使用 npm 中的 [ts-node](https://www.npmjs.com/package/ts-node) 包“本地运行”您的类型脚本。

此外，您需要始终在文件的根目录中声明一个 tsconfig.json 文件，并添加一些 npm 脚本来简化您的工作。当然，根据项目的不同，您需要调整一些配置，但是步骤是相同的。我真的建议你在使用任何自动化工具之前至少做一次。

谈到自动化工具，对于本文，我的目标是使用我的 [cli 工具](https://www.npmjs.com/package/makin-cli)创建一个简单的“hello world ”,同时解释 TypeScript 配置。

出于对“如何创建 Node.js cli”的好奇，我创建了一个[**makin-cli**](https://www.npmjs.com/package/makin-cli)**CLI，并且我从一个简单的 CLI 开始，它可以为您的项目添加更漂亮、更简洁的元素。然后我想，“添加 TypeScript 自动化配置也是为了好玩吗？”现在，0.0.13 版本已经提供了这个选项。**

**要安装 CLI:**

```
npm i -g makin-cli
```

**然后确认其版本:**

```
✗ makin-cli -V
[23:14:38] [info]                       _      _                          _   _ 
  _ __ ___     __ _  | | __ (_)  _ __             ___  | | (_)
 | '_ ` _ \   / _` | | |/ / | | | '_ \   _____   / __| | | | |
 | | | | | | | (_| | |   <  | | | | | | |_____| | (__  | | | |
 |_| |_| |_|  \__,_| |_|\_\ |_| |_| |_|          \___| |_| |_|

0.0.11
```

**现在，让我们使用一个文件夹来创建我们的 TypeScript 项目。在我的情况下，它被称为**中型脚本。****

**在这里，我们应该首先从以下方面开始我们的项目:**

```
npm init
```

**对于本文，我只是按 enter/return 键来确认所有提供的可选选项，而不做任何更改，结果是:**

```
**➜  medium-typescript** npm initThis utility will walk you through creating a package.json file.It only covers the most common items, and tries to guess sensible defaults.See `npm help init` for definitive documentation on these fieldsand exactly what they do.Use `npm install <pkg>` afterwards to install a package andsave it as a dependency in the package.json file.Press ^C at any time to quit.package name: (medium-typescript)version: (1.0.0)description:entry point: (index.js)test command:git repository:keywords:author:license: (ISC)About to write to /Users/marcossilva/projects/medium-typescript/package.json:{"name": "medium-typescript","version": "1.0.0","description": "","main": "index.js","scripts": {"test": "echo \"Error: no test specified\" && exit 1"},"author": "","license": "ISC"}Is this OK? (yes)
**➜  medium-typescript**
```

**所以现在我们有了一个除了 package.json 文件之外什么也不包含的空白项目。**

**通常，我们在一个 **src** 文件夹中编写我们的“源”代码，并将运行整个应用程序的初始文件命名为 *index.ts* 。为此，我将创建一个 src 文件夹，然后在 src 文件夹中创建 index.ts 文件:**

```
**➜  medium-typescript** mkdir src**➜  medium-typescript** touch src/index.ts**➜  medium-typescript**
```

**一个奇怪的事实:如果你现在将以下内容添加到你的索引中**

```
(async () => {
  ***console***.log('Hello World');
})()
```

**您仍然可以运行:**

```
**➜  medium-typescript** node src/index.tsHello Typescript**➜  medium-typescript**
```

**而且看起来效果非常好。但是如果你开始用某种更具体的类型脚本方式编码，就不会了。现在，让我们创建一个名为 services 的文件夹，然后创建一个名为 *hello.service.ts* 的文件，文件的最小长度为:**

```
class HelloService {
  getHello() {
    return 'Hello World';
  }
}

export default new HelloService()
```

> **注意，将服务导出为 *new HelloService()* 会使您的类使用 [**单例模式**](https://en.wikipedia.org/wiki/Singleton_pattern) **。****

**然后，更新我们的 src/index.ts:**

```
import helloService from './services/hello.service';

(async () => {
  ***console***.log(helloService.getHello());
})()
```

**现在，再运行一次:**

```
**➜  medium-typescript** node src/index.ts(node:24314) Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension.(Use `node --trace-warnings ...` to show where the warning was created)/Users/marcossilva/projects/medium-typescript/src/index.ts:1import helloService from './services/hello.service';^^^^^^SyntaxError: Cannot use import statement outside a moduleat wrapSafe (internal/modules/cjs/loader.js:988:16)at Module._compile (internal/modules/cjs/loader.js:1036:27)at Object.Module._extensions..js (internal/modules/cjs/loader.js:1101:10)at Module.load (internal/modules/cjs/loader.js:937:32)at Function.Module._load (internal/modules/cjs/loader.js:778:12)at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:76:12)at internal/main/run_main_module.js:17:47**➜  medium-typescript**
```

**欢迎来到 Typescript…**

## **解决和配置它**

**如前所述，我们需要安装所需的包，并创建和配置 tsconfig.json 文件。现在， **makin-cli** 进入游戏并试图为你自动化这个机械过程。在新 TypeScript 项目的根目录中，让我们运行:**

```
makin-cli -ts
```

**输出应该是:**

```
➜  medium-typescript makin-cli -ts
[23:28:12] [info]                       _      _                          _   _ 
  _ __ ___     __ _  | | __ (_)  _ __             ___  | | (_)
 | '_ ` _ \   / _` | | |/ / | | | '_ \   _____   / __| | | | |
 | | | | | | | (_| | |   <  | | | | | | |_____| | (__  | | | |
 |_| |_| |_|  \__,_| |_|\_\ |_| |_| |_|          \___| |_| |_|

[23:28:12] [info] Welcome back ;)
[23:28:12] [info] Configuring typescript...
[23:28:12] [info] Installing typescript [@types/node](http://twitter.com/types/node) ts-node
[23:28:20] [info] Adding tsconfig.json
[23:28:20] [info] Adding build and start scripts to package.json
➜  medium-typescript
```

**它现在应该用以下内容更新您的 package.json devDependencies:**

```
"devDependencies": {
  "@types/node": "^16.9.4",
  "ts-node": "^10.2.1",
  "typescript": "^4.4.3"
}
```

**并在 package.json 上自动生成以下脚本:**

```
"build": "tsc -p .",
"start": "ts-node src/index.ts"
```

**最后也是重要的一点，您可以看到现在您有了一个 *tsconfig.json* 文件，它包含:**

```
{
  "compilerOptions": {
    "module": "commonjs",
    "declaration": true,
    "removeComments": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "allowSyntheticDefaultImports": true,
    "target": "ES2020",
    "lib": ["ES2020"],
    "moduleResolution": "node",
    "sourceMap": true,
    "outDir": "./dist",
    "baseUrl": "./",
    "incremental": true
  }
}
```

**介意***【outDir】:"的差距。****/dist 会影响你的 JavaScript 编译构建。如果你想要其他的，请更改这个文件。***

***现在，我们可以再次运行我们的 index.ts，但是使用将在 *ts 节点 src/index.ts* 中运行的 npm 启动脚本，该脚本使用 **ts 节点**来执行 TypeScript。***

```
***➜  medium-typescript** npm run start> medium-typescript@1.0.0 start> ts-node src/index.tsHello World**➜  medium-typescript***
```

***一切都好，一切就绪！我们已经可以编码和运行 TypeScript 了。构建和运行呢？***

```
***➜  medium-typescript** npm run build> medium-typescript@1.0.0 build> tsc -p .**➜  medium-typescript** node dist/index.jsHello World**➜  medium-typescript***
```

***当我们运行`npm run build`时，我们会将所有的 TypeScript 文件编译成 JavaScript，并将其添加到 **dist** 文件夹中。一旦它们是纯 JavaScript，您就可以运行“node dist/index.js ”,您将再次毫无问题地获得 Hello World。***

***有了以上所有内容，您已经能够在您的项目中玩和练习 TypeScript 了。当然，构建真实世界的 API、微服务、前端和其他东西需要经历一个获取知识的巨大旅程，但每个人都从自己的第一步开始。***

***我还假设，如果你读到这里，那是因为你要么正在开始你的软件开发职业生涯，要么你已经有了经验，但还没有打字稿。所以现在，你已经准备好更进一步了！***

***如果你读到这里并且使用了 [makin-cli](https://www.npmjs.com/package/makin-cli) ，非常感谢！如果你真的是一个 TypeScript 初学者，我会要求你创建一个新的 Hello World，但不要使用我的 CLI。只需重复一次 CLI 的操作，即手动:***

*   ***添加依赖项(提示:`npm i --save-dev @types/node ts-node typescript`***
*   ***在 package.json 的脚本中添加启动和构建脚本***
*   ***添加我的 cli 自动生成的相同 tsconfig.json 文件***

***用更漂亮的和 ESLint 在你的代码中增加一点质量怎么样？***

*****更漂亮的**允许你自动格式化代码，并使其成为你编写的每个文件的标准，这允许你在同一个项目中轻松地与多个开发者合作。***

***[ESLint](https://eslint.org/) 静态分析你的代码，快速发现问题。***

***我的 makin-cli 支持这两种配置，要将其添加到您的项目中，您只需执行以下操作:***

```
*makin-cli -p -l*
```

***有了回应:***

```
*➜  medium-typescript makin-cli -p -l
[23:44:06] [info]                       _      _                          _   _ 
  _ __ ___     __ _  | | __ (_)  _ __             ___  | | (_)
 | '_ ` _ \   / _` | | |/ / | | | '_ \   _____   / __| | | | |
 | | | | | | | (_| | |   <  | | | | | | |_____| | (__  | | | |
 |_| |_| |_|  \__,_| |_|\_\ |_| |_| |_|          \___| |_| |_|

[23:44:06] [info] Welcome back ;)
[23:44:06] [info] Configuring prettier...
[23:44:06] [info] Installing prettier
[23:44:08] [info] Adding .prettierrc
[23:44:08] [info] Adding format script to package.json
[23:44:08] [info] Configuring lint...
[23:44:08] [info] Installing eslint
[23:44:26] [info] Configuring .eslintrc
[23:44:26] [info] Adding lint script to package.json
➜  medium-typescript*
```

***为了测试它是否工作，我们添加了两个脚本: **format** 和 **lint。*****

```
*➜  medium-typescript npm run format> medium-typescript@1.0.0 format
> prettier --write "src/**/*.ts"src/index.ts 25ms
src/services/hello.service.ts 5ms
➜  medium-typescript npm run lint> medium-typescript@1.0.0 lint
> eslint "{src,apps,libs,test}/**/*.ts" --fix➜  medium-typescript*
```

***随着项目的增长，你可以看到使用 beautiful/lint 的好处，并开始有更多的人来编写代码。***

***感谢阅读到目前为止。如果你碰巧不能复制我的文章，请看看我的[极简 git repo](https://github.com/makinhs/medium-typescript) 中的最终版本。***

***如果这篇文章对你的学习有所帮助，别忘了留下掌声！***

***想了解更多高级内容并学习如何开始构建 GraphQL API 吗？看看我的文章！***

***[](/graphql-backend-in-nodejs-made-easy-with-nestjs-1489be18b994) [## 使用 NestJS 简化 Node.js 中的 GraphQL 后端

### 在本文中，我将向您展示如何以一种非常非常简单的方式开始一个 GraphQL 后端项目…使用 NestJS！

javascript.plainenglish.io](/graphql-backend-in-nodejs-made-easy-with-nestjs-1489be18b994) 

或者，创建一个 REST TypeScript API 怎么样？

[](https://makinhs.medium.com/creating-a-rest-api-series-with-nestjs-part-01-scaffolding-and-basic-cli-usage-30ace19c5bb8) [## 使用 NestJS 创建 REST API 系列—第 1 部分—搭建和基本 CLI 用法

### 欢迎回来！在这个迷你系列文章中，我将指导您如何使用 NestJS 框架构建 REST API

makinhs.medium.com](https://makinhs.medium.com/creating-a-rest-api-series-with-nestjs-part-01-scaffolding-and-basic-cli-usage-30ace19c5bb8) 

回头见！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)***