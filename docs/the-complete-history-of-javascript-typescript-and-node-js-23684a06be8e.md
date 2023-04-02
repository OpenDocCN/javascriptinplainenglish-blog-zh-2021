# JavaScript、TypeScript 和 Node.js 的完整历史

> 原文：<https://javascript.plainenglish.io/the-complete-history-of-javascript-typescript-and-node-js-23684a06be8e?source=collection_archive---------9----------------------->

![](img/2123cebd401ca804fe18e1774aa9a5ee.png)

# 一点历史

你已经知道在公司软件工程领域使用 JavaScript 的优势是什么，以及 Node.js 是初创公司的最佳选择的 5 个理由是什么。你不知道的是这一切是如何开始的。

这种语言本身已经走过了一段极其漫长的路，从仅仅被用作网站上交互的促进者，到一种成熟的、普遍有用的编程语言。我们将带你踏上从它的诞生到打字时代的旅程。

# JavaScript 的婴儿期

在互联网的早期，每个网站都是静态的。直到 1995 年，还没有办法让网站充满活力；这意味着不可能响应不同的条件而改变网页的内容。这就是为什么在 1995 年，JavaScript 被创造出来。这种语言的创造者布伦丹·艾奇(Brendan Eich)被赋予了一个简单的任务——让交互性成为可能。艾希的创作有一个明确的目标，因此实现了它。很长一段时间，就是这样。

