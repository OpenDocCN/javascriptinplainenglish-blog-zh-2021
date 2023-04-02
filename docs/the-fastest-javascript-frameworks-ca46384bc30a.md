# 最快的 JavaScript 框架

> 原文：<https://javascript.plainenglish.io/the-fastest-javascript-frameworks-ca46384bc30a?source=collection_archive---------6----------------------->

![](img/c01a7b67276e19ca811b49b48da4c5f8.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

框架非常有用。它们帮助人们通过组件重用代码，并允许更多的声明式编码风格。很可能，如果你正在读这篇文章，你以前用过一个，不管是 React、Angular、Vue.js、Alpine、Preact，还是众多框架中的另一个。

然而，由于存储和呈现组件所需的代码，它们带来了性能成本。幸运的是，您可以通过选择一个快速的框架来最小化成本。在本文中，我们将看看几个最快的 JavaScript 框架，并在基准测试 [krausest.github.io](https://krausest.github.io/js-framework-benchmark/2021/table_chrome_90.0.4430.72.html) 上对它们进行比较，同时展示它们的使用示例。

# Solid.js

正如他们在 GitHub 上的页面所描述的， [**Solid**](https://github.com/ryansolid/solid) **是一个用于构建用户界面的声明式、高效、灵活的 JavaScript 库。固体就像反应和苗条一起工作的结果。它结合了 React 的 JSX 和钩子与 Svelte 的编译性质和粒度，使其成为一个性能强大的软件。**

正如你在上面看到的，Solid 看起来很像 React。然而，要记住的最重要的事情，也是为什么 Solid 快得多的部分原因，是 **Solid 认为 render 函数是一个构造函数，必须使用 effects 来声明性地更新内容。这允许 Solid 仅在某些状态改变时运行某些效果，减少了状态改变时需要运行的代码。幸运的是，如示例所示，Solid 在 JSX 编译表达式来实现钩子，所以在某些情况下，如果您之前使用了 React，您可以保留大部分代码。**

## 基准测试结果

**速度:**比普通版慢 9%

**内存:**使用的内存比普通内存多 21%

**启动时间(下载&执行):**比普通版本慢 3%

## [Solid.js 链接](https://github.com/ryansolid/solid)

# 地狱

[Inferno](https://infernojs.org/) 甚至比 Solid 更接近于 React，主要是相同的功能，除了一些生活质量的变化，如向功能组件添加生命周期方法，这些方法作为道具传递，而不是有一个`useEffect()`钩子，并支持 [Hyperscript](https://github.com/hyperhype/hyperscript) 以及 JSX。然而，尽管 Inferno 类似于 React，但它仍然比 React 甚至 Preact 快得多。如果你想与 React 生态系统兼容，Inferno 是最好的选择之一，它允许你使用 React 包，同时还能获得相对 React 真正好的性能。

Inferno 示例比 solid 示例更冗长，但这主要是因为它是一个类组件，对于 Inferno 来说更受欢迎，但您仍然可以在 Inferno 中使用功能组件。总的来说，Inferno 是这个列表中反应最接近的。

## 基准测试结果

**速度:**比普通版慢 23%

**内存:**比普通内存多 30%

**启动时间(下载&执行):**比普通版本慢 6%

## [魔族链接](https://infernojs.org/)

# 超 app

如果你喜欢 [HyperScript](https://github.com/JorgeBucaran/hyperapp) 并且注重性能，那么 [Hyperapp](https://github.com/JorgeBucaran/hyperapp) 是最好的选择之一。Hyperapp 很小，根据 [Bundlephobia](https://bundlephobia.com/result?p=hyperapp@2.0.14) 只有 1.7kb 的 gzip，速度极快。虽然它支持 JSX，但它包括内置在其模板函数中的 HyperScript，并且主要用于 HyperScript。

如果你想使用 HTML 之类的东西，我不建议你使用 Hyperapp，但是如果你喜欢 HyperScript，它是一个很好的选择。

## 基准测试结果

**速度:**比普通版慢 26%

**内存:**比普通内存多 35%

**启动时间(下载&执行):**比普通版本慢 2%

[Hyperapp 链接](https://github.com/JorgeBucaran/hyperapp)

# 回复:DOM

[RE:DOM](https://redom.js.org/) 是一个轻量级的组件框架实现，试图尽可能接近本地 DOM(因此 RE:DOM)，正因为如此，它没有实现任何 VDOM，并且速度非常快。有一些插件可以与 RE:DOM 一起使用 JSX，但是目前，主要的方法是只使用模板函数，这意味着它可以在没有构建步骤的情况下工作。此外，除了一些功能之外，它还支持 IE 6 的浏览器。

虽然 RE:DOM 仍然支持生命周期和其他反应性组件，但它要小得多，因此您必须实现其他框架内置的一些东西。我会向那些想要更多的本机 DOM 的人推荐这个，但是不推荐给那些想要最佳易用性并且不关心使用本机 DOM 的人。

## 基准结果

**速度:**比香草慢 27%

**记忆:**比香草多 40%的记忆

**启动时间(下载&执行):**比普通版本慢 2%

[RE:DOM Link](https://redom.js.org/)

# 苗条的

在本文列出的所有产品中，Svelte 是最受欢迎的。它最大的吸引人之处在于它是一个“正在消失的框架”，用一些非常小的辅助方法编译成几乎是本机的 JavaScript。Svelte 是该列表中唯一使用完整文件模板语法的框架，其中每个组件都是一个单独的文件，并且文件内部很像普通的 HTML，大部分逻辑都在`<script>`标签中。

正如您所看到的，Svelte 和 reactor 一样简洁，具有相同的简单反应性，而且感觉更像是本机 JavaScript。此外，Svelte 有更多的内置功能，例如应用程序范围的数据存储和转换，同时仍然设法在所有框架中占据最小的空间。

## 基准结果

**速度:**比香草慢 31%

**记忆力:**记忆力比普通香烟高出 34%

**启动时间(下载&执行):**比普通版本慢 2%

# 结论

上面所有的框架都很棒，你应该尝试一下，找出你最喜欢的方法。对于想要《JSX 与反应》的人来说,《固体与地狱》是很好的选择，对于 HyperScript 来说,《超级脚本》是很明显的选择，对于声明性操作和普通 JavaScript DOM 操作的混合，RE:DOM 是很好的选择，对于想要最小的学习曲线和类似 Vue.js 的语法的人来说，Svelte 是最佳选择。

感谢您的阅读，为了向您展示这些框架有多快，我将留给您 React 的结果:

**速度:**比香草慢 98%

**记忆力:**记忆力比普通香烟高出 91%

**启动时间(下载&执行):**比普通模式慢 36%

*更内容于*[T5](http://plainenglish.io/)