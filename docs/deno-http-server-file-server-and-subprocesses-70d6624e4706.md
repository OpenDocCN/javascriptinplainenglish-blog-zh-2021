# Deno — HTTP、服务器、文件服务器和子进程

> 原文：<https://javascript.plainenglish.io/deno-http-server-file-server-and-subprocesses-70d6624e4706?source=collection_archive---------15----------------------->

![](img/a5ac1c3f78b41a7bace6c7786c094323.png)

Photo by [Maksym Kaharlytskyi](https://unsplash.com/@qwitka?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Deno 是一个新的服务器端运行时环境，用于运行 JavaScript 和 TypeScript 应用程序。

在本文中，我们将了解如何开始为 Deno 开发应用程序。

# 简单 HTTP Web 服务器

我们可以用 Deno 提供的`server`模块创建一个简单的 HTTP 服务器。

例如，我们可以写:

```
import { serve } from "https://deno.land/std@0.75.0/http/server.ts";const server = serve({ hostname: "0.0.0.0", port: 8080 });
console.log(`HTTP server running on port 8080`);for await (const request of server) {
  const bodyContent = `Your user-agent is: ${request.headers.get("user-agent") || "Unknown"}`;
  request.respond({ status: 200, body: bodyContent });
}
```

我们导入`serve`函数来创建我们的 HTTP 服务器。

对象有`hostname`和`port`来监听请求。

然后，我们在 for-await-of 循环中创建响应体。

我们通过调用`request.headers.get`来获取标题。

然后我们用 HTTP 状态代码和对象中的主体调用`request.response`，我们用它作为`respond`的参数。

然后，我们可以使用以下命令运行脚本:

```
deno run --allow-net index.ts
```

然后，当我们转到 [http://localhost:](http://localhost:) 8080 时，我们应该会看到类似这样的内容:

```
Your user-agent is: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.111 Safari/537.36
```

# 文件服务器

我们也可以用 Deno 轻松创建一个文件服务器。

为此，我们只需运行:

```
deno run --allow-net --allow-read https://deno.land/std@0.75.0/http/file_server.ts
```

然后，当我们转到 http://localhost:4507/时，我们会看到列出了当前文件夹中的文件。

# TCP 回送服务器

我们可以用`Deno.listen`和`Deno.copy`方法轻松创建一个 TCP echo 服务器。

例如，我们可以写:

```
const listener = Deno.listen({ port: 8080 });
console.log("listening on 0.0.0.0:8080");
for await (const conn of listener) {
  Deno.copy(conn, conn);
}
```

监听 8080 端口。

然后我们遍历`listener`数组来观察请求。

然后我们调用`Deno.copy`将连接数据重定向到入站。

# 创建子流程

我们可以使用`Deno.run`方法创建一个子流程。

例如，我们可以运行:

```
const p = Deno.run({
  cmd: ["echo", "hello"],
});
await p.status();
```

运行`echo hello`。

然后我们可以用`p.status`方法等待它的完成。

我们需要`--allow-run`标志来运行子流程。

我们可以通过使用各种方法从子流程中获得结果并运行它们。

例如，我们可以写:

```
const fileNames = Deno.args;const p = Deno.run({
  cmd: [
    "deno",
    "run",
    "--allow-read",
    "https://deno.land/std@0.75.0/examples/cat.ts",
    ...fileNames,
  ],
  stdout: "piped",
  stderr: "piped",
});const { code } = await p.status();if (code === 0) {
  const rawOutput = await p.output();
  await Deno.stdout.write(rawOutput);
} else {
  const rawError = await p.stderrOutput();
  const errorString = new TextDecoder().decode(rawError);
  console.log(errorString);
}Deno.exit(code);
```

我们调用`status`方法来获取状态代码。

如果代码是 0，我们就写输出。

否则，我们将错误输出到`stderr`。

我们把绳子记录下来。

最后，我们用命令的退出代码调用`Deno.exit`。

# 结论

我们可以创建一个简单的 HTTP 服务器、文件服务器，并使用 Deno 轻松运行子流程。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**