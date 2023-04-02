# Web 开发人员:使用 Snowpack 而不是 Webpack

> 原文：<https://javascript.plainenglish.io/web-developers-use-snowpack-instead-of-webpack-70e7b04f7853?source=collection_archive---------9----------------------->

## 为什么您应该通过简化和加速您的开发过程来利用 ES 模块的强大功能

![](img/0a8dc80027445294049bd16a38309a2f.png)

Photo by [NOAA](https://unsplash.com/@noaa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 从后到前？

我必须承认我喜欢把事情简单化。我希望我的后端代码看起来与我的前端代码相似。这意味着在客户端和服务器端都使用现代 javascript (ES6+)。我还希望以同样的方式处理依赖关系，即不要将它们包含在我的 repo 中，而是轻松地导入它们。在服务器端，现在有了 **node.js** 中的 **npm** 和 **ES 模块**支持，这是可能的。在客户端，现在有了浏览器中的 **npm** 、 **ES 模块**支持和 **snowpack** 就可以实现了！

# 服务器

因此，让我们来看看由于 node.js 版本 13.9.0+，我们可以在服务器上做些什么。

请注意。mjs 扩展，这告诉节点我们在 ES 模块土地。现在我们需要做的就是安装 socket.io…

```
npm i socket.io
```

然后，您可以简单地运行它:

```
node server.mjs
```

# 客户

因此，为了在前端实现类似的代码，例如:

我们需要在客户端使用 [Snowpack](https://www.snowpack.dev/) 来完成以上工作…

```
npm i -D snowpack
npm i socket.io-client
```

然后更新您的 package.json 脚本，如下所示:

您现在可以这样做:

```
npm run dev
```

这将启动一个快速的 web dev 服务器，监视您的代码的变化，使 webpack 相形见绌；-).

```
npm run build
```

…将构建到一个静态的**构建**目录中，您可以将它部署到任何地方。

如果你想缩小你的构建，我发现 [Snowpack](https://www.snowpack.dev/) 做得很好，只需添加以下内容:

由于 [Snowpack](https://www.snowpack.dev/) 使用 [esbuild](https://esbuild.github.io/) 捆绑& minify，所以速度极快，这要感谢被写入 [Go](https://golang.org/) ！

# 摘要

Snowpack 是 web 开发未来的一瞥。Webpack 对于小项目来说太复杂，对于大项目来说又太慢，它的日子肯定屈指可数了。Snowpack 对像 [esbuild](https://esbuild.github.io/) 这样的神奇工具的拥抱和 Svelte 对 Snowpack 的拥抱无疑是这一切走向的良好指标。要是我们能跳过使用 [npm](https://www.snowpack.dev/posts/2021-01-13-snowpack-3-0) …嘘 [Deno](https://deno.land/) 就好了。