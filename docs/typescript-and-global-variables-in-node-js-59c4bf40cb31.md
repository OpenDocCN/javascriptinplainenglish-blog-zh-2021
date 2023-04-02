# Node.js 中的 TypeScript 和全局变量

> 原文：<https://javascript.plainenglish.io/typescript-and-global-variables-in-node-js-59c4bf40cb31?source=collection_archive---------1----------------------->

## 如何使用 TypeScript *和*制作 Node.js 中的全局变量确保类型正确。

![](img/f1801930494bfd9533e0399f99faa256.png)

Photo by [Blake Connally](https://unsplash.com/@blakeconnally?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**先决条件:**应该已经安装了 VSCode 和 TypeScript。

**TL；**博士——这是一个工作项目:[空](https://github.com/tomnil/emptyts)。

# 声明全局变量

在项目的根目录下创建一个名为`global.d.ts`的文件，内容如下。请注意:

*   使用`var`，这是工作所必需的(参见[typescriptlang.org](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#type-checking-for-globalthis)了解相关信息)。
*   没有了`export {}`，所有的变量都会变成`any`

```
declare global { var Config: {
        Foo: string;
    }; var Foo: string;
}export { };
```

在`index.ts`文件中，尽量使用变量:

```
global.Config = { Foo: "Bar" };global.Foo = "Bar";
```

# 用 TypeScript 编译

确保`tsconfig.json`有适合`include`和`exclude`的部分。示例如下:

```
"include": [
    "src/**/*.ts",
  ],
  "exclude": [
    "node_modules",
    "<node_internals>/**",
    "bin/**"
  ]
```

接下来，只需编译(从终端)。一切都会好的。

```
tsc -b -v
```

# 从终端运行

```
node -r ts-node/register/transpile-only src\index.ts
```

# 在 VSCode 中运行

用这个`launch.json`(或者复制配置)。按`F5`键，或者通过调出命令面板(ctrl-shift-p)并搜索“选择并开始调试”来选择并启动`Debug typescript`配置。

```
{
 // Detailed docs:
 // [https://code.visualstudio.com/docs/nodejs/nodejs-debugging](https://code.visualstudio.com/docs/nodejs/nodejs-debugging)
 "version": "0.2.0",
 "configurations": [
  {
   "name": "Debug typescript",
   "type": "node",
   "request": "launch",
   "smartStep": false,
   "sourceMaps": true,
   "args": [
    "${workspaceRoot}/src/index.ts"
   ],
   "runtimeArgs": [
   "-r",
    "ts-node/register/transpile-only"
   ],
   "cwd": "${workspaceRoot}",
   "protocol": "inspector",
   "internalConsoleOptions": "openOnSessionStart",
   "env": {
    "TS_NODE_FILES": "true" // Respect include/exclude in tsconfig.json => will read declaration files  (ts-node --files src\index.ts)
   },
   "skipFiles": [
    "<node_internals>/*",
    "<node_internals>/**",
    "<node_internals>/**/*",
    "${workspaceRoot}/node_modules/**",
    "${workspaceRoot}/node_modules/**/*"
   ],
   "outputCapture": "std",
   "stopOnEntry": false
  }
 ]
}
```

# 初始化全局变量

在下面这段代码中，我们将设置一个全局记录器并初始化它。同样，变量*必须*使用`var`才能工作。

## 全球. d.ts

```
type Logger = {
    Info: (iMessage: string) => void
}declare global {
    var Foo: string;
    var log: Logger;
}export { };
```

## index.ts

`index.ts`初始化全局记录器，然后开始使用。

注意*初始化*变量需要使用`global.`(或`globalThis.`)，但是*使用它不需要*。示例:

```
import * as Logger from './logger';
import * as expresshelper from './expresshelper'**global.log** = Logger;**log.Info**("Booting system...");
global.Foo = "Bar";
expresshelper.Init();
log.Info("Booting system Complete!");export { }
```

## logger.ts

神奇的伐木工:)

```
console.log("logger is initializing...");export function Info(iMessage: string) {
    console.log(`${new Date().toISOString()} Saving to log: ${iMessage}`);
}
```

## expresshelper.ts

注意`// log.info`，这将在下面讨论。

```
// log.Info("Setting up Express");export function Init() {
    log.Info("Initializing Express.")
}
```

## 开始此代码...

如果运行此代码，将会呈现以下输出(如预期的那样)。

```
logger is initializing...
2021-08-14T08:51:25.620Z Saving to log: Booting system...
2021-08-14T08:51:25.621Z Saving to log: Initializing Express.
2021-08-14T08:51:25.621Z Saving to log: Booting system Complete!
```

## 导入并在文件的根位置定义代码

需要理解的重要一点是，`import`在*运行代码，文件的点被读取*，所以试图取消对`expresshelper.ts`文件中`log.info`的使用的注释会产生这个错误(因为全局变量`log`在`index.ts`中被初始化之前就被使用了)。

```
log.Info("Setting up Express");
^
ReferenceError: log is not defined
```

因此，避免在文件的根使用全局变量的代码。或者完全避免。:)

# 修改另一个模块的全局变量

Express 的示例如下:

## 全球. d.ts

```
import "express";declare global {
    namespace Express {
        interface Request {
            token: string,
            UserID: string
        }
    }
}export { };
```

# 尽情享受吧！:)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)