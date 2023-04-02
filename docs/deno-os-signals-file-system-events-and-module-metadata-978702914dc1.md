# Deno —操作系统信号、文件系统事件和模块元数据

> 原文：<https://javascript.plainenglish.io/deno-os-signals-file-system-events-and-module-metadata-978702914dc1?source=collection_archive---------10----------------------->

![](img/8baf58271e9d2618a8aca42b3944c101.png)

Photo by [Zeke Tucker](https://unsplash.com/@zeketucker?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Deno 是一个新的服务器端运行时环境，用于运行 JavaScript 和 TypeScript 应用程序。

在本文中，我们将了解如何开始为 Deno 开发应用程序。

# 处理操作系统信号

我们可以用`Deno.signal`方法处理信号。

例如，我们可以写:

`index.ts`

```
console.log("Press Ctrl-C");
for await (const _ of Deno.signal(Deno.Signal.SIGINT)) {
  console.log("interrupted!");
  Deno.exit();
}
```

如果我们按 Ctrl+C，我们将触发`sigint`信号来中断程序。

我们用 for-await-of 循环来观察信号。

`Deno.Signal.SIGINT`是`sigint`信号的对象。

我们调用`Deno.exit`退出程序。

我们通过运行以下命令来运行程序:

```
deno run --unstable index.ts
```

还有，我们可以把它写成承诺。

例如，我们可以写:

`index.ts`

```
console.log("Press Ctrl-C to end the program");
await Deno.signal(Deno.Signal.SIGINT);
console.log("interrupted!");
Deno.exit();
```

观察`sigint`信号。

# 停止观察信号

我们可以通过调用`sig.dispose`方法来停止观察信号。

例如，我们可以写:

`index.ts`

```
const sig = Deno.signal(Deno.Signal.SIGINT);
setTimeout(() => {
  sig.dispose();
  console.log("No longer watching SIGINT signal");
}, 5000);console.log("Watching SIGINT signals");
for await (const _ of sig) {
  console.log("interrupted");
}
```

在`setTimeout`回调。我们调用`sig.dispose`方法来停止观察`sigint`信号。

调用`sig.dispose`时，for-await-of 循环在 5 秒后退出。

# 文件系统事件

我们可以用`Deno.watchFs`方法观察文件系统事件。

例如，我们可以写:

`index.ts`

```
const watcher = Deno.watchFs(".");
for await (const event of watcher) {
  console.log(event);
}
```

我们用`Deno.watchFs`观看脚本所在的文件夹。

我们从`event`对象中获取事件。

然后我们就像这样:

`index.ts`

```
{ kind: "create", paths: [ "/home/runner/IntelligentWorthwhileMice/./lock.json" ] }
{ kind: "modify", paths: [ "/home/runner/IntelligentWorthwhileMice/./lock.json" ] }
{ kind: "access", paths: [ "/home/runner/IntelligentWorthwhileMice/./lock.json" ] }
{
  kind: "create",
  paths: [ "/home/runner/IntelligentWorthwhileMice/./.3s18gah600nwj.foo.txt~" ]
}
{
  kind: "access",
  paths: [ "/home/runner/IntelligentWorthwhileMice/./.3s18gah600nwj.foo.txt~" ]
}
{
  kind: "modify",
  paths: [ "/home/runner/IntelligentWorthwhileMice/./.3s18gah600nwj.foo.txt~" ]
}
{ kind: "modify", paths: [ "/home/runner/IntelligentWorthwhileMice/./foo.txt" ] }
{
  kind: "modify",
  paths: [
    "/home/runner/IntelligentWorthwhileMice/./.3s18gah600nwj.foo.txt~",
    "/home/runner/IntelligentWorthwhileMice/./foo.txt"
  ]
}
```

已显示。

然后我们可以运行它:

```
deno run --allow-read index.ts
```

监视文件夹中的任何文件系统事件。

# 模块元数据

我们可以用`import.meta`属性获得模块元。

例如，我们可以写:

```
console.log(import.meta.url);
console.log(Deno.mainModule);
console.log(import.meta.main);
```

然后我们会看到这样的情况:

```
file:///home/runner/IntelligentWorthwhileMice/index.ts
file:///home/runner/IntelligentWorthwhileMice/index.ts
true
```

当我们运行时，从控制台输出:

```
deno run --allow-read --unstable index.ts
```

`import.meta.url`和`Deno.mainModule`都得到模块的路径。

如果是入口点模块,`import.meta.main`返回`true`。

# 结论

我们可以用 Deno 处理 OS 信号，获取模块元数据，观察文件系统事件。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**