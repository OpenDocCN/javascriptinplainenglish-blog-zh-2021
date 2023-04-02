# 为哈比神写一个 LiveReload 插件:启用自动页面重载

> 原文：<https://javascript.plainenglish.io/write-a-livereload-plugin-for-hapi-enable-automatic-page-reloads-7cec2d0c6cdb?source=collection_archive---------23----------------------->

如何为哈比神写一个 LiveReload 插件？

![](img/b6eb983a8d3489538b6bf0129978d175.png)

一段时间以来，我一直想解决的一个问题是缺少一个[的 LiveReload](https://github.com/livereload/livereload-js) 插件来支持[的哈比神](https://hapi.dev/)。如果关闭缓存，在手动重新加载时可以看到模板的变化，但是我已经习惯了用 [Vue](https://vuejs.org/) 开发时自动重新加载。

## 肝叶建筑

完整的肝脏加载协议[可供所有人查看](http://livereload.com/api/protocol/)。简言之，它需要两个部分。

## 计算机网络服务器

LiveReload 服务器接受 HTTP 和 WebSocket 连接(在同一端口上)。它负责为 LiveReload 客户端代码提供服务，并监控文件系统的变化。它还监听来自客户端的指示 URL 更改的消息。

当发生更改时，它会向客户端发送一条消息(通过 WebSocket ),指出哪个文件发生了更改，以便在需要时可以重新加载。

## 客户

客户端在浏览器中运行，它连接到服务器并等待消息。当它收到要求重新加载的消息时，它就会这样做。

(这是一个相当简略的解释……)

我并不打算实际上重新实现客户端——我只是想自动插入导致客户端代码被加载并开始监听的片段。

## 插件结构

哈比神插件似乎是最好的起点。我从以前的工作中了解到，哈比神服务器在[请求/响应生命周期](https://hapi.dev/api/?v=20.1.4#request-lifecycle)中有“扩展点”,可以连接到这些扩展点并用于监控或修改请求或响应。

哈比神插件的基本结构很简单——它是一个导出名为`plugin`的结构的对象，该结构包含名为`register()`的函数(和一些元数据)。注册函数接收一个`server`对象和一个(可选)`options`对象。它做它需要做的事情，然后返回或者抛出一个异常。

下面是一个非常基础的插件。它导出了哈比神在插件中寻找的结构。register 函数创建一个向用户问好的路由，或者如果用户没有指定要问候谁，则创建一个向全世界问好的路由。

```
'use strict';

async function register(server, options = {}) {
  server.route({
    path: "/hello",
    method: "GET",
    handler: function () {
      const name = options.name || "world";
      return `Hello ${name}\n`;
    }
  });
}

module.exports = {
  name: 'hapi-reload',
  version: '0.1.0',
  register: register
};
```

有多种方法来声明你的插件——哈比神的文档很好地涵盖了这一切。现在我们保持简单，把插件代码放在一个名为`plugin.js`的文件中。

我们还需要启动并运行一台服务器，这样我们就有东西可以插入了。

```
const Hapi = require("@hapi/hapi");
const hapiLivereload = require("./plugin");

async function run() {
  const serverOpts = {
    port: process.env.PORT || 4000,
    host: '0.0.0.0'
  };
  const server = Hapi.server(serverOpts);

  await server.register({
    plugin: hapiLivereload
  });
  return server.start();
}

run()
  .then(() => console.log("Server up"))
  .catch(err => console.error("Couldn't run", err));
```

而且——这很有效。

```
$ node dev/server.js
Server up$ curl http://localhost:4000/hello
Hello world
```

我们可以添加`name`选项来定制响应。

```
await server.register({
    plugin: hapiLivereload,
    options: {
      name: "Paul"
    }
  });
```

现在它认识我了！

```
$ curl http://localhost:4000/hello
Hello Paul
```

## 用哪个挂钩？

所以这是一个基本的插件，但它没有做任何特别有用的事情——你可能会想到更简单的方式来说“你好，世界”。

让我们再次开始查看请求生命周期。浏览步骤列表，`onPreResponse`看起来不错——响应已经生成，但尚未传输，更好的是:

> request.response 中包含的响应可能会被修改(但不会被赋予新值)。若要返回不同的响应类型(例如，用 HTML 响应替换错误)，请返回新的响应值。

让我们尝试一种新的方法——而不是特定的路线来问候用户，让所有的*响应都这样做。友好多了。*

```
async function register(server, options = {}) {
  server.ext({
    type: 'onPreResponse',
    method: function(request, h) {
      const name = options.name || "world";
      console.log(`Replacing "${request.response.source}"`);
      return `Hello ${name}\n`;
    }
  });
}
```

`console.log`向我们展示了我们正在替换什么(对调试有用)；我们只需返回我们想要的新回复文本，医生说这应该可以。

为了测试它，我们需要一条*不返回`Hello world`的路线。我们可以将它添加到我们的服务器代码中的`run()`。*

```
server.route({
    path: "/",
    method: "GET",
    handler: () => "I should be an index page\n"
  })
```

如果我们尝试一下呢？

```
Server up
Replacing "I should be an index page
"$ curl http://localhost:4000/
Hello Paul
```

太棒了。

## 肝负荷寄存器

livereload 插件的`register`功能基本上是一样的。差异是特定于插件的，计算出客户端代码的位置。

```
const logger = require("util").debuglog("hapi-livereload");

let host, port, src;

async function register(server, options = {}) {
  host = options.host || "localhost";
  port = options.port || 35729;
  src = options.src || '//' + host + ':' + port + '/livereload.js?snipver=1';

  server.ext({
    type: 'onPreResponse',
    method: addSnippet
  });
}
```

我们还没有涉及到的是`addSnippet`函数，这是事情变得更复杂的地方——实际上是修改返回的网页。

我们还使用 Node 的标准`[util.debuglog](https://nodejs.org/api/util.html#util_util_debuglog_section_callback)`功能添加了一个`logger`功能，因此如果用户需要，我们可以向他们报告。

## 修改 HTML

我花了一些时间寻找一个 HTML 解析器。事实上，插件不仅需要解析输出的 HTML 页面，而且我们还必须能够修改它并将其作为文本发送出去，这使得事情变得复杂。

幸运的是，我最终偶然发现了喜马拉雅山，这非常适合我的工作。它将 HTML 文档转换成 JSON 对象，因此这个文档:

```
<div class='post post-featured'>
  <p>Himalaya parsed me...</p>
  <!-- ...and I liked it. -->
</div>
```

变成了这个 JSON:

```
[{
  type: 'element',
  tagName: 'div',
  attributes: [{
    key: 'class',
    value: 'post post-featured'
  }],
  children: [{
    type: 'element',
    tagName: 'p',
    attributes: [],
    children: [{
      type: 'text',
      content: 'Himalaya parsed me...'
    }]
  }, {
    type: 'comment',
    content: ' ...and I liked it. '
  }]
}]
```

(示例摘自 Github 页面。)

除了`parse`之外，还有一个`stringify`方法，它将 JSON *转换回*为 HTML。完美。

这是一个比我开始时意识到的更大的问题。对于大问题，我发现最好的办法是分解它们，如下图所示。

```
function addSnippet(request, h) {
  // Is it HTML? If not, we can't work with it.
  // Can we parse it?
  // If we can parse it, does it have a HTML tag as it should?
  // And is there a 'head' element we can attach our script to?
  // Did someone already add a livereload script to it?
  // Add the script to the 'head' element
  // Convert back to HTML and return it
}
```

这看起来是一个可管理的分解，所有的单个部分看起来并不具有挑战性。让我们来解决它们。

## 我们能处理回复吗？

这里我们采用简单的方法——我们假设[的哑剧类型](https://webplatform.github.io/docs/concepts/Internet_and_Web/mime_types/)是正确的，并检查`text/html`。

```
function isHtml(response) {
  return response.contentType?.indexOf("text/html") >= 0;
}
```

## 我们能解析它吗，它有正确的节点吗？

我们最终要搜索相当多的节点，所以让我们有一个方便的函数。

```
function findNode(nodes, name) {
  return nodes.find(node => node.tagName === name);
}
```

这样，我们的解析/检查代码可以写成如下。我们试图解析它；如果我们可以解析它，我们就寻找`html`元素。如果存在，我们就寻找*的子元素*，它是`head`元素。

注意——我们在这里使用`h.continue`。这向哈比神表明，我们对这个回应没什么可说的，继续下一个话题。

```
const doc = parse(response.source);
  if (!doc || doc.length == 0) {
    logger("Couldn't parse", response.source);
    return h.continue;
  }

  const htmlNode = findNode(doc, "html")
  if (!htmlNode) {
    logger("Couldn't find HTML tag", response.source);
    return h.continue;
  }

  const headNode = findNode(htmlNode.children, "head");
  if (!headNode) {
    logger("Couldn't find HEAD tag", response.source);
    return h.continue;
  }
```

## 已经有剧本了吗？

从技术上讲，脚本可以在页面的任何地方。我们不希望只搜索整个网页——其中可能有大量的节点。所以我们将简化我们的问题，只检查`head`中的脚本，这是它最有可能出现的地方。

为此，我们需要:

1.  找到`head`节点的所有子节点，
2.  它们是脚本节点，
3.  带有`src`属性
4.  并检查`livereload.js`的`src`值

步骤 1 很简单— `head.children`。剩下的 3 个步骤可以重写为——对于每个节点，如果它是一个`script`节点，检查`src`属性和`src`值。如果`src`值包含`livereload.js`，那么脚本已经被添加。

```
function reloadExists(nodes) {
  let found = false;

  nodes.forEach(node => {
    if ((node.type === 'element') && (node.tagName === 'script')) {
      const reloadAttribs =
        node.attributes
            .filter(node => node.key === 'src')
            .filter(attr => attr.value?.indexOf('/livereload.js') >= 0);
      found = reloadAttribs.length > 0;
    }
  })

  return found;
}
```

## 添加脚本

我们需要添加一个`script`节点来加载客户端脚本。我们将把它设为`[async](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attributes)`，这样它就不会减慢网站的其他加载速度。

由于我们使用的是 JSON，这现在相对容易了——我们将一个新节点推到现有的`head`子节点上。

```
headNode.children.push({
    type: 'element',
    tagName: 'script',
    attributes: [{ key: 'src', value: src }, { key: "async", value: null }, { key: "defer", value: null }],
    children: []
  })
```

## 转换回 HTML

最后一步，我们从钩子返回新的 HTML，这样哈比神将使用它作为响应。喜玛拉雅让这变得简单:

```
return stringify(doc);
```

## 把它们放在一起

我们现在可以从上面充实我们的`addSnippet`框架，用实际代码替换注释。

```
function addSnippet(request, h) {
  logger("Processing response for", request.info.id);

  // Less typing.
  const response = request.response;

  if (!isHtml(response)) {
    logger("Response isn't HTML, skip it.");
    return h.continue;
  }

  const doc = parse(response.source);
  if (!doc || doc.length == 0) {
    logger("Couldn't parse", response.source);
    return h.continue;
  }

  const htmlNode = findNode(doc, "html")
  if (!htmlNode) {
    logger("Couldn't find HTML tag", response.source);
    return h.continue;
  }

  const headNode = findNode(htmlNode.children, "head");
  if (!headNode) {
    logger("Couldn't find HEAD tag", response.source);
    return h.continue;
  }

  if (reloadExists(headNode.children)) {
    logger("Snippet already exists, skip.");
    return h.continue;
  }

  headNode.children.push({
    type: 'element',
    tagName: 'script',
    attributes: [{ key: 'src', value: src }, { key: "async", value: null }, { key: "defer", value: null }],
    children: []
  })

  logger("Processing done for", request.info.id);
  return stringify(doc);
}
```

## 尝试一下

为了测试它，我们需要一个实际服务于 HTML 文件的路由——没有什么特别的，所以我们可以很容易地看到代码是否被添加了。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Home Page</title>
</head>
<body>
<header><h1>Hello from Hapi!</h1></header>
<main>
    <p>This is a paragraph</p>
    <p>This is still also a paragraph.</p></main>
</body>
</html>
```

我们将改变我们的`/`路线来提供服务。假设`html`变量包含 HTML 页面:

```
server.route({
    path: "/",
    method: "GET",
    handler: (request, h) => h.response(html)
  })
```

尝试一下:

```
<!doctype html>
<html lang='en'>
<head>
    <title>Home Page</title>
<script src='//localhost:35729/livereload.js?snipver=1' async defer></script></head>
<body>
<header><h1>Hello from Hapi!</h1></header>
<main>
    <p>This is a paragraph</p>
    <p>This is still also a paragraph.</p></main>
</body>
</html>
```

就在那里！你可以看到 HTML 看起来和以前完全不一样——例如,`doctype`的大小写被改变了——但是它有相同的语义。

## 结论

## 好的…

我还没有对它进行过大量的测试，但是这种方法似乎适用于普通的 HTML 文件。

实现起来并不难——哈比神提供了我们融入请求/响应生命周期所需要的一切，喜马拉雅库正好提供了我们处理 HTML 所需要的东西(如果没有它，事情会变得困难得多)。

## …还有“哎呀”

然而……当我把它和我正在做的项目整合在一起时，我发现它不能和 Vision 一起工作。`source`元素不是一个呈现的页面，它是一个数据结构，大概对 Vision 有意义。

在这一点上，我做了之前应该想到的事情——我将 JavaScript 放在由 Vision 呈现的头部分中。一旦我做到了这一点，我就不需要插件就可以运行 livereload 了。

因此，从“让肝脏加载工作”的角度来看，这实际上是一个相当无意义的工作。不过，这仍然是一次有用的经历，我从中吸取了教训。所以它并没有被浪费掉，只是有点“doh！”瞬间。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)