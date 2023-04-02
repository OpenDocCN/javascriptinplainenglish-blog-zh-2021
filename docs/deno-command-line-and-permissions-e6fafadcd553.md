# Deno —命令行和权限

> 原文：<https://javascript.plainenglish.io/deno-command-line-and-permissions-e6fafadcd553?source=collection_archive---------18----------------------->

![](img/8f8972ba3a805a9e76b5c1f413734d2b.png)

Photo by [Mael BALLAND](https://unsplash.com/@mael_bld?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Deno 是一个新的服务器端运行时环境，用于运行 JavaScript 和 TypeScript 应用程序。

在本文中，我们将了解如何开始为 Deno 开发应用程序。

# 命令行界面

我们可以通过跑步获得帮助:

```
deno help
```

或者:

```
deno -h
```

简称。

我们也可以写:

```
deno --help
```

做同样的事情。

# 脚本参数

我们可以用`Deno.args`属性在脚本中获得命令行参数。

例如，我们可以写:

`index.ts`

```
console.log(Deno.args);
```

然后当我们跑的时候:

```
deno run index.ts a b -c --quiet
```

我们得到:

```
[ "a", "b", "-c", "--quiet" ]
```

从控制台输出。

# 许可

运行需要访问各种资源的代码需要权限。

默认情况下，必须特别启用它们。

以下权限可用:

*   `-A`， `— allow-all` —允许所有权限。这将禁用所有安全性。
*   `— allow-env` —允许环境访问，例如获取和设置环境变量。
*   `— allow-hrtime` —允许高分辨率时间测量。高分辨率时间可用于计时攻击和指纹识别。
*   `— allow-net=<url>` —允许网络访问。我们可以指定一个可选的逗号分隔的域列表，以提供允许域的允许列表。
*   `— allow-plugin` —允许加载插件。请注意—允许插件是一个不稳定的特性。
*   `— allow-read=<allow-read>` —允许文件系统读取访问。我们可以指定一个可选的逗号分隔的目录或文件列表，以提供允许文件系统访问的允许列表。
*   `— allow-run` —允许运行子流程。请注意，子进程不是在沙箱中运行的，因此没有与 Deno 进程相同的安全限制。因此，慎用。
*   `— allow-write=<allow-write>` —允许文件系统写访问。您可以指定可选的逗号分隔的目录或文件列表，以提供允许的文件系统访问的允许列表。

例如，如果我们有一个发出 HTTP 请求的程序，比如:

```
const [url] = Deno.args;
const res = await fetch(url);
const body = new Uint8Array(await res.arrayBuffer());
await Deno.stdout.write(body);
```

我们用以下方式运行它:

```
deno run --allow-net index.ts https://yesno.wtf/api
```

让程序访问互联网。

# 权限 API

我们可以使用`Deno.permissions.query`方法和一个拥有我们想要查询的权限的对象来查询表单权限。

例如，我们可以写:

`index.ts`

```
const desc1 = { name: "read", path: "/foo" } as const;
console.log(await Deno.permissions.query(desc1));const desc2 = { name: "read", path: "/foo/bar" } as const;
console.log(await Deno.permissions.query(desc2));const desc3 = { name: "read", path: "/bar" } as const;
console.log(await Deno.permissions.query(desc3));
```

然后当我们跑的时候:

```
deno run --unstable index.ts
```

我们看到:

```
PermissionStatus { state: "prompt" }
PermissionStatus { state: "prompt" }
PermissionStatus { state: "prompt" }
```

已登录控制台。

我们需要`--unstable`选项来使`Deno.permissions.query`方法可用。

我们可以通过使用`Deno.permissions.revoke`方法来撤销权限:

```
const desc = { name: "read", path: "/foo/bar" } as const;
console.log(await Deno.permissions.revoke(desc));const strongDesc = { name: "read", path: "/foo" } as const;
await Deno.permissions.revoke(strongDesc);
```

然后我们得到:

```
PermissionStatus { state: "prompt" }
```

已显示。

# 结论

我们可以用 Deno 获取和设置权限。

我们可以在脚本中轻松获得命令行参数。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**