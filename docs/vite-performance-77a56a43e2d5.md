# Vite，这个构建工具可以帮你节省大量的时间

> 原文：<https://javascript.plainenglish.io/vite-performance-77a56a43e2d5?source=collection_archive---------7----------------------->

## JavaScript 快速

## 测试它的 Vue，React 和 Svelte

![](img/2f7423cd00e34e3f6243a6d3ae5030f5.png)

Source: [vitejs.dev](https://vitejs.dev/)

为了构建你的网络应用，有大量的工具。在所有的工具中，有一个特殊的类别:构建工具。这些帮助我们启动我们的开发服务器，并将我们的应用捆绑到生产版本中。一个最近流行的构建工具:Vite。但是它有什么特别之处呢？

Vite 在引擎盖下使用 esbuild。这是一个 JavaScript bundler，用 Go 写的，让它超级快。但是有多快呢？这就是我们将要发现的——使用 Vite，使用 esbuild 作为 React、Vue 和 Svelte 应用程序的构建工具。我用 Vite 为这三种技术设置了一个应用程序，并与它们的默认构建工具/ CLI 进行了性能比较。说到性能，我指的是两件事:

*   启动开发服务器:在浏览器中编辑我们的开发版本需要多长时间。
*   构建生产包。

让我们看看 Vite 是否更快以及快多少——玩得开心！

## 使用 Vite 创建项目

给你留下一些关于 Vite 表现的数据是很酷的。但更酷的是，留给你如何实际使用工具。

```
For npm 6: 
npm init vite@latest my-vue-app --template <template># npm 7+: 
npm init vite@latest my-vue-app -- --template <template>
```

在可供选择的模板中，有“vue”、“react”、“svelte”等。这些是我用过的。

## 基准测试的工作原理

为了公平竞争，我一共做了 6 个应用。一个应用程序，使用默认的构建工具，例如，`create-react-app`使用 React，另一个应用程序使用 Vite 技术。除了 React 之外，我还为 Vue 和 Svelte 做了这个，产生了 6 个不同的项目。

此外，我确保 React、Vue 和 Svelte 应用程序使用相同的代码和相同的依赖版本。

测量开发服务器或构建过程所花费的时间可以通过我刚刚发现的东西来完成:

让我们深入了解一下基准测试的结果。

## 启动开发服务器所需的时间

**React.js:**

*   创建-反应-应用:5.24 秒
*   维特:1.05 秒

**Vue.js:**

*   Vue CLI: 3.75 秒
*   维特:1.07 秒

**苗条:**

*   简单苗条:1.76 秒
*   维特:1.03 秒

## 构建生产包所需的时间

**反应:**

*   创建-反应-应用:4.75 秒
*   维特:2.99 秒

**Vue.js:**

*   Vue CLI: 3.9 秒
*   维特:2.39 秒

**苗条:**

*   简单苗条:1.11 秒
*   Vite: 1.11 秒(是的，完全相同)

如您所见，事实上，在大多数情况下，Vite 要快得多。至少，不存在 Vite 比竞争对手慢的场景。

如果你想了解更多关于 Vite 的知识，请查阅官方文档。

感谢您的阅读！

*更多内容看* [***说白了. io***](http://plainenglish.io/)