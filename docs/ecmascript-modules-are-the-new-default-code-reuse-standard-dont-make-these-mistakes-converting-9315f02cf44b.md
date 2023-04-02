# 在转换 Node.js 应用程序时不要犯这些错误

> 原文：<https://javascript.plainenglish.io/ecmascript-modules-are-the-new-default-code-reuse-standard-dont-make-these-mistakes-converting-9315f02cf44b?source=collection_archive---------11----------------------->

## ECMAScript 模块是新的默认代码重用标准

![](img/0e3bc02373962e781b9b8065aa8b2fe3.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

ECMAScript 模块是封装 JavaScript 代码以供将来重用的官方标准格式。Es6 模块现在在 Node.js 12 和更高版本中得到完全支持，所以是时候开始使用它们了。

到目前为止，JavaScript 开发人员和节点库通常将 commonjs 用于模块。如果您在过去几年中使用过 typescript，您将会熟悉应用程序中的模块导入语法。大多数 typescript 应用程序不使用 commonjs `require(“module”)`，而是使用某种变体的`import module from “module”`。

然后，Typescript 会将这个导入语法转换成 commonjs require 语句。这一步在现代 Node.js 应用程序中是不必要的。你可以在你的编译代码中直接使用`import module from “module”`。

如果你使用 typescript，你可以修改你的 **tsconfig** 设置来输出 ECMAScript (ES6)模块，这样就可以了。如果你不使用 typescript，如果你想更新你的应用程序，你可能需要做一些重写。

当我升级 Node.js 应用程序以使用 ECMAScript 模块(如配置 typescript、设置 jest、正确配置 package.json 等)时，我花了一些时间和调查来找出这些问题的解决方案。

# 对 ECMAScript 6 (ES6)模块的 Node.js 支持

从 Node.js 14 开始，对 ECMAScript 模块的支持是稳定的。因此，使用该功能没有任何问题。

如果你还在生产中使用 Node.js 12(这个我是有罪的！)，那么 ECMAScript 模块特性将被标记为“实验性的”,因此您应该谨慎使用。但是支持是完全存在的。请注意，Node.js 12 即将停止使用，需要来自 *2022/04/30* 的支持。因此，您应该考虑升级到 Node.js 14。

当然，如果您提供了一个其他应用程序依赖的库，那么留意您的客户支持的 Node.js 版本是值得的。

一般来说，截至 2021 年，大多数积极开发的 Node.js 应用程序都应该原生支持 ECMAScript 模块。

# package.json 类型属性

在 Node.js 中使用 ECMAScript 模块有两种主要方式。您可以在文件中使用`.mjs`后缀，或者在 package.json 中设置`type: "module"`属性。在使用 TypeScript 时，`.mjs`后缀实际上并不相关或不实用，因此在 package.json 文件中设置 type 属性更容易。

考虑下面的示例 package.json 文件类型，注意我已经显式地将`type`设置为 module。

```
"name": "shared-api-client",
  "version": "1.0.0",
  "description": "OpenAPI client for shared-api-client",
  "author": "OpenAPI-Generator",
  "main": "./dist/index.js",
  "typings": "./dist/index.d.ts",
  "type": "module",
```

这**非常重要**，因为它告诉你的包的消费者从你的代码中加载模块作为 ECMAScript 模块，而不是 CommonJS 模块。

如果您发现您发布的模块有一个问题，某个工具不能正确地从其中导入模块，那么您可能没有设置 type 属性，其他 Node.js 工具会认为您希望通过 CommonJS 加载模块。它们会断裂。

例如，如果您已经配置了实验模块，您可以让 Jest 本机使用 ES6 模块。

但是如果你的包使用导入/导出，而你没有告诉 Jest 这个包使用的是 ES6 模块，那么它会尝试把它作为 CommonJS 加载，Jest 就会崩溃。您将得到一个错误: *Jest "SyntaxError:意外的令牌导出。"*

如果您要发布一个包含 ECMAScript ES6 模块的包，请记住设置`type: "module"`。

# 使用顶级 await(在 TypeScript 中)

await 通常在异步函数中调用。没有办法在函数之外拥有一个。这里有一个例子:

```
import fs from 'fs/promises'
// this is ok because it's in an async function
const myFunc = async () => {
  await fs.readFile('path')
}

// this fails to compile in tsc because it is at the top level of a module
await fs.readFile('path')

// just to make this a module
export {}
```

但是函数中没有等待的真实用例。

特别是，如果您正在为 Jest 测试设置资源，您可能有一个 Jest 在开始运行测试之前运行的设置文件。

```
import dotenv from 'dotenv'

import { AuthenticatedRequests } from './commonDataModels/AuthenticatedRequests'
dotenv.config()

// async function that gets a valid auth token from a third party service so we can build requests
await AuthenticatedRequests.setToken()

export {}
```

您可以通过在`setToken()`方法中使用`.then()` promise 语法来避免使用`await`，并使其成为一个同步方法。但是我更喜欢尽可能使用 async/await。

如果你正在用一个顶层的`.mjs`文件编写一个本地节点模块，await 应该很适合你。

如果您是在 TypeScript 中编写的，那么您必须将 **tsconfig** 中的模块选项设置为“ **esnext** ”(在编写本文时)。我将在另一节描述如何配置 TypeScript。

# 将 CommonJS 模块导入 ES6 模块

现在你的目标是 ES6 或更高版本，你不能再在自己的模块中使用任何 CommonJS 模块。您必须使用`import`语法导入它们。

TypeScript 和 Node.js 都为此提供了互操作性。我来描述一下打字稿的那个。

大多数导入 CommonJS 模块的 TypeScript 应用程序应该在它们的 **tsconfig** 文件中打开`esModuleInterop`。那你就用一个【正常】`import`就可以了。

旧的 TypeScript CommonJS 互操作以违反 ES6 标准的方式处理 CommonJS 导入。EsModuleInterop 对 TypeScript 编译器进行了一些更改，以更好地处理这些问题。这些问题在 TypeScript 文档[中有所描述。](https://www.typescriptlang.org/tsconfig#esModuleInterop)

```
// this imports the default export from a commonjs module.
import dotenv from 'dotenv'

// this imports default and any named exports on module.exports
import * as dotenv from 'dotenv'
// you could access dotenv.default here
// or const postConfig = dotenv() (dotenv module doesn't export a function on exports but this is just an example)
```

# 变量 __filename 和 __dirname 在 ECMAScript ES6 模块中不可用

当您尝试使用这些特殊变量中的一个时，如果您使用 ECMAScript 模块，您将得到错误*“reference error:_ _ filename is not defined”*。

这是因为当 Node.js 在 ECMAScript ES6 模块模式下运行时，它们根本不可用。在`import.meta.`中，有一种替代方法可以让您获得当前的工作目录。以下是使用方法。

```
console.log(import.meta.url)
// returns where the module (usually the file) is located e.g. file:///Users/me/personal-projects/blog/e2e-backend/src/preRun.ts

// and how to get a string file path
console.log(new URL('./new-file-path.json', import.meta.url).pathname)
// returns e.g. /Users/me/personal-projects/blog/e2e-backend/src/new-file-path.json
```

Node.js 文档建议您可以直接为`fs`方法提供一个`URL`实例，但是我在应用程序中使用的类型需要传递一个字符串。所以，这就是我将 URL 的`.pathname`属性传递给`fs`方法的原因。

我怀疑这个打字问题将在 Node.js 类型的新版本中得到解决，因此您可能能够在应用程序中传递 URL 而无需读取路径名。

```
// this works on my application with installed Node.js types
const contents = fs.readFileSync(
  new URL('./new-file-path.json', import.meta.url).pathname
)

// this is how the Node.js docs suggest using URL with fs methods but this did not
// pass with my typescript Node.js types
const contents = fs.readFileSync(
  new URL('./new-file-path.json', import.meta.url)
)
```

# 为 ECMAScript ES6 模块配置 TypeScript

您需要设置您的 TypeScript 配置来支持 ES6 模块特性。我将假设您使用的是 TypeScript 4 或更高版本。

如果您使用的是 Node 14 和更高版本，您可以访问 ES2020 上的所有可用功能，没问题。您可以使用这些库，也可以将它们作为输出目标。

如果你只想使用 ECMAScript ES6 模块，并且不需要使用顶级 await，那么你可以使用`es2020`模块。这可以通过以下方式完成:

```
{
  "compilerOptions": {
    "lib": ["es2020"],
    "module": "es2020",
    "target": "es2020",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "allowSyntheticDefaultImports": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

如果您还想使用顶级 await，那么在撰写本文时，您需要像这样将模块选项设置为`esnext`。

`esnext`旨在包含实验特性，因此您可能不想在生产中使用它。

顶级等待很可能在将来被添加到一个永久的模块配置中。因此，如果你来自未来，并且正在阅读这篇文章，请查看 TypeScript 文档以获得对顶级 await 的支持！

```
{
  "compilerOptions": {
    "lib": ["es2020"],
    "module": "esnext",
    "target": "es2020",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "allowSyntheticDefaultImports": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

我个人的观点是，在目前的写作阶段，拥有顶级等待是很好的，但是在生产运行时环境中通常有需要它们的方法。不过，我确实在每天运行的开发工具中使用它们。

如果您使用的是 Node.js 12，这是您应该使用的 TypeScript 配置:

```
{
  "compilerOptions": {
    "lib": ["es2019", "es2020.promise", "es2020.bigint", "es2020.string"],
    "module": "esnext",
    "target": "es2019",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "allowSyntheticDefaultImports": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

重要的是要注意，你需要替换的`__filename`的`import.meta`属性只在 ES2020 模块或更高版本中可用( **esnext** 也会有)。

# 为 ECMAScript ES6 模块配置 Jest 和 TypeScript

如果你想用 TypeScript 在 Jest 中使用 ES6 模块，我推荐使用 **ts-jest** 预置，并打开 **useEsm** 。

```
npm i --save-dev ts-jest
// or
// yarn add -D ts-jest

{
  "preset": "ts-jest",
  "roots": ["<rootDir>/src"],
  "extensionsToTreatAsEsm": [".ts"],
  "testRegex": ".e2e-spec.ts$",
  "setupFiles": ["<rootDir>/src/preRun.ts"],
  "globals": {
    "ts-jest": {
      "useESM": true
    }
  }
}
```

现在，当你调用 Jest 时，告诉它使用 ES6 模块。

```
"test" : "NODE_OPTIONS=--experimental-vm-modules npx jest"
```

# 在 TypeScript 中使用 node: schema

Node.js 模块实现支持模式。导入的“from”部分实际上是一个 URL！并且节点缓存也这样对待它。一个非常有趣的模式是`node:`模式，因此您可以清楚地知道这个导入是一个节点模块，而不是一个定制的应用程序模块。

```
import fs from 'node:fs'
```

目前(2021 年 6 月)这个模式有一个问题，Node.js 类型的维护者试图添加这个模式，但它导致了 CommonJS 导入的问题。所以，他们恢复了加法。

现在，您不能将节点模式与 TypeScript 和 Node.js 类型一起使用。

我相信这个问题将来会得到解决，但是为了让你不要浪费时间去解决它，我想我应该分享一下调查结果！

# 结论

ECMAScript 模块就在这里，随时可以使用！

出于向后兼容性的考虑，在您的浏览器 web 应用程序中使用它们还需要一段时间，但是在 Node.js 中，我们控制运行时，所以现在就开始使用它们。

通过对 TypeScript 进行一些配置更改，您可以停止将 ES6 模块移植到 CommonJS 中，如果需要的话，您将获得一些新的有用特性。

如果您有任何问题，可以通过 Twitter 联系我[！](https://twitter.com/darraghor)

![](img/467d203c246f32851b7b8ae0da31744f.png)

*原载于*[*https://www.darraghoriordan.com*](https://www.darraghoriordan.com/2021/06/26/publishing-package-using-esm-esmodules/)*。*

*更多内容看* [***说白了***](http://plainenglish.io)