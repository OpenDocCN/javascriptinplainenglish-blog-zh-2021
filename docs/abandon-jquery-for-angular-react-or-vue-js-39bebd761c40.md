# 放弃 Angular、React 或 Vue.js 的 jQuery

> 原文：<https://javascript.plainenglish.io/abandon-jquery-for-angular-react-or-vue-js-39bebd761c40?source=collection_archive---------4----------------------->

## 放弃 PHP 而使用 jQuery

![](img/77adabcf1a1090a5a4ef685ae3513bb8.png)

Photo by [Tudor Baciu](https://unsplash.com/@baciutudor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我使用 jQuery 已经很久了。然后是香草 JS，我们如此优雅地称呼它，JavaScript 在本地实现。我密切关注淘汰赛和公司，但从未真正投资过。AngularJS 也是如此，超级英雄，每个人都在谈论它！MVVM 出现了。当我刚刚深入理解了一个 MVC 架构的来龙去脉时，一个需要重新键入的野蛮的名字。不用了，谢谢。

我要告诉你的是:就我而言，我发誓要把角色分开。我不想回到带有无效 W3C 属性和源代码的 HTML 混合结构和行为中去哭泣。jQuery 或 Vanilla JS 仍然是安全的值，这让我感到很欣慰！

但是在那里。由于看到它经过，我最终研究了这个角。事实证明，我在他身上发现的主要缺点可以通过一点严谨来解决。好吗？但是，在 jQuery 一直在做这项工作的地方，花费这么多精力去使用这个时髦的工具有什么好处呢？

即使由于我对 Aurelia，React then Angular 的表面研究，我部分理解了这种变化的有用性，但由于 Vue.js 的研究，我似乎已经找到了放弃 jQuery 的好理由的明确答案。在一个简单的下午的阅读中！我现在对这个图书馆发誓！

简单来说:jQuery 穿越 DOM，Vue 穿越数据！这改变了一切。

# **最开始，有 jQuery**

我真的很喜欢 jQuery。正是由于这个 JavaScript 库，我今天成为了一名充满热情的全栈 JavaScript 开发人员。回到我业余开发网站的时候，我从我的 PHP 文件中选择了 jQuery。然而，我放弃了 PHP，它开始用严肃的对象语法来装饰自己，以支持更前端的专门化。我被 jQuery 的灵活性迷住了。

jQuery 怎么可能是用 JavaScript 完成的？当时我与 JavaScript 的唯一联系是 JavaScript 编辑器网站上的“征税”脚本。为了避免浏览器之间的各种错误，我花了几个小时“破解”它们。JavaScript 绝对是我讨厌的“肮脏”语言。但是这个 jQuery 简单、优雅、编写快捷、简单、独立于 HTML，有数千个插件等等。我不知道我有没有说过，但也很简单。

使用 HTML 作为结构，CSS 作为皮肤，jQuery 作为交互，我发现了一个很好的开发方法，通过分离不同的角色而不混合，这样我就可以用相同的 HTML 得到完全不同的界面。

当然，为了跟得上后端，我在学校用 Java 学习了面向对象编程，在工作中用 C #。我尊重这些语言的严谨性、复杂性以及它们所承载的哲学实现目标。但是 jQuery 太可伸缩、太通用、太优雅、太简单，不是我的最爱。当然，如果我必须做点实实在在的事情，我会的。但是和近几年研究的后端语言不同，对于一些简单的东西，jQuery 也是这样回答的！

jQuery 已经变得如此舒适，以至于很难脱离它，甚至很难想象其他库可以做得更好。

但这个问题还是困扰着我。一个让我远离 PHP、C #和 Java 的库是如何用 JavaScript 开发的。

# **JavaScript 不是自动的！**

所以我卷起袖子去真正理解 JavaScript 的基础知识。我想说，对我来说，关键是理解这种语言的异步特征的全部范围，以及将函数作为参数传递的可能性。

我做一件事情，我也传递这个事情完成时应该调用的函数，不管这个事情要花多长时间。不可思议，所以不是 jQuery“发明”了这个。事实上，由于闭包，这种机制是可能的，函数可以在函数中传递自己的事实来自于函数是对象的事实。这种可怜的语言没有类型，没有迎合价值观的可能性，事实上是弱类型的，并使用强制来“自动”根据需要改变类型。

JavaScript 肯定比第一眼看上去更有趣，它融合了我以前学习过的所有语言中的许多概念。最后，研究了最近所有浏览器中实现的原生 DOM API，我得出结论，是时候告别 jQuery 了。这个神奇的工具包实际上只是从正确的角度更容易地处理 JavaScript 的垫脚石。你只需要有勇气。

因此，我向香草 JS 敞开怀抱，并说服自己原生 JavaScript，加上少量使用的小库和 polyfills，是拯救我的关键。

我想对你说的是，在那个时候，有了这样一个启示，我在安古拉杰的起步就很糟糕！

# **AngularJS，Node.js，React，Angular 都在一个篮子里？**

我错过了后端！我依靠我的 C #专家同事来管理一个完整的网站。我用 CodeIgniter 或 Laravel 重做了一点 PHP，这让我明白了 JavaScript 的“魔力”在其他语言中是多么的缺乏。但是看起来我们可以在服务器端使用 JavaScript。

所以在那里，当 Node.js 只显示 0.1xx 版本时，我不需要更多就可以跳到它上面！然而，被迫在分配给我找到的不同版本的不同资源之间游泳，最初很难区分什么真正属于 Node.js 的核心和那些像 Expressor 这样的 npm 包，甚至属于 Express 本身的中间件。

尽管我的 JavaScript 背景并不复杂，但学习曲线让我认为 Node.js 需要一点推动，才能让前端开发人员“困在”jQuery 或 PHP 后端开发人员警惕 JavaScript 开始使用。

JavaScript 生态系统爆炸了，我对这个生态系统的理解也爆炸了。现在没有人在雇佣 JavaScript 专家了。要约内容是宣布我们需要一个致力于这样一个框架的 JavaScript 开发者。给定 NodeJS，ReactJS，NodeJS，AngularJS，或者 VueJS，还有人知道自己在说什么吗？如果连 JavaScript 开发者都丢了，非专家怎么可能？

但是经过几次重新穿越和严谨的观察，终于，它没有那么恐怖了。请教专家！

# **查看？我没见过她！**

除了安古拉杰，还有一个谨慎谦逊的人，可以和他竞争。简单，优雅脱颖而出，渴望以一种进化和多才多艺的方式使用。此外，它的 API 定义得非常好，以至于在从一个版本到另一个版本的转换过程中，深入改变它的内部机制不会影响它的外部使用，这给了它一个虚拟的 DOM。AngularJS 方面，已经失去了所有人，并迫使普通人使用 TypeScript(即使不是强制性的好运无)。

# **见过，见过的人，都会见到。见过吗？**

由于 React 的虚拟 DOM 和 JSX 的使用，当 React 带来服务器端渲染时，Vue 仍然存在，能够进行服务器端渲染。

事实上，Vue 从一开始就在那里，而且是经过深思熟虑的，从外表上看几乎没有改变。但是，从性能、重量、学习曲线来看，它超越了 Angular 和 React！尽管如此，Vue.js 还是溜了进来，由一个独立的 JavaScript 社区领导，重量级的谷歌和脸书正在那里展开战争。

Vue 是如此的可扩展和简单，以至于你可以像使用 jQuery 一样轻松地使用它！这不是诡计。Vue 被设计成既可以在客户端 DOM、一些界面和表单上少量使用，也可以独立处理完整的客户端和服务器端 DOM 以及完整的导航。

# **现在呢？**

Vue.js 之于 Angular 和 React 就像 jQuery 之于 Vanilla JS 一样。此外，如果您仍然处于 jQuery 的舒适区中，并且像一个不可约的高卢人一样通过说服自己 Angular 和 React gas factories 没有什么可以带给您来捍卫这一立场，请尝试 Vue 的冒险。Js。由于其直观的[向导](https://vuejs.org/v2/guide/)，你不需要超过半天的时间就能感受到它的潜力。

无论如何，对我来说，那都是 Vue！

*更多内容尽在*[***plain English . io***](http://plainenglish.io)