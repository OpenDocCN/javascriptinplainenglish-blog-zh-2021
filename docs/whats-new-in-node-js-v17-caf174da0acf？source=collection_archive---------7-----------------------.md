# Node.js v17 有什么新功能？

> 原文：<https://javascript.plainenglish.io/whats-new-in-node-js-v17-caf174da0acf?source=collection_archive---------7----------------------->

## Node.js 17 的特性解释。

![](img/11f2a48e74b064eb44cde48878935a0f.png)

[Image source](https://nodejs.org/en/)

流行的 JavaScript 运行时的最新主要版本(v17)刚刚在几周前发布。Node.js 17 已成功添加为**当前**发布线，Node 16 已作为长期支持( **LTS** )。

由于是奇数版本，这个版本将[而不是](https://github.com/nodejs/release)推广到 LTS。尽管是一个相对较小的更新，但这个版本对运行时进行了一些改进，包括更有前途的 API、JavaScript 引擎升级和 OpenSSL 3.0 支持。

在这个博客中，你会发现这次发布的主要亮点！

# 1.新的基于承诺的 API

在最近几个主要的 Node.js 版本中，为`dns`、`fs`、`stream`和`timers`模块添加了基于 Promise 的 API。在 Node.js 17 中，这种混杂工作已经扩展到了`readline`模块，它主要用于接受来自命令行的输入。新的 API 可从`readline/promises`模块访问。

以前，我们习惯对`readline`模块使用回调函数。现在，当从`readline/promises`导入时，您将能够使用`async`

*在节点 v17 之前:*

```
import readline from "readline";
import process from "process";

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.question(`What's your name?`, (name) => {
  console.log(`Hey ${name}!`);
  rl.close();
```

*在节点 v17 之后:*

```
import readline from "readline/promises";
import process from "process";

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

const name = await rl.question(`What's your name?`);
console.log(`Hey ${name}!`);
rl.close();
```

# 2.Node.js 版本将包含在堆栈跟踪中

当调试一个问题时，开发人员的一个常见问题是-*node . js 使用的是什么版本？Node.js 17 通过在堆栈跟踪的末尾包含版本号，使得提供这些信息变得更加容易。*

```
file:///home/harsha/dev/demo/main.mjs:1
throw new Error("Uncaught exception");
      ^

Error: Uncaught exception
    at file:///home/harsha/dev/demo/main.mjs:1:7
    at ModuleJob.run (node:internal/modules/esm/module_job:185:25)
    at async Promise.all (index 0)
    at async ESMLoader.import (node:internal/modules/esm/loader:281:24)
    at async loadESM (node:internal/process/esm_loader:88:5)
    at async handleMainPromise (node:internal/modules/run_main:65:12)

Node.js v17.0.0
```

您可以在启动 Node.js 脚本时使用`--no-extra-info-on-fatal-exception`命令行标志，以便在程序的堆栈跟踪中省略这些信息。

# 3.支持 OpenSSL 3.0

Node.js 17 将对 OpenSSL 1.1.1 的支持扩展到了 [OpenSSL 3.0](https://www.openssl.org/blog/blog/2021/09/07/OpenSSL3.Final/) 。

目标是让 OpenSSL 3.0 中的 API 与以前的 OpenSSL 版本中提供的 API 兼容。但是，由于一些限制以及允许的密钥大小和算法，可能会对生态系统产生一定的影响。

当您的应用程序或其依赖项使用 OpenSSL 3.0 中不允许的算法或密钥大小时，这种影响会反映在 Node.js 17 中的错误消息`ERR_OSSL_EVP_UNSUPPORTED`中。

您可以使用`--openssl-legacy-provider`命令行标志来启用 OpenSSL 3.0 遗留提供者，作为缓解这些限制的临时方法。

# 4.V8 JavaScript 引擎升级到 v9.5

截止 Node.js 17，v8 JavaScript 引擎已经更新到 [v9.5](https://v8.dev/blog/v8-release-95) 。

这将调整应用程序的性能，并增强开发过程的体验。

此版本中的更改主要旨在扩展日期和日历以及时区输出的国际化:

*   `Intl.DisplayNames` API 支持的其他类型
*   `Intl.DateTimeFormat` API 中扩展的`timeZoneName`选项

# 折旧和移除

Node.js 17 还附带了一些[弃用和移除](https://nodejs.org/en/blog/release/v17.0.0/#deprecations-and-removals)。通读一遍以了解更多信息。

# 结论

在这个主要版本之后，Node.js 16 已经被提升到 LTS。这个 LTS 版本包含核心包脚本，它是包管理器和 Node.js 应用程序项目之间的桥梁，应该在开发过程中使用。这将允许用户使用`npm`和`yarn`，而实际上不需要安装它们。这意味着一些功能将会得到长期支持。所以现在是采用 Node.js 16 版本的理想时机，因为即使 Node.js 12 也将在 2022 年退出服务。

嗯，真的应该升级到 [v17](https://nodejs.org/en/download/current/) 吗？虽然它不是 LTS 版本，但它有一些重要的更新，你不能忽视。因此，我将由您来决定是否升级。

感谢阅读！

# 参考

[](https://medium.com/the-node-js-collection/node-js-17-is-here-8dba1e14e382) [## Node.js 17 来了！

### 这篇博客由贝瑟尼·格里戈斯撰写，Node.js 技术指导委员会提供了额外的资料…

medium.com](https://medium.com/the-node-js-collection/node-js-17-is-here-8dba1e14e382) [](https://nodejs.org/en/) [## 节点. js

### Node.js 是基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时。

nodejs.org](https://nodejs.org/en/) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)