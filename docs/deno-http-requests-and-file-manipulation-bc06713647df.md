# Deno — HTTP 请求和文件操作

> 原文：<https://javascript.plainenglish.io/deno-http-requests-and-file-manipulation-bc06713647df?source=collection_archive---------12----------------------->

![](img/ca127db0fe50e2b5765cfd0bd2b2b1a1.png)

Photo by [Viktor Talashuk](https://unsplash.com/@viktortalashuk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Deno 是一个新的服务器端运行时环境，用于运行 JavaScript 和 TypeScript 应用程序。

在本文中，我们将了解如何开始为 Deno 开发应用程序。

# 管理依赖关系

我们可以在 Deno 应用中管理依赖关系。

我们可以用`export`语句重新导出模块:

`math.ts`

```
export {
  add,
  multiply,
} from "https://x.nest.land/ramda@0.27.0/source/index.js";
```

`index.ts`

```
import { add, multiply } from "./math.ts";console.log(add(1, 2))
console.log(multiply(1, 2))
```

我们在`math.ts`转口货物，在`index.ts`进口。

# 取数据

我们可以用带 Deno 的 Fetch API 获取数据。

Fetch API 是用 Deno 实现的。

例如，我们可以写:

```
const res = await fetch("https://yesno.wtf/api");
const json = await res.json()
console.log(json);
```

然后当我们跑的时候:

```
deno run --allow-net index.ts
```

我们会得到这样的结果:

```
{
  answer: "yes",
  forced: false,
  image: "https://yesno.wtf/assets/yes/7-653c8ee5d3a6bbafd759142c9c18d76c.gif"
}
```

记录在案。

`--allow-net`标志在我们的脚本中启用网络通信。

要得到 HTML，我们可以写:

```
const res = await fetch("https://deno.land/");
const html = await res.text()
console.log(html);
```

然后我们从`deno.land` URL 下载 HTML 代码。

为了捕捉错误，我们编写:

```
try {
  await fetch("https://does.not.exist/");
} catch (error) {
  console.log(error.message)
}
```

然后我们记录来自`error.message`属性的消息。

# 读写文件

Deno 附带了一个用于读写文件的 API。

它们有同步和异步两种版本。

获得文件系统的访问权限需要`--allow-read`和`--allow-write`权限。

例如，我们可以写:

`index.ts`

```
const text = await Deno.readTextFile("./people.json");
console.log(text)
```

`people.json`

```
[
  {
    "id": 1,
    "name": "John",
    "age": 23
  },
  {
    "id": 2,
    "name": "Sandra",
    "age": 51
  },
  {
    "id": 5,
    "name": "Devika",
    "age": 11
  }
]
```

然后当我们跑的时候:

```
deno run --allow-read index.ts
```

我们读取 JSON 文件并记录数据。

`Deno.readTextFile`返回一个承诺，这样我们就可以使用`await`。

# 编写文本文件

要写一个文本文件，我们可以使用`writeTextFile`方法。

例如，我们可以写:

```
await Deno.writeTextFile("./hello.txt", "Hello World");
console.log('success')
```

创建`hello.txt`并使用第二个参数中的字符串作为内容。

然后当我们跑的时候:

```
deno run --allow-write index.ts
```

我们也可以使用`writeTextFileSync`方法同步写文本文件。

例如，我们可以写:

```
try {
  Deno.writeTextFileSync("./hello.txt", "Hello World");
  console.log("Written to hello.txt");
} catch (e) {
  console.log(e.message);
}
```

# 读取多个文件

我们可以通过写来读取多个文件:

```
for (const filename of Deno.args) {  
  const file = await Deno.open(filename);
  await Deno.copy(file, Deno.stdout);
  file.close();
}
```

然后当我们运行时:“

```
deno run --allow-read index.ts foo.txt bar.txt
```

我们应该看到打印出的`foo.txt`和`bar.txt`的内容。

我们调用`Deno.open`来打开每个文件。

`Deno.args`有命令行参数，也就是`['foo.txt', 'bar.txt']`。

然后我们调用`Deno.copy`将内容复制到`stdout`。

然后我们用`file.close`关闭文件句柄。

# 结论

我们可以用 fetch API 发出 HTTP 请求，用 Deno 读写文件。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**