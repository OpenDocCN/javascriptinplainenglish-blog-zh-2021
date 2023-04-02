# Deno —工人、库和模块

> 原文：<https://javascript.plainenglish.io/deno-workers-libraries-and-modules-1cb3ed6c42bc?source=collection_archive---------8----------------------->

![](img/aae6655639d15110d0157665c256492a.png)

Photo by [sol](https://unsplash.com/@solimonster?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Deno 是一个新的服务器端运行时环境，用于运行 JavaScript 和 TypeScript 应用程序。

在本文中，我们将了解如何开始为 Deno 开发应用程序。

# 工人

Deno 支持 web worker API。

例如，我们可以写:

`index.ts`

```
const worker = new Worker(new URL("worker.js", import.meta.url).href, {
  type: "module",
  deno: true,
});
worker.postMessage({ filename: "./log.txt" });
```

`worker.js`

```
self.onmessage = async (e) => {
  const { filename } = e.data;
  const text = await Deno.readTextFile(filename);
  console.log(text);
  self.close();
};
```

`log.txt`

```
hello
```

然后当我们跑的时候:

```
deno run  --unstable --allow-read index.ts
```

我们用`Worker`构造函数创建工人。

我们将 URL 传递给工人。

对象将`type`指定为`'module'`，将`deno`设置为`true`，这样我们就可以运行 worker 了。

`worker.js`有工人。

`self`是 worker 实例。`onmessage`方法通过调用`postMessage`接受传入的消息。

然后我们调用`Deno.readTextFile`方法来读取 worker 中的一个文件。

然后我们应该会看到控制台中记录的`hello`。

# 重新加载模块

默认情况下，Deno 缓存模块，而不提取或重新编译它。

如果我们需要重新加载它们，我们运行:

```
deno cache --reload index.ts
```

重新加载`index.ts`使用的所有东西。

我们还可以通过运行以下命令来重新加载`index.ts`使用的特定模块:

```
deno cache --reload=https://deno.land/std@0.75.0 index.ts
```

如果我们想重新加载`index.ts`使用的多个模块，我们运行:

```
deno cache --reload=https://deno.land/std@0.75.0/fs/copy.ts,https://deno.land/std@0.75.0/fmt/colors.ts index.ts
```

# 锁定文件

Deno 使用一个小的 JSON 文件存储并检查模块的子资源完整性。

`-lock=lock.json`标志启用并指定锁文件检查。

为了更新锁文件，我们运行:

```
--lock=lock.json --lock-write
```

运行应用程序时，我们可以使用 `— -lock=lock.json`选项来检查数据。

# 标准程序库

我们应该运行导入的固定版本，以避免意外的更改。

例如，不要写:

```
import { copy } from "https://deno.land/std/fs/copy.ts";
```

我们应该在导入时包含版本号，方法是:

```
import { copy } from "https://deno.land/std@0.75.0/fs/copy.ts";
```

我们可以使用具有不稳定 Deno APIs 的库。

上面的`copy`模块不稳定，所以要使用它，我们运行:

```
deno run --allow-read --allow-write --unstable main.ts
```

启用不稳定的 API。

# 导入和导出模块

我们可以使用标准的 ES 模块来处理 Deno 应用程序。

例如，我们可以写:

`math.ts`

```
export const add = (a: number, b: number) => a + b;
export const multiply = (a: number, b: number) => a * b;
```

`index.ts`

```
import { add, multiply } from "./math.ts";console.log(add(1, 2))
console.log(multiply(1, 2))
```

我们有`math.ts`，它导出了`add`和`multiply`函数。

然后我们在`index.ts`中使用它们。

# 远程导入

我们也可以直接从远程 URL 导入模块。

例如，我们可以写:

```
import {
  add,
  multiply,
} from "https://x.nest.land/ramda@0.27.0/source/index.js";console.log(add(1, 2))
console.log(multiply(1, 2))
```

我们从`https://x.nest.land/ramda@0.27.0/source/index.js`导入`add`和`multiple`函数。

然后我们可以用同样的方式使用它们。

# 结论

我们可以通过 Deno 直接使用 web workers。

此外，我们可以从各种来源导入模块。