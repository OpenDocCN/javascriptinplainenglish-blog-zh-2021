# 你可以在你的网页上使用一些 JavaScript 策略

> 原文：<https://javascript.plainenglish.io/a-few-javascript-strategies-you-can-use-on-your-web-pages-1dc040629ad?source=collection_archive---------14----------------------->

## 关于如何在你的网站上使用 JavaScript 的提示。

![](img/a28b1f1998dbf92d61a390e60b619af3.png)

Photo by [KOBU Agency](https://unsplash.com/@kobuagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 在网页中的主要用途是增强或添加静态网页中没有的功能。如果使用正确，这对熟练的开发人员来说是一笔巨大的财富。如果您滥用 JavaScript，您(和您的用户)将会陷入各种各样的噩梦中。

在我们开始制定好的策略之前，这里有三件事**不是**要做:

## 不要使用 JavaScript:

添加需要被搜索引擎索引的信息。这是一个显而易见但仍然容易被忽视的问题。我们如此努力地想让 HTML 简洁明了，以至于我们很容易将可索引信息转移到 JavaScript 中，而不是保留在 HTML 中。如果搜索引擎需要看到它，就把它留在 HTML 中。

## 修复你懒得在源代码中修复的东西。

如果你有机会应用一个补丁，移动元素，或者在不使用 JavaScript 的情况下实现你的结果，那就去做吧。用 JavaScript 编辑 DOM 会对性能产生影响。只有当它有意义时才使用它。

## 主要是为了让网站变得“酷”

我可以把这句话倒过来说，“只使用 JavaScript 来增强用户体验，向用户提供适当的指示，并提高网站的整体可用性。”或者用更老套的话来说，“负责任地编写 JavaScript。”你可以做很多事情，但是一定要只处理你应该做的事情。

# 好策略

## 选择一个好的框架(或者不选择)初学 JavaScript 程序员应该使用框架吗？

目前有许多强大的 JavaScript 框架和库。原型、MooTools 和 jQuery 只是其中的几个。接下来的问题是，“您应该先学习普通的 JavaScript，还是从这些框架中的一个开始？”尽管 JavaScript 语法和最佳实践非常重要，但我认为如果你只是想增强你的网页，你应该从框架开始。这通常是最容易学习的，你不必浪费时间在浏览器如何处理常见函数的差异上(想想 XML/HTTP/Request)。

如果您计划开发高级 AJAX/DHTML 前端，那么学习如何操作 DOM、发出 AJAX 请求等。，使用唯一的 JavaScript 将是一个好主意。

## 延伸阅读:

*   [操纵 DOM](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents)
*   [发出 AJAX 请求](https://medium.com/@Sharad35386442/6-different-ways-to-do-ajax-calls-in-javascript-b47200fe7a38)

如果您想为您选择的框架构建插件，了解幕后发生的事情也是很好的。

## 框架可能会使维护更容易

假设你将是唯一一个维护或编辑你的代码的人是非常短视的。您的业务可能会增长，您的客户可能会转向另一家开发商，等等。正是由于组编辑的想法，我建议使用一个可靠的框架。如果你使用一个框架，并且正确地使用它(以“正确的方式”来做)，其他人拿起你的代码应该会更容易发现发生了什么。

## 进一步阅读

*   [编写可维护的 JavaScript 代码](https://blog.bitsrc.io/javascript-best-practices-for-readable-and-maintainable-code-b54f0aca2353)

## 知道何时避免使用框架

在很多情况下，使用框架变得不切实际。如果你需要做的只是在页面上显示或隐藏一个元素，那么使用直接的 JS。不值得花费 50k+的开销来加载框架。如果你正在构建一个包含在另一个站点上的小部件，不要使用框架。

例如，FoxyCart 是一个超级易用的购物车系统，它使用 JavaScript 来驱动购物车。然而，在使用 FoxyCart 时你会遇到的一个问题是，它们包含了自己的 jQuery 副本。

作为一个嵌入在别人网站上的小部件/库，他们应该已经手工编写了自己的库，以避免与其他库发生冲突。(对于 jQuery 用户，使用$。noConflict 不会修复在同一个站点上运行两个 jQuery 副本的问题)。

# 固定元件跳跃

如果页面上的许多元素专门应用于 JavaScript 上下文，当 JavaScript 最终加载时，您可能会看到元素跳跃或出现然后消失。在许多不同的情况下，这可能是一个问题，但这里有一些避免它的策略。如果您将 JavaScript 文件放在页面底部(正如您应该做的那样)，这通常会是一个更大的问题。

## 使用特殊的 CSS 类

我喜欢给我打算用 JavaScript 增强的元素添加一个`no_js`类。属性对 JavaScript 文件中的元素进行样式化。当 JavaScript 被禁用或尚未加载时，它们应该如何出现的类。JavaScript 设置的最后一步是从元素中移除该类。

## 早点开始编辑

如果你使用 JavaScript 框架(比如 MooTools 或 jQuery)，一定要使用它们的 DOM Ready 函数，而不是 onLoad。DOM 通常在所有东西都完全加载之前就准备好了，可能会给你提供你需要的额外时间。

## 用 JavaScript 添加特定于 JavaScript 的元素

如果 HTML 元素的唯一值是在使用 JavaScript 时实现的，那么用 JavaScript 动态添加它。例如，您不希望一个空的 div #覆盖图位于 HTML 的末尾。用 JavaScript 加上就行了。

# 排除故障

## 使用 Firebug 和 console.log

在一个微小的脚本中，加入`alert ('Here'!')`可能会运行良好。但是，在做更大的事情时，您可能希望利用 Firebug 控制台进行测试和调试。用它来输出值和对象，甚至是 DOM 对象。它通常会提供快速的洞察力，让你更快地解决问题。

## 不要忘记删除 console.log 语句。

如果使用 Firebug，一定要删除`console.log`语句，或者提供另一种方法来避免遗漏方法错误。

我经常发现这一点:它在我的电脑上有效，但在客户的电脑上无效。我们都在用火狐。更令人困惑的是，该网站在 Safari 中也能正常运行。

> *怎么了？*

是我用来调试的剩余 console.log 语句！Safari 通常会跳过这些语句而不会抱怨太多，所以在部署(或向客户端显示 comp)之前，请确保搜索“console.log”并删除这些语句。

## 结论

我刚刚提到了一些在页面上使用 JavaScript 的策略和技巧。随意分享你自己的！当我将来遇到其他有用的技巧时，我一定会用简单的英语在 JavaScript 上再次发布。