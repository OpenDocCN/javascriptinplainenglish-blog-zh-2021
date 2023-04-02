# 通过例子抽象语法树

> 原文：<https://javascript.plainenglish.io/abstract-syntax-trees-by-example-9e581091b24f?source=collection_archive---------11----------------------->

## Babel 是一个非常强大的代码生成器和解析器，但是文档中并没有很多关于如何使用它来解析、生成和操作抽象语法树的例子，我在这里收集了一些我自己使用它的例子。

我目前正在做一个兼职项目，需要大量的 JSX/HTML 解析、操作和使用抽象语法树(AST)的生成。

ASTs 非常强大，你可以用它们来构建自己的[巴别塔插件](https://babeljs.io/docs/en/plugins)、[宏](https://github.com/kentcdodds/babel-plugin-macros)，或者直接将它们作为你的应用程序的一部分，对你的代码进行定制解析和操作。

你可以在这里阅读更多关于 ASTs 的基础知识:

*   [巴别塔插件手册。](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/en/plugin-handbook.md)
*   [用 ASTs 升级自己的解析游戏](https://medium.com/basecs/leveling-up-ones-parsing-game-with-asts-d7a6fc2400ff)
*   [KCD 关于宏的视频](https://www.youtube.com/watch?v=nlAHtAQlFGk)

在处理 ASTs 时，您需要经常查阅的一个主要资源是 [babel types 文档](https://babeljs.io/docs/en/babel-types)，但是我发现它的一个大问题是缺少关于如何使用不同方法以及输出的代码类型的示例。

因此，作为我自己和他人的资源，我在这里收集了一些我自己使用的例子，并将随着时间的推移更新这个帖子，因为我正在进行这个项目:

对于所有的例子，假设我正在导入这些库:

babel imports

# 向 JSX 元素添加属性:

Add an attribute to a JSX element

> *注意:上述条件中的* `*visited*` *param 名称是为了避免在同一个节点中再次遍历而导致无限循环，因为 babel 不保证只访问同一个节点一次。可能有更好的方法，但在我搞清楚之前，这就是这种情况的原因。*

# 将元素包装在新元素中:

Wrapping an Element in a new one

# 获取元素的所有键/值属性

Get all key/value props of an Element

# 将新道具应用于元素

Apply New Props to an Element

为了渲染生成的 JSX 输出，我使用了这个库 [react-jsx-parser](https://github.com/TroyAlford/react-jsx-parser) ，我检查了它的源代码，它似乎使用了 [Acorn](https://github.com/acornjs/acorn) ，这是另一个 AST 解析器/生成器(babel 实际上是基于 Acorn 的)。

关于如何使用特定方法的示例，我找到了一些其他的好资源:

*   在 GitHub 上搜索 babel 插件，看看它是如何在不同的上下文中使用的。
*   搜索[codata](https://www.codota.com)寻找我正在尝试使用的方法，例如[https://www . codata . com/code/JavaScript/functions/% 2540 babel % 252 ftypes/stringLiteral](https://www.codota.com/code/javascript/functions/%2540babel%252Ftypes/stringLiteral)(tbh，我发现他们的搜索比 Github 的好很多)。

此外，我发现 [AST Explorer](https://astexplorer.net/) 在快速尝试特定方法并查看它们的输出方面很有用，但是我错过了 VS 代码给出的每个方法签名的自动完成。( [Kent C. Dodds](https://medium.com/u/db72389e89d8?source=post_page-----9e581091b24f--------------------------------) 在[这个视频](https://www.youtube.com/watch?v=1ERAJG9ILhk)展示了如何用它来构建 babel 宏)。

感谢阅读！

*最初发布于*[*https://fel fel . dev*](https://felfel.dev/abstract-syntax-trees-by-example/)*。*