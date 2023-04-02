# Deno 独有的特性之一:Web 存储 API

> 原文：<https://javascript.plainenglish.io/deno-web-storage-5fb1401b5f82?source=collection_archive---------4----------------------->

## Node.js 没有这个——如何在 Deno 中使用

![](img/f55b3a496fa2af488f12c9681b6b65b0.png)

Deno 有几个很酷的特性。

在我们已经从 Node.js 了解到的当中，有一些是独家的。Web 存储 API 就是其中之一。Web 存储 API？“我以前听说过，”你现在可能会想。事实上，web 存储 API 在 Web 上是众所周知的。有了它，我们可以使用本地存储或会话存储在浏览器中永久或临时保存值。

正如我在之前[解释的，Deno 旨在提供我们从浏览器知道的窗口对象，甚至在后端。因此，Web 存储 API 也可以在替代节点中使用。下面是我们如何使用它。](/deno-vs-node-js-here-are-the-most-important-differences-62b547443be1)

# 本地存储

本地存储是一个永久的键值存储。对于永久，我的意思是，即使我们关闭并重新启动服务器，我们也可以访问以前保存的值。在 Node.js 中，我们必须使用 Redis 这样的数据库。

由于`localStorage`属于窗口对象，就像在浏览器中一样，我们可以直接访问它。不需要先导入任何东西。

让我们写一个基本的例子:

```
localStorage.setItem("counter", "1")console.log(localStorage.getItem("counter"))
```

运行这段代码时，输出应该是“1”。但是等等，用 Deno 执行总是有点特别。要运行该文件，我们需要提供位置标志。

在浏览器中，每个本地存储条目都链接到一个页面的域(因此存储只能由每个 web 应用程序访问)。但是在后端，我们没有不同的域。为了模拟这种分类，本地存储 API 需要一个我们提供的位置，就像在浏览器中一样。

例如，我们可以使用本地主机:

```
deno run --location [http://localhost/](http://localhost/) index.ts
```

现在，您应该看到“1”出现在终端中。让我们重新运行代码，但先稍微修改一下，看看值是否被持久存储。因此我更改了文件，剩下的唯一一行代码是:

```
console.log(localStorage.getItem("counter"))
```

重新运行代码，就像以前一样，您应该再次看到“1”。该值被永久存储。

为了更新一个值，我们使用带有值的键的`setItem`函数。例如:

```
localStorage.setItem("counter", "2")
```

要清除本地存储，我们可以使用:`localStorage.clear()`

从存储中删除单个键-值对:`localStorage.removeItem("counter")`

# 但是现在的会话存储呢？

现在，让我们来看看非永久性悬挂物。我说手控盒是因为会话存储器使用完全相同的功能。只有两个区别。

首先，我们显然使用了`sessionStorage.<any-function>`而不是`localStorage.<any.function>`。

其次，我们不再需要位置标志，因为我们不会永久保存任何东西。因此，只需使用以下代码运行您的代码:

`deno run index.ts`

就是这样。感谢您的阅读！

关于 Deno 的更多信息:

[](/is-deno-already-dead-661ce807338a) [## 德诺已经死了吗？

### 炒作消失的一些原因

javascript.plainenglish.io](/is-deno-already-dead-661ce807338a) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)