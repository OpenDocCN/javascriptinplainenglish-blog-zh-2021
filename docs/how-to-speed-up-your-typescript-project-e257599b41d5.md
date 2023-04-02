# 如何加快你的打字稿项目

> 原文：<https://javascript.plainenglish.io/how-to-speed-up-your-typescript-project-e257599b41d5?source=collection_archive---------5----------------------->

## 在你的项目中使用 SWC

![](img/edd1e599bc809487fed78966f5c6779f.png)

Photo by [Mohiuddin Farooqui](https://unsplash.com/@mohifarooqui?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

TypeScript 成为后端(Node.js)和前端(Angular/React)开发的标准。它所带来的类型让我们可以放心地开发应用程序，不会犯任何愚蠢的错误。它并没有解除我们使用最佳编码实践的责任，但是它确实让开发人员的生活稍微轻松了一些。

然而，TypeScript 有一个缺点。现在是编译时间。那么，我们来谈谈如何加快你的 TypeScript 项目。

# 介绍

代码越多，编译的时间就越长。我想我们都同意这一点。在某些情况下，这也是我们将应用程序分成更小的部分(服务)的原因，因此我们不需要编译所有的东西。

这包括:

*   生产就绪集装箱化，
*   类型脚本支持，
*   [扑通](https://plopjs.com/)进行代码生成，
*   内置对 Redis 和 PostgreSQL 的支持，
*   像命令模式或依赖注入这样的最佳实践，
*   REST/graphQL API 支持

…以及更多！

在其原始形式中，运行“npm run watch”命令(在监视模式下启动 TypeScript 编译器 tsc)需要 28 秒来准备好一个环境。

听起来不是很多，但是随着更多代码的出现，这个数字会慢慢增加。那么编译过程中会发生什么呢？

简而言之，有两个主要组成部分:

*   类型检查，
*   转换成 JavaScript

在这一点上，我们不能对第一个做太多，但是，有一种方法可以加快传输部分。

TypeScript 本身不能把 TypeScript 代码改成 JavaScript 文件。没有这样的功能。但是，有一个只允许我们检查类型的标志——no emit 标志。

那么，如果我们对翻译部分使用更快的东西，而只对类型脚本类型检查使用 tsc，会怎么样呢？

# 什么是 SWC？

![](img/322d0de0d2898a1d0ca091fe1495da3f.png)

Photo by [Harley-Davidson](https://unsplash.com/@harleydavidson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

[SWC](https://swc.rs/) 代表超高速 JavaScript/TypeScript 编译器。它是在 Rust 中创建的一个工具，只有一个任务——将代码从 TS/ES 传输到特定的目标。它不会检查类型(至少现在不会)，但正因为如此，它比 TSC 快得多。

我们的样板文件在 7 秒内编译完成。这比使用内置的 TypeScript 工具快 4 倍。那么它是如何工作的呢？

SWC 可以作为标准的 devDependency 与:
`npm i -D @swc/core @swc/cli`一起安装

仅此而已！至少对于一些基本功能来说。🙂

可以通过运行:
`swc <some-directory> --out-dir build`来试试

很快你就能翻译出代码。如果你需要一个监视模式，那么只需要在末尾加上-w 标志。

当然，对于更复杂的项目来说，它会稍微复杂一点。默认情况下，SWC 关闭了大部分功能，对于许多 TypeScript 应用程序，有必要添加额外的配置。

这可以用一种特殊的。swcrc 文件。

```
{  "jsc": {    "parser": {      "syntax": "typescript",      "decorators": true,      "dynamicImport": true    },    "transform": {      "legacyDecorator": true,      "decoratorMetadata": true    },    "target": "es2018",    "keepClassNames": true,    "loose": true  },  "module": {    "type": "commonjs",    "strict": true,    "strictMode": true,    "lazy": false,    "noInterop": true  },  "sourceMaps": "inline"}
```

遗憾的是，目前还没有从 tsconfig 创建 SWC 配置的工具。因此，您应该记住保持两个文件同步。

SWC 配置中有几个有用的键。

第一个是 jsc。这个键包含与我们将要使用的解析器类型相关的所有内容，例如，TypeScript 或 ECMAScript，但也包含一些关于我们希望代码转换到的目标 js 版本的信息。

第二个是模块。这对于 Node.js 应用程序特别有用，因为需要 CommonJS 模块。

显然，这些只是许多可能的配置选项中的几个。其余的可以在 [SWC 配置网站](https://swc.rs/docs/configuring-swc)上随意查看。

# 类型呢？

![](img/19bfb5f8aada2b23a382a575d4913d02.png)

Photo by [elnaz asadi](https://unsplash.com/@elnazasadi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一个问题仍然没有答案。我们会放弃类型检查吗？事实上，SWC 既不关心代码的有效性，也不关心类型。所以实际上我们正在失去使用 TypeScript 的最大理由。搞什么鬼？！别担心，我们不会那么做的。😊

在本文的开头，我提到了 TypeScript 可以通过两种方式工作。它要么生成代码并检查类型，要么只检查类型。那我们就用第二种方法吧！

我们需要的命令很简单:

`tsc -w --pretty --skipLibCheck --noEmit`

然而，我们仍然需要同时运行 SWC 和海训方案。我们可以为此使用一个库(以具有跨操作系统的功能)，或者我们可以同时使用和运行两者。

`swc src --out-dir build/src -w --sync & tsc -w --pretty --skipLibCheck --noEmit`

这种方法的好处是什么？

该应用程序准备在 7s 内开发，同时，我们将获得所有关于代码中可能错误的信息。

我们的应用程序越大，SWC 和 TSC 之间的差异就越大，所以有可能更早开发是一个巨大的优势。

# 结论

![](img/ebd0b2e28caf2a3452dc20832c661767.png)

Photo by [Keenan Constance](https://unsplash.com/@keenangrams?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

那么，问题出在哪里？-你可能会问。

使用 SWC 生成的代码与 TSC 生成的代码略有不同。在某些情况下，这会导致我们的 tsc 工作应用程序出现一些问题。

例如，根据配置，修饰类作为类或对象返回(然而，在 tsc 中，它总是一个类)。这听起来不错，但是如果你的任何一个函数需要一个特定的类型(比如 class)，它就会崩溃。我们在 Awilix 助手类中遇到了这个问题。另一个问题是新功能的支持。SWC 发展得相当快，但它仍然不支持 TSC/Babel 的所有功能。最新的功能列表可以在 [SWC 网站](https://swc.rs/docs/comparison-babel)上找到。但也值得查看 GitHub 问题页面。

## 所以我会推荐使用 SWC 吗？

这里有光明的一面。在 SWC 和海训中心之间来回切换非常容易，所以我们都应该尝试一下。我将对此进行更多的尝试，看看它在更大的项目中有多稳定。然而，在这一点上，我对结果非常满意！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)