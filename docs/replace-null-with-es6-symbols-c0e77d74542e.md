# 用 ES6 符号替换 null

> 原文：<https://javascript.plainenglish.io/replace-null-with-es6-symbols-c0e77d74542e?source=collection_archive---------1----------------------->

![](img/9c465f6eb23ae6592224e22116dc5550.png)

当我在开发我的小型项目库时，我需要表示一个缺失的值。过去，当我想要更多的控制时，我在简单的设置和选项中使用可空的方法。

在这种情况下，两者都不正确，所以我想出了一个不同的方法来展示。

# 为什么可空是不够的

可空意味着当有一个值时，它是一个字符串、一个数字或一个对象。当没有值时，我们使用`null`或`undefined`。

*提示:*如果您在 TypeScript 中使用可空类型，请确保您打开了`[strictNullChecks](https://www.typescriptlang.org/tsconfig#strictNullChecks)`

这通常是好的。

一般来说，有两种情况不是这样:

1.  值*可以是`null`或`undefined`。最后，这些都是有效的 JavaScript 原语，人们可以以多种方式使用它们。*
2.  你想增加一些高级逻辑。到处写`x == null`变得繁琐。

在我的例子中，我处理的是一个承诺的输出，它可以返回任何东西。而且我可以预见，这两个‘失踪’最终都会被归还。

一般来说，问题 1 和 2 有相同的解决方案:使用实现选项类型的库。

# 为什么选择太多

Option(有时称为 Maybe)类型有两种可能:要么没有值(`None`在`Nothing`上)，要么有值(`Some`或`Just`)。

在 JavaScript/TypeScript 中，这意味着引入一个包装值的新结构。最常见的是一个具有属性`tag`的对象，该属性定义了它的可能性。

这就是如何在 TypeScript 中快速实现选项:

通常，你会使用一个定义类型的库和一些有用的工具。[这里是我最喜欢的 fp-ts 库中选项的介绍](https://dev.to/ryanleecode/practical-guide-to-fp-ts-option-map-flatten-chain-6d5)。

我构建的库很小，没有依赖性，并且不需要使用任何选项工具。因此，引入一个选项库将是大材小用。

[](https://github.com/robinpokorny/promise-throttle-all) [## github-robinpokorny/promise-throttle-all:🤏promise . all 有限并发

### Promise.all 用有限的并发限制正在进行的异步操作，比如一次只运行几个 API 请求…

github.com](https://github.com/robinpokorny/promise-throttle-all) 

有一段时间，我在考虑内联这个选项，也就是从头开始编码。对于我的用例来说，这只有几行。但是，这会使库的逻辑有点复杂。

然后，我有了一个更好的主意！

# 符号作为新的空值

回到 Nullable，无法解决的问题是`null`(或`undefined`)是全局的。它是一个等于自身的值。对每个人来说都一样。

如果你返回`null`，我返回`null`，以后，就不可能知道`null`从哪里来了。

换句话说，永远只有一个实例。为了解决这个问题，我们需要有一个新的`null`实例。

当然，我们可以使用空对象。在 JavaScript 中，每个对象都是一个新的实例，它不同于任何其他对象。

但是，嘿，在 ES6 中我们有了一个新的原语来做这件事:符号。(阅读一些[符号介绍](https://hacks.mozilla.org/2015/06/es6-in-depth-symbols/)

我做的是一个新的常数，代表一个缺失值，这是一个符号:

让我们来看看好处:

*   这是一个简单的值，不需要包装
*   其他任何内容都被视为数据
*   这是一个私有的 None，该符号不能在其他地方重新创建
*   它在我们的代码之外没有任何意义
*   标签使调试更容易

太棒了！特别是第一点允许用 None 作为`null`。查看一些使用示例:

# 符号几乎是空的

也有一些缺点。

首先，这在 IMO 中很少见，环境必须支持 ES6 符号。也就是说 Node.js > =0.12(不要和 v12 混淆)。

第二，电子监管化(去电子监管化)存在问题。有趣的是，符号的行为和`undefined`一模一样。

因此，关于实例的信息当然会丢失。然而，由于它的行为类似于`undefined`——本机“缺失值”)——这使得它非常适合表示自定义的“缺失值”。

相反，选项基于结构而不是实例。任何属性`tag`设置为`none`的对象都被视为无。这使得序列化和解序列化更加容易。

# 摘要

我对这种式样相当满意。在不需要对财产进行高级操作的地方，这似乎是比`null`更安全的选择。

也许，如果这个自定义符号泄漏到模块或库之外，我会避免它。

我特别喜欢使用变量名和符号标签，我可以传达缺失值的域含义。在我的小图书馆里，它代表着承诺没有实现:

不同的域含义可能会有多个缺失值。

> *让我知道你对这个用法的看法？是不是很好的替代* `*null*` *？每个人都应该使用期权吗？*

注意:符号并不总是容易使用，看我的演讲*符号让一切变得复杂*。

*原载于*[robinpokorny.com/](https://robinpokorny.com/blog/replace-null-with-es6-symbols/)*。*