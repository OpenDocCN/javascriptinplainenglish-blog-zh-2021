# 哈比神和 TypeScript—将路线分割成多个文件

> 原文：<https://javascript.plainenglish.io/more-hapi-and-typescript-routes-da37dfc324ca?source=collection_archive---------9----------------------->

[上次我们离开的时候](/using-typescript-with-hapi-73af8cc81118)，服务器只有一个单独的路由，而且都在一个文件里。这是一个不错的开始，但它不完全是可扩展的。让我们从外部文件添加一些路线。

我们将选择类似于传统的“你好世界”的东西。我们会有一个路由，`/hello`，上面会写着“Hello World”。我们还将在“那个”的“下面”增加一条路线，`/hello/name`，它将迎接`name`。

我们这里产生的文件都在 [GitHub repo](https://github.com/arafel/hapi-typescript) 里。

# 测试一下！

当然，由于我们正在添加新的功能，我们知道什么是第一位的…好消息是，这次我们根本不需要做任何设置，我们可以直接使用测试文件。

`test/hello.test.ts`:

```
import { Server } from "@hapi/hapi";
import { describe, it, beforeEach, afterEach } from "mocha";
import { expect } from "chai";

import { init } from "../src/server";

describe("server greets people", async () => {
	let server: Server;

	beforeEach(() => {
		server = await init();
	})
	afterEach(() => {
		await server.stop();
	});

	it("says hello world", async () => {
		const res = await server.inject({
			method: "get",
			url: "/hello"
		});
		expect(res.statusCode).to.equal(200);
		expect(res.result).to.equal("Hello World");
	});

	it("says hello to a person", async () => {
		const res = await server.inject({
			method: "get",
			url: "/hello/Tom"
		});
		expect(res.statusCode).to.equal(200);
		expect(res.result).to.equal("Hello Tom");
	});
})
```

进口产品大同小异。事实上，几乎所有这些都是与`index`测试相同的结构——唯一真正的区别是我们在一个`describe`块中有两个测试。

既然它们如此相似，我就假设这是可以理解的，然后继续。但在此之前，先检查一下它是否失败:

```
server greets people
    1) says hello world
    2) says hello to a person

  smoke test
    ✓ index responds

  1 passing (70ms)
  2 failing
```

好吧，这正是我们所期望的，但失败了。向前…

# 编码吧！

## 路线

同样，这次没有设置工作，只有代码。直入主题—我们希望将这些路线保存在单独的文件中。使用明显的名称…

`src/hello.ts`:

```
import { Request, ResponseToolkit, ResponseObject, ServerRoute } from "@hapi/hapi";

async function sayHello(request: Request, h: ResponseToolkit): Promise<ResponseObject> {
  const name: string = request.params.name || "World";
  const response = h.response("Hello " + name);
  response.header('X-Custom', 'some-value');
  return response;
}

export const helloRoutes: ServerRoute[] = [
  {
    method: "GET",
    path: "/hello",
    handler: sayHello
  },
  {
    method: "GET",
    path: "/hello/{name}",
    handler: sayHello
  }
];
```

好吧，这个有很多我们以前没见过的类型。忽略我们上次遇到的`Request`型，我们刚刚遇到:

*   `[ResponseToolkit](https://hapi.dev/api/?v=20.1.0#response-toolkit)` -如果你没有使用 [Vision](https://github.com/hapijs/vision) 来渲染模板，工具包是你通常用来发送你的响应的东西。您可以生成如上所示的响应。
*   `[ResponseObject](https://hapi.dev/api/?v=20.1.0#response-object)`是`ResponseToolkit`产生的东西——看起来很合理，对吗？里面的很多东西你可以不去管。您可能需要像`[response.code](https://hapi.dev/api/?v=20.1.0#-responsecodestatuscode)`这样的东西来显式设置状态代码。
*   `[ServerRoute](https://hapi.dev/api/?v=20.1.0#route-options)`顾名思义，是在服务器上定义的一条路线。上面的路线非常简单 HTTP 方法、路径和处理它的函数。

在路线定义中，`/hello/{name}`告诉 hapi 在`/hello/`之后捕获路径组件，并将其放在`request.params`对象中。

这就是你所需要做的，在这里你开始看到 hapi 和 Express 之间的一些区别——已经包含和处理了主体/请求解析，包含了电池，不需要插件。这使得使用相同的函数来处理两个路由变得简单。

重要提示—在现实生活中，**不要**简单地获取用户参数并回显它们。使用类似 [Hoek 的 escapeHtml()](https://hapi.dev/module/hoek/api/?v=9.1.1#escapehtmlstring) 的东西。

## 计算机网络服务器

将这些路由插入服务器很简单。导入路线数组:

`src/server.ts`:

```
import { helloRoutes } from "./hello";
```

将其添加到服务器:

```
server.route(helloRoutes);
```

就这样，我们应该完成了。我们当然要知道…

```
$ yarn test
yarn run v1.22.10
$ NODE_ENV=test mocha -r ts-node/register test/**/*.test.ts

  server greets people
    ✓ says hello world
    ✓ says hello to a person

  smoke test
    ✓ index responds

  3 passing (63ms)

✨  Done in 3.05s.
```

完美！