> [*为 JavaScript 之父称*](https://thenewstack.io/brendan-eich-on-creating-javascript-in-10-days-and-what-hed-do-differently-today/) *:*
> 
> 我受命于市场营销，让它(JavaScript)看起来像 Java，但又不至于太大。只是这种傻傻的小兄弟语言，对吧？Java 的伙伴。

# 浏览器中的异步操作

在某一点上，人们觉醒了，意识到可以做得更多。页面仍然需要完全重新加载才能显示新信息，这导致了一个缓慢而低效的过程。必须有一种方法来防止网站重新加载以获取和处理新数据，对吗？

这种创新的第一个广泛的例子是微软允许 Internet Explorer 5 发出 HTTP 请求。1999 年，他们实现了一个名为“XMLHttpRequest”的对象，该对象允许从外部数据源**获取数据，而无需**重新加载页面。

为什么要实现这个功能？长话短说，MSFT 这样做只是为了让 Outlook 网站在后台获取电子邮件。长期效果远不止让一个网站运行得更好。

> *根据 ITMAGINATION 前端开发人员 Monika Mazurczak 的说法:*
> 
> *(微软的 XMLHttpRequest)是 JavaScript 世界中两个最重要的发展之一。异步操作允许用户做更多的事情，而不必重新加载页面，这对于 UX 来说是一个巨大的胜利。”*

还有一个大问题需要解决。JavaScript 引擎实现有很大的不同，甚至每个浏览器都有不同的语言风格！例如，网景有 JavaScript，而 IE 有 Jscript。尽管 MSFT 的实现在某种程度上与 JavaScript 兼容(因为两者都基于 ECMAScript 规范)，但实现却有着本质的不同。

# jQuery——轻松构建不同的浏览器

2006 年，世界看到了旨在解决这一问题的解决方案。14 年前，jQuery 问世了，它抽象出了实现中的差异。您在上面看到的图片是 jQuery 如何处理不同浏览器之间的实现差异。您在下面看到的只是在页面加载完成后调用“jQuery.ready()”函数。

你知道现在会是什么样子吗？由于实现的标准化，这非常简单。有几种方法可以做到这一点，这是其中之一:

jQuery 将成为最受欢迎的 JavaScript 库，而且遥遥领先。从市场份额来看，它至今仍是最受欢迎的图书馆，大约 79.8%的 10k 热门网站上都有它的身影。

相比之下，React.js 被广泛认为是前端开发的现代标准，React 在前 10，000 个最受欢迎的页面中有 43.7%被使用。就前端而言，jQuery 是启动的最后一个重要步骤。跨浏览器的一致性允许开发者创建他们想创建的应用程序，而这在以前是不可能的。

# 2009 年——可以说是自发布以来生态系统最重要的一年

三年后，可以说是整个 JavaScript 世界最重要的一年，有两件事改变了生态系统。

其中一个事件是 Node.js 的首次发布，另一个事件是该语言的第一个修订版——ECMAScript 2009(更广为人知的名称是 ES5)问世了。

**首届 ECMAScript 2009**

ES5 带来了许多绝对必要的特性。[严格模式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)，数组上的基本操作，如[过滤器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)、[映射](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)和[归约](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) ( [“函数式编程的三位一体”](https://dev.to/mlevkov/the-holy-trinity-map-filter-and-reduce-381e))、 [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON) 对象、属性获取器&设置器，以及更多超出本文范围的内容。

**第二个事件——node . js 的诞生**

Node.js 的创建使 JavaScript 成为一种相关的语言，因为运行时使我们除了在浏览器内执行之外，还可以在浏览器外执行脚本。[有趣的是，这并不是第一次允许在服务器端执行 JavaScript 的尝试。Netscape 的 Live Wire 是第一个，但因为这可能是你第一次听说它；这说明了该解决方案的受欢迎程度。虽然它确实值得一提，但我们不会花太多的篇幅来讨论它。](https://www.chicagotribune.com/news/ct-xpm-1997-07-18-9801160234-story.html)

现在，JavaScript 已经可以正式使用了，在该语言被企业正式采用之前，还有一个方面需要解决。语言是动态的，没有类型系统。

你看，当你考虑写一个比你的标准入门项目更大的应用程序时，你迟早会遇到问题。强类型语言，如 Java 或 C#给了你一层安全——它们会自己捕捉一些错误，而不必以任何方式涉及到你，即开发人员。这是因为在运行代码时，他们会自己确保代码的正确性。

# TypeScript 来帮忙了

有一些尝试使 JS 更可预测，然而，微软可能已经提出了迄今为止最好的解决方案。JavaScript 的超集 Typescript 于 2012 年首次问世。它的目的是促进大型应用程序的开发。

它的一些特性使得它在职业玩家中非常受欢迎。

首先，由于 C#和 TypeScript 是同一个人创作的，[它们有一些相似之处。](https://www.telerik.com/blogs/uncovering-typescript-for-c-developers)当然，不要指望两人是双胞胎。

其次，从 JavaScript 迁移到 TypeScript 很容易——您可以一步一步地迁移您的代码库。

第三，TypeScript 在前端与 React 和 Vue 无缝集成。在后端，所有主要的库都使用现成的 TypeScript。Nest.js 默认使用 TS；而 Express.js 和 Fastify 有它们额外的类型定义，让你安装了就不用管了。

如果您需要的任何库不在 TypeScript 宣传列车上，您通常仍然能够使用它们，同时享受增强的设计时支持[。用户免费为所有最流行的库贡献类型定义](https://github.com/DefinitelyTyped/DefinitelyTyped)，在最坏的情况下，你可以编写自己的声明。换句话说——如果你正在使用它——它有类型定义。

# JavaScript 的未来会怎样？

最后，JavaScript 确实取得了长足的进步，并承担了没人梦想的角色。尽管许多人嘲笑它的类型系统，或者它的不一致性，整个生态系统不止一次地证明了自己是一个可靠的竞争者。

纵观 JavaScript 的历史，有两个因素使得它成为最主要的通用编程语言。这两方是开源贡献者和 ECMA。开发人员的适应力和奉献精神已经使这种语言走出了低谷，弥补了它的不足。ECMA 给了他们一个坚实的基础，增加了语言所需要的特性。

JavaScript 的未来并不明朗。似乎它的受欢迎程度主要取决于 [WebAssembly](https://webassembly.org/) 项目的未来。长话短说，有一段时间有可能编译语言，比如 C++或者 Rust 到浏览器可以使用的代码。然而，它的使用有一些严重的限制，例如，你不能访问 DOM(页面的结构),你只能使用相对较新的浏览器。

结果可能是，JavaScript 将不再是唯一能够在浏览器引擎中执行的编程语言。如果发生这种情况，艾希创作的优越性可能会受到挑战，尽管有一个方面将保持不变——语言的简单性。

***PS:我们正在招聘 Node.js 开发者。*** *对于所有 Node.js 的专业人士，我们有一个好消息——我们正在招聘。无论你是一个* [*后端开发者*](https://www.itmagination.com/open-jobs/NodejsDeveloper-8050000012856481) *，* [*React 开发者*](https://www.itmagination.com/open-jobs/ReactDeveloper-8050000012874788) *，* [*React 原生开发者*](https://www.itmagination.com/open-jobs/ReactNativeDeveloper-8050000012886577) *，还是一个* [*棱角开发者*](https://www.itmagination.com/open-jobs/SeniorFrontendEngineerwithAngular-8050000009516936) *，我们都在等你。*

*原载于*[*https://www.itmagination.com*](https://www.itmagination.com/blog/the-complete-history-of-javascript-typescript-and-node-js)*。*