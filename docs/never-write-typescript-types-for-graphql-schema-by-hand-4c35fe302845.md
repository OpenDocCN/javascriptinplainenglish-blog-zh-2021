# 永远不要手工为 GraphQL 模式编写类型脚本类型

> 原文：<https://javascript.plainenglish.io/never-write-typescript-types-for-graphql-schema-by-hand-4c35fe302845?source=collection_archive---------7----------------------->

![](img/254ba15da3fe4f7b8a1316f51260c97b.png)

# 为什么我们要使用 TypeScript？

现代软件开发最佳实践要求程序员编写大量代码:

*   业务逻辑
*   测试。单位/综合/E2E 和*偶数类型*。**类型是测试**，甚至在你运行程序之前就可以大量运行

没有测试，您的系统将注定面临众所周知的问题:

*   团队把大部分时间花在修复 bug 上，而不是增加新功能
*   每一个新添加的特性都会使下一个特性更难实现

**你需要写大量的代码来掌控你的游戏。** **不要让自己的生活更艰难。永远不要再手工为 GraphQL 模式编写类型脚本类型**。

TypeScript 验证您的程序是否支持当前的 GraphQL 模式。这为前端和后端增加了一层令人敬畏的质量测试:

*   您的 CI/CD 可以对您的 repo 运行 TypeScript 验证和单元测试，并检测任何模式裂缝。

但是手工编写打字稿是一项乏味的任务，结果很脆弱。

# 为什么我们要从 GraphQL 模式自动生成 TypeScript？

GraphQL 允许从模式文件自动生成 TypeScript 类型。该功能将:

**节省时间**。应该手动验证每个模式更新并检查错误。即使是一个小的模式也可以是 1000 行的 TypeScript 定义。别忘了在 React 前端你需要写 [Apollo React 钩子](https://www.apollographql.com/docs/react/api/react/hooks/)。

**保护您免受人为错误**。GraphQL 规范非常复杂，有很多细节。您很可能知道以下两者之间的区别:

```
offers(input: OffersInput): [ProductOffer]!
```

和

```
offers(input: OffersInput): [ProductOffer!]!
```

但是，您能在每次模式更新时可靠地验证每个这样的(以及许多更小的)差异吗？

**保护您免受 GraphQL 规范或模式更新的影响。** GraphQL 语言规范随时间演进:[https://spec.graphql.org/](https://spec.graphql.org/)

你的代码库将始终与最新的 GraphQL 模式**保持同步。通过这种方式，您可以避免重大变更意外部署到生产环境中。多酷啊。通过自动生成类型脚本，您的 GraphQL 模式成为整个分布式系统的唯一事实来源。**

# 如何从 GraphQL 模式设置自动类型脚本生成

> *在这篇文章中我使用了一个* [*Monorepo*](https://medium.com/@adamhjk/monorepo-please-do-3657e08a4b70) *项目设置，例如，我所有的包和项目都存储在一个单独的 repo 中。这样，客户端应用程序和后端可以访问 GraphQL 模式的一个物理副本。但是您可以将您的项目存储在您想要的任何地方，只需找到一种方法为您的后端和前端提供相同的 GraphQL 模式文件。*
> 
> ***如果您正在使用第三方 API*** *您可以直接从端点使用当前的 GraphQL 模式。我将在后面描述这个过程。*

我强烈推荐使用 [GraphQL 代码生成器](https://graphql-code-generator.com/)包。

*   **将“devDependencies”安装到你的软件包**(你可以使用不同的软件包版本和插件)

“@graphql-codegen/cli” — is the main package, “@graphql-codegen/*” — are plugins

*   **将“graphql-codegen”命令添加到您的“package.json”脚本部分。**

Good points will be “build” or “postinstall” (will be automatically called on the package installation)

*   在你的包根目录下创建一个“codegen.yml”。这个文件将为你的“graphql-codegen”命令提供配置。检查 codegen.yml 文档

“模式”——程序应该在哪里搜索 GraphQL 模式文件。在这种情况下，我们的客户机“order-list-app”在附近的 monorepo 包“order-list-backend”中搜索服务器 GraphQL 模式。然而，**如果你使用的是第三方 API** ，那么你应该在这里放上你的 URL 端点。

“文档”——这些文件看起来像 graphql 模式，但是描述了客户端的操作。GraphQL 客户端使用“文档”来形成 graphql 请求，在后端可能会被省略。

" graph QL _ API _ build/types _ and _ hooks . tsx "-放置结果的位置

“插件”——应该生成什么代码。在这个例子中，我想要 TypeScript types+[Apollo React Hooks](https://www.apollographql.com/docs/react/api/react/hooks/)。后端没有挂钩，所以后端可以省略“typescript-react-apollo”插件。

*   **就这样！免费使用和享受大量的类型。他们会从上到下测试你的系统。**

# 您不应该将生成的 TypeScript 文件提交给 git

在“yarn install”或“npm install”之后，文件将直接从 graphql 模式编译，没有必要提交它们。这样，你的 GraphQL 模式将成为一个**真实的单一来源**。

# 您应该在每次架构更新时重新编译 TypeScript 类型

如果已经更新了模式，应该调用“graphql-codegen”脚本来重新编译类型。不要担心忘记它。编译后的文件不会提交给 repo，CI/CD 会从头开始重新编译它们并捕捉错误。这种不一致的状态是不能断产的。

# 结论

TypeScript 代码生成易于自动化和使用。 [graphql-code-generator](https://github.com/dotansimha/graphql-code-generator) 在 github 上有 6k 颗星。这个软件包是抛光的方式以上，你可以真实地手写。

使用编译类型，您将获得:

*   更少的错误
*   更快的发展

GraphQL 不仅仅是“用更少的网络流量休息”。这是一项更加深奥的技术。

## 感谢您的阅读，

非常感谢您在评论中的反馈。