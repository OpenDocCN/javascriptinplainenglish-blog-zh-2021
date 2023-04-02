# 用 Deno 编写服务器端应用

> 原文：<https://javascript.plainenglish.io/getting-started-with-writing-server-side-apps-for-the-deno-runtime-environment-f2a02955c4db?source=collection_archive---------17----------------------->

![](img/38656b091ded7d22ea5e575446236ac4.png)

Photo by [Kamen Atanassov](https://unsplash.com/@katanassov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Deno 是一个新的服务器端运行时环境，用于运行 JavaScript 和 TypeScript 应用程序。

在本文中，我们将了解如何开始为 Deno 开发应用程序。

# 装置

Deno 作为一个单独的可执行文件发布，没有依赖性。

所以我们可以很容易地安装它们。

它可以在多个平台上使用。

我们可以运行以下命令来安装它们:

Shell (Mac、Linux):

```
$ curl -fsSL https://deno.land/x/install/install.sh | sh
```

PowerShell (Windows):

```
$ iwr https://deno.land/x/install/install.ps1 -useb | iex
```

自制软件(Mac):

```
$ brew install deno
```

[巧克力](https://chocolatey.org/packages/deno) (Windows):

```
$ choco install deno
```

[勺](https://scoop.sh/) (Windows):

```
$ scoop install deno
```

使用货物从源头构建和安装

```
$ cargo install deno
```

# 入门指南

要创建 hello world 应用程序，我们可以编写:

```
console.log("hello world");
```

`console`在 Deno 运行时可用。

我们可以通过编写以下代码创建一个简单的服务器应用程序:

```
import { serve } from "https://deno.land/std@0.75.0/http/server.ts";
const s = serve({ port: 8000 });
console.log("http://localhost:8000/");
for await (const req of s) {
  req.respond({ body: "Hello World\n" });
}
```

我们直接从 URL 导入`server`模块。

然后我们调用`serve`来创建我们的服务器。

我们通过循环遍历`s`数组来监听请求，并用`req.respond`发送我们的响应。

现在我们应该在浏览器屏幕上看到“Hello world”。

# 发出 HTTP 请求

我们可以通过编写以下内容来发出 HTTP 请求:

`index.ts`

```
const [url] = Deno.args;
const res = await fetch(url);
const body = new Uint8Array(await res.arrayBuffer());
await Deno.stdout.write(body);
```

然后，我们进入项目，通过运行以下命令来运行它:

```
deno run --allow-net index.ts https://yesno.wtf/api
```

访问网络需要`--allow-net`选项。

`Deno.args`让我们获得命令行参数。

`fetch`让我们用给定的`url`发出 HTTP 请求。

我们通过调用`res.arrayBuffer`解析主体来获得请求。

然后我们用`Deno.stdout.write`将响应写到屏幕上。

# 读取文件

Deno 提供了开箱即用读取文件的方法。

为此，我们写道:

`index.ts`

```
const filenames = Deno.args;
for (const filename of filenames) {
  const file = await Deno.open(filename);
  await Deno.copy(file, Deno.stdout);
  file.close();
}
```

我们从`Deno.args`获取文件路径。

然后我们循环通过`filenames`并调用`Deno.open`来打开文件。

然后我们调用`Deno.copy`将文件内容复制到`stdout`来显示在屏幕上。

当我们完成时，我们调用`file.close`来关闭文件句柄。

当我们奔跑的时候。

```
deno run --allow-read index.ts files/bar.txt files/foo.txt
```

并且假设`files/bar.txt`和`files/foo.txt`存在，那么我们应该看到显示的每个文件的内容。

`--allow-read`标志让我们允许从文件系统中读取文件。

# 结论

我们可以创建简单的服务器端 JavaScript 或 TypeScript 应用程序，并用 Deno 运行时运行它们。