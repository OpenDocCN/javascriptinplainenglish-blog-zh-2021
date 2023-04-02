# 使用平台

> 原文：<https://javascript.plainenglish.io/using-the-platform-instead-of-frameworks-33b4607fc3cc?source=collection_archive---------6----------------------->

## 无框架、无构建的网站:2021 年它们能带你走多远？

![](img/0a2de658c4fe73da66bb0879a14dff02.png)

A still from an animated diagram in [Schematics: A Love Story](https://schematics.elisehe.in), a framework-free website that uses no build tools. Incidentally a metaphor for volatility in JavaScript trends.

我最近看到了 Daniel Kehoe 的一系列文章，介绍了无栈方式(Stackless Way)，这是对 web 开发的一种乐观看法，建议我们“使用平台”(语言内置的现代功能)而不是框架，并构建每隔几年就会被替换的工具。

这是一个好时机——框架疲劳是真实存在的！所以，我没有最终使用 Rollup 来替换我们的一个代码库中的一个古老的 Browserify 版本(它也可以真正使用从 Polymer 到 LitElement 的升级…)，而是决定使用“无堆栈”。我花了很长时间构思了一个动作设计项目，只用浏览器的原生功能构建了它:普通的 JavaScript、ES6 模块和 web 组件。

在一个没有依赖的代码库上工作是一种重新发现我在 2021 年可以免费得到什么的方式，以及我通过将框架、编译器和捆绑器结合在一起所增加的价值。我想分享我在这个过程中学到的东西(以及我需要忘记的东西)。

## 该项目

这个项目本身，[*Schematics:A Love Story*](https://schematics.elisehe.in/)，是一本同名视觉诗集的动画图表集。如果你对详细的实现感兴趣，可以看看 GitHub 上的[库](https://github.com/elisehein/schematics)。

[](https://schematics.elisehe.in) [## 示意图→一个爱情故事

### 朱利安·希巴德的视觉诗集，由伊莉斯·海因制作。

schematics.elisehe.in](https://schematics.elisehe.in) 

# 无堆叠方式

丹尼尔·凯霍并不是唯一一个反对现代网络复杂性的人。弗兰克·奇梅罗的 [*万事开头难*](https://frankchimero.com/blog/2018/everything-easy/) 每次都能打动我，最近，我很享受[这种关于缺乏对普通 JS 欣赏的轻松咆哮](https://medium.com/codex/youre-missing-out-on-vanilla-js-91aceec917d6)。

出于深思熟虑的目的添加外部 JS 依赖项的呼吁已经变得很普遍，但一些思想流派质疑单页面应用程序作为一个整体的概念:毕竟，服务器端呈现仍然是一个东西。页面也可以预先构建到一个完全静态的网站中，并从 CDN 提供服务(参见 [Jamstack](https://jamstack.org/what-is-jamstack/) )。这些方法认识到，我们可以将当前由前端框架管理的一些复杂性转移到堆栈的其他地方。

但是 Kehoe 关于无堆栈的系列文章感觉有点不同。这不仅仅是关于 JavaScript——这是对作为平台的网络原生特性的全心投入(路由？只要确保每个网址匹配一个. html 文件！)

当然，这种纯粹主义是有限度的。对我来说，无堆栈的方式不太现实，更像是一种学习和反省的工具，一种后退一步重新爱上平台的方式。

由于完全是关于动作设计，我自己的项目依赖于许多 a `setTimeout`和页面转换——一个单页应用程序，真的……只是手工制作的。使之成为可能的两个主要技术是 ES6 模块和 web 组件，它们与模块 cdn 一起构成了无堆栈方式的支柱。

# ES6 模块

如果您从事 web 开发已经有一段时间了，您可能还记得这样做:

鉴于 JavaScript 缺乏对本地导入/导出机制的支持，我们只能在文档`<head>`中单独列出所有需要的脚本。这当然不是最理想的:

*   每个脚本标签发起一个 HTTP 请求；
*   没有命名空间(所有脚本都存在于全局范围内)；
*   执行顺序是线性的，直接映射到脚本标签的顺序。

为了解决这个问题，JavaScript 的模块化方法在过去的几年里激增(AMD、UMD、CommonJS)，随之而来的是构建工具和捆绑器来将模块化代码转换成浏览器可以理解的东西。

ECMAScript 模块(也称为 ESM 或 ES6 模块)是 JavaScript 中第一个*本机*模块标准。我在这里强调 *native* ，因为这意味着我们可以抛弃构建工具和捆绑器，而支持 HTML 中的`<script type=“module”>`和 JS 中的`import` / `export`:

**对模块化的原生支持是迈向无构建代码库的最重要的一步。**如果我的余生只能接触到一个 [ES6 特性](http://es6-features.org/)，我相信模块会带我实现结构良好的原生 JavaScript。

不需要构建你的 JS 应用程序是不可思议的。为*原理图*设置目录结构，跳过`npm run build`并看到我的源文件被镜像——照原样——我兴奋得头昏脑胀！—在浏览器中。这让我想起了我刚开始建网站的时候，双击`index.html`就足以预览你的作品。

如果您使用 ES6 模块，您确实需要一个本地服务器(所以双击一个 HTML 文件可能会永远成为过去)。但是在编辑代码和在浏览器中查看更改之间没有延迟，并且您在检查器中看到的源代码正是您在编辑器中键入的内容(没有 sourcemaps！).

别管更快的编辑-编译-调试周期——这直接说明了 Chimero 对今天的代码库中缺乏可读性的[的担忧，这是学习这门手艺的障碍](https://frankchimero.com/blog/2018/everything-easy/):

> 以前，网站可以自我解释；现在，需要有人带你走一遍。模糊来自于复杂而不清晰。我相信源的易读性是网络最重要的属性之一。[……]帮助某人*编写*标记的最好方法是确保他们能够*阅读*标记。
> 
> — [弗兰克·奇梅罗](https://frankchimero.com/blog/2018/everything-easy/)

## 应用捆绑包的未来

仅仅因为你不需要一个构建工具来运行你的代码，并不意味着你不应该使用一个产品构建来优化性能。我这里指的不是变性，而是缩小、扭曲、摇晃树木等。

我将 JavaScript 捆绑到一个单一的`app.js`文件中已经有很长时间了，我的第一反应是将所有的东西连接到一个单一的脚本中 *Schematics* 。当然，这不适用于 ES6 模块——文件的概念是不同模块之间的界限，没有办法为每个文件指定多个模块。

幸运的是，您不需要将 ES6 模块捆绑到一个文件中来提高性能。让我重复一遍:**您不需要将您的 ES6 模块捆绑到一个文件中来提高性能**。

原因如下:

1.  `<script type=“module">`请求在默认情况下被[延迟](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules#other_differences_between_modules_and_standard_scripts):它们不会阻塞文档解析。
2.  从单独的源文件为所有模块提供服务对于缓存来说是非常好的，因为不受某些更改影响的模块可以继续从缓存中检索。当您提供单个包时，任何一个更改都会使整个包失效。
3.  你可以通过使用[动态导入](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#dynamic_imports)来延迟加载部分代码——在运行时，在你真正需要的时候导入模块。
4.  可以用`[modulepreload](https://developers.google.com/web/updates/2017/12/modulepreload)`预加载关键模块。这将在主线程之外立即开始解析和编译链接的模块。
5.  最后，HTTP2 将来可能允许我们从第一个`<script type=“module”>`请求中解析整个依赖图，并在一个响应中发回所有需要的文件。目前，这需要在服务器端编写定制的逻辑。

不要忘记包的大小:

> 如果您检查由最流行的捆绑器生成的输出代码，您会发现许多样板文件，它们的唯一目的是动态加载其他代码和管理依赖关系，但是如果我们只是使用带有导入和导出语句的模块，这些都是不需要的！
> 
> — [菲利普·沃顿](https://philipwalton.com/articles/using-native-javascript-modules-in-production-today)

有关 ES6 模块负载性能和应用捆绑包的更多细节和有趣讨论，请参见 ECMAScript 讨论档案上的[这个帖子。规范还没有确定下来，有很多想法在流传，有些比其他的更大胆(我个人最喜欢的是将整个模块依赖图作为. zip 文件提供的建议)。](https://esdiscuss.org/topic/fwd-are-es6-modules-in-browsers-going-to-get-loaded-level-by-level)

> 不过，Chrome 中有大量正在进行的模块工作，所以我们越来越接近让 bundlers 得到他们应得的休息了！
> 
> — [塞尔吉奥·戈麦斯](https://developers.google.com/web/updates/2017/12/modulepreload)

更多阅读:

[](https://philipwalton.com/articles/using-native-javascript-modules-in-production-today/) [## 在今天的生产中使用原生 JavaScript 模块

### 关于 web 开发、开源、软件架构和未来的思考。

philipwalton.com](https://philipwalton.com/articles/using-native-javascript-modules-in-production-today/) [](https://tutorials.yax.com/articles/javascript/import/index.html) [## JavaScript 导入说明

### Javascript 'import '语句:它的目的和使用方法。来自关于无堆栈 web 的一系列文章…

tutorials.yax.com](https://tutorials.yax.com/articles/javascript/import/index.html) [](https://medium.com/backticks-tildes/introduction-to-es6-modules-49956f580da) [## ES6 模块简介

### 软件工程的一个重要方面是效率。每个成功的应用程序都需要一个坚实的架构…

medium.com](https://medium.com/backticks-tildes/introduction-to-es6-modules-49956f580da) 

# Web 组件

Web 组件是几种本地技术(自定义元素、影子 DOM 和 HTML 模板)的总称，这些技术让我们将元素的标记和动态行为捆绑到一段可重用的代码中，在高层上与 React 或 Vue 组件没有什么不同。截至 2021 年 5 月， [*所有制作 Web 组件的方法*](https://webcomponents.dev/blog/all-the-ways-to-make-a-web-component/) 列出了一个假想的`<my-counter>`组件的 55 种变体，用于跨捆绑包大小、编码风格和性能的比较。当然，本地 web 组件脱颖而出，因为它们没有外部依赖性(因此，具有无与伦比的小捆绑包大小)。

这里是我自己对 web 组件的一些印象，当谈到 DX 和架构时，与外部框架进行比较。

## 阴影 DOM 和<template></template>