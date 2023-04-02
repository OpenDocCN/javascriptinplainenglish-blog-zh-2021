# 通过解决一个常见错误来理解 Next.js 中的代码拆分

> 原文：<https://javascript.plainenglish.io/understand-code-splitting-in-next-js-by-solving-a-common-error-db61a9b1b1a1?source=collection_archive---------3----------------------->

## 一个小小的错误如何让我学到了很多关于前端开发的知识

![](img/14c1c727d31fae4e17ab2bf17cb4c32b.png)

Photo by [Ivan Bandura](https://unsplash.com/@unstable_affliction?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral), portraying a mine. Illustrating the fact that it sometimes better to dig deeper.

在为 Next.js 项目定制站点地图功能时，我遇到了以下错误:`Module not found: Can't resolve 'fs'`。虽然这看起来是一个明显的错误，但对解决方案的探索让我获得了许多真知灼见。

Next.js 越来越受欢迎。有一个很好的理由，它使得用 React 开发服务器端呈现的应用程序变得轻而易举。它拥有令人印象深刻的功能，并且开箱即用。

我的[个人网站](https://maikelveen.com/)利用了 Next.js，Next.js 缺少的一个功能是 sitemaps，这是可以理解的，因为它的形成很大程度上取决于具体的数据源和其他变量。

我认为花时间为我的网站创建一个网站地图是值得的；这肯定不会伤害搜索引擎优化。实现网站地图功能需要经历重重困难。您可以利用由 Next.js 的构建过程创建的清单。我在开发过程中遇到了一个奇特的错误:`The Module not found: Can't resolve 'fs'`。

这个错误似乎很简单:没有找到文件系统模块。可能是没有安装之类的。然而，使这个错误更加有趣的是它发生在浏览器中。文件系统模块不可用的环境，当然也不应该作为依赖项。

当时解决这个错误对我来说是一个不小的任务，但这个过程让我更好地理解了 Next.js 是如何工作的。更具体地说，它教会了我更多关于代码捆绑和拆分的知识。本文解释了如何解决这个错误，并强调了错误上下文，希望您在学习的同时了解更多关于 Next.js 的知识。

该错误描述找不到模块。究竟什么是模块？首先，让我们回顾一下模块、代码捆绑和拆分是怎么回事。

# 模块和代码捆绑

在 Next.js 甚至 React 出现之前，通常的做法是在一个 JavaScript 文件中编写整个网站的所有代码。依赖项，比如 jQuery，是在这个主脚本加载之前加载到脚本标记中的。然而，随着复杂性和依赖关系的不断增加，跟踪和加载依赖关系的麻烦变得太沉重了。

解决方案是将代码库分成模块，这些模块是 JavaScript 的封装单元。在很长一段时间里，模块系统被类似于 [CommonJS](https://en.wikipedia.org/wiki/CommonJS) 的项目所模仿。然而，由于 ES6 模块是带有`import`和`export`语句的 JavaScipt 的原生模块。大多数现代浏览器都支持本机模块。更多信息请点击[这里](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)阅读。

2021 年，我们将我们的代码库分割成模块，并获得许多好处:可维护性和可重用性。最有可能的是，我们所有的模块都在单独的文件中。我们是否在`script`标签中单独加载这些内容？不，当然不是！然后，我们将回到起点，并在浏览器中受到相当大的性能打击。

现在*代码捆绑*开始发挥作用。所有的模块都被打包成一个(或多个)文件，以减少浏览器在加载页面时的请求数量。在前端开发中，当有人提到*构建*时，他们通常指的是捆绑。这一步通常包括缩小:从源代码中删除不必要的字符以减小包的大小。

捆绑包括各种其他任务，可能会变得非常复杂。如今，大多数 React 应用程序都通过工具捆绑文件，如 [Webpack](https://webpack.js.org/) 、 [Rollup](https://rollupjs.org/guide/en/) 或[brower versify](http://browserify.org/)。

# 代码分割

随着代码库的增长，这个包的大小也会增长。现在我们再次面临一个问题。增加包的大小会导致装载时间增加。如果有一件事我们想避免的是缓慢的网页；我们不想考验客人的耐心。

为了避免大的包，我们可以将代码分成多个包。代码分割是大多数捆绑器都支持的一个特性。这是这些捆扎机最引人注目的特点之一。你可以在 React [这里](https://reactjs.org/docs/code-splitting.html)了解更多关于代码拆分的信息。Next.js 是一个构建在 React 之上的框架。当我们使用 Next.js 时，我们有一个现成的 Webpack 设置来捆绑我们的应用程序。

# 下一步捆绑和拆分

本质上，Next.js 是一个运行在[节点](https://nodejs.org/en/)运行时环境中的 web 服务器。它提供特定路径上的页面，这由 Next.js 项目的`pages`文件夹中的文件决定。

使用 React，JavaScript 包由浏览器加载。然后，渲染也由浏览器完成。使用 Next.js，这种渲染由 web 服务器完成。它在服务器端呈现页面并提供输出:HTML。

当您构建交互式页面时，这个 HTML 仍然包含对 JavaScript 包的多个引用。正如你可能想象的那样，并不是你为一个特定页面编写的所有代码都需要在*所有其他页面上使用。加载这些代码是一种浪费。这就是 Next.js 的代码分割发挥作用的地方:它从一个代码库创建多个包。*

这意味着每个页面只加载特定页面所需的 JavaScript。这是使用 Next.js 的好处之一。如果一个特定的页面不使用导入的库，它就不会包含在该页面的 JavaScript 包中。客户机代码被 Next.js 自动分解到几个不同的资源中，而不是生成一个包含所有代码的文件。

在 Next.js 中，特定的包被称为块。如何创建块是由一个复杂的代码分割策略决定的，这个策略[一直在改进](https://nextjs.org/blog/next-9-2#improved-code-splitting-strategy)。

# 解决错误

现在我们明白了什么是代码捆绑和拆分。让我们回顾一下最初导致这项调查的问题。

`The Module not found: Can't resolve 'fs'`当您试图导入一个在服务器端可用但在浏览器中不可用的模块时，很可能会出现错误和类似问题。文件系统模块就是一个很好的例子。

当您在服务器端工作时，需要文件系统模块是完全合理的。例如，从磁盘上的文件中提取数据时。但是，该模块在浏览器中不可用，也不应该包含在浏览器包中。

这是否意味着您根本不能使用这样的节点模块？不，幸运的是，在 Next.js 的现代版本(9.4+)上，你可以安全地在`getStaticProps`或`getServerSideProps`中使用`fs`，分别用于[静态生成](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation)和[服务器端渲染](https://nextjs.org/docs/basic-features/data-fetching#getserversideprops-server-side-rendering)。不需要额外的配置。

当你在那些函数中只引用一个服务器端模块时，依赖关系会被 Next.js 团队创建的一个定制的 Babel 插件正确地树摇掉。

[树抖动](https://webpack.js.org/guides/tree-shaking/)通过从入口点开始，只包含可能被执行的函数，从包中删除未使用的函数。在 Next.js 的情况下，通过删除在`getStaticProps`或 getServerSideProps 文件中使用的依赖项和函数来扩展它。

当你遇到这个问题时，遵守上面的规则就有可能解决问题。

# 代码消除

Next.js 背后的团队 Vercel 提供了一个手动工具 [y tool](https://next-code-elimination.vercel.app/) 来检查浏览器捆绑包中删除了哪些代码。你可以看到，当一个函数只在`getStaticProps`或`getServerSideProps`中被引用时，它就被删除了。

成交了，对吧？没那么快。即使只从`getStaticProps`函数中调用使用文件系统模块的函数，我仍然会得到错误。然后，经过一段时间的困惑，我才明白，这个方法也叫*本身*。

这个抛出错误的函数是一个递归函数。我发现这样的函数也会导致这个问题的出现。在这种情况下，初始函数调用是在`getServerSideProps`中完成的。然而，它也递归地调用自己，这导致它被包含在浏览器包中。

在这种情况下，需要将以下代码添加到 next.config.js 中:

当您使用较旧的 Next.js 版本时，这也是一个解决方案。该配置实际上告诉 Webpack 为 fs 创建一个空模块，这有效地抑制了错误。

# 运行代码服务器端

可以利用其他选项仅在服务器端运行某些代码。您可以在代码中检查 window 属性，以便在浏览器或服务器上执行一段代码。

您可以使用以下条件来检查您的代码是否在服务器端执行:`if(typeof window === 'undefined')`。该条件范围内的任何内容都只在服务器上执行。

这是惯用的检查。如果 JavaScript 在节点环境中运行，那么几个内部对象，比如`window`对象，是不可用的。当我们检查对象的存在时，我们可以有效地确定我们是否在服务器端。

更令人惊讶的是，Next.js 还从浏览器捆绑包中删除了使用这些检查的代码，作为一种构建时优化的形式。浏览器捆绑包将不包括条件范围内的内容。

# 结论

> *这是一件痛苦的事情*
> 
> *看看自己的烦恼就知道了*
> 
> 你自己而不是其他人成功了
> 
> *-索福克勒斯，阿贾克斯*

那么主要外卖是什么呢？如果您以前不熟悉这些概念，那么希望您已经学习了一些关于代码捆绑和拆分的知识。

然而，这里还有一个更重要的教训。我通过简单的谷歌搜索找到了问题的解决方案。然而，我并不完全理解问题的解决方案和确切原因。我可以应用这个补丁，继续做其他的事情。

在谷歌上搜索解决方案，应用它，然后继续前进，却不了解错误的微妙之处或原因，这是软件开发人员比他们愿意承认的更经常做的事情，包括我自己。有时我们时间紧迫，没有时间深入挖掘，这是可以理解的。但是如果情况允许，我们应该后退一步，认识到每个错误的背后都是潜在的知识宝库。

一个有经验的前端开发人员很可能会对这个错误毫不在意。然而，我用它来识别知识缺口，并成功地采取了行动。如果你正面临类似的情况，我建议你尝试同样的方法。感谢您的阅读！

# 进一步阅读

[](https://www.simplethread.com/javascript-modules-and-code-bundling-explained/) [## 用 JavaScript 模块解开代码捆绑之谜——简单线程

### 什么是 JavaScript 捆绑？什么是 ECMAScript 模块？这篇文章解释了我们如何来到这里，并删除了一些…

www.simplethread.com](https://www.simplethread.com/javascript-modules-and-code-bundling-explained/) [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) [## JavaScript 模块

### 本指南为您提供了开始使用 JavaScript 模块语法所需的一切。

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules) [](https://reactjs.org/docs/code-splitting.html) [## 代码分解-反应

### 大多数 React 应用程序会使用 Webpack、Rollup 或 Browserify 等工具“捆绑”文件。捆绑是一个过程…

reactjs.org](https://reactjs.org/docs/code-splitting.html)