# Interface Forge:一个生成测试数据和夹具的 TypeScript/JavaScript 库

> 原文：<https://javascript.plainenglish.io/generating-test-data-and-fixtures-with-interface-forge-5a5548233aa5?source=collection_archive---------5----------------------->

![](img/b39a8ead59e0f07ca9882633fbe84fb8.png)

Source: [https://www.pxfuel.com/](https://www.pxfuel.com/)

在这篇文章中，我介绍了 [Interface Forge](https://github.com/Goldziher/interfaceForge) ，并讨论了它的一些用例，我喜欢把它称为“模拟驱动开发”。

*关于 TypeScript 的注意事项* : [接口伪造](https://github.com/Goldziher/interfaceForge)是用 TypeScript 编写的，它提供了强大的 TS 支持。因此，下面所有的例子都使用 TS 作为基础，但是这并不意味着你不能使用普通的 JS 来使用这个库，你当然可以这样做。

## 生成动态测试数据

这让我想到了编写这个库的必要性——我在工作中开始了一个新项目，并使用 TypeORM +附带的 NestJS API 开发了一个数据模型。我需要用一些测试数据播种数据库，为 API 和定制的 TypeORM 存储库编写集成测试。

例如，假设我们有一些实体:

当运行大多数后端测试时，我需要用至少一个用户播种数据库。一种选择是使用硬编码的测试数据，就像这样:

这种方法对于单个测试套件来说是不错的，但是如果我想要重用这个逻辑，或者如果我想要能够创建多个用户，这将是不可伸缩的。此外，如果我想在后端服务和前端服务之间共享数据，这也是不可能的。

这就是动态数据生成发挥作用的地方，即进入[界面伪造](https://github.com/Goldziher/interfaceForge):

在上面的例子中，我们从 Forge 接口库导入了`TypeFactory`,并使用它创建了两个工厂——一个用于 UserProfile，另一个用于 User。

因为字段“id”、“createdDate”、“updatedDate”和“user”将由 TypeORM 自动设置，所以我们需要将它们从传递给 TypeFactory 的泛型中删除。为此，我们使用内置的 TypeScript 函数 Omit。

我们还使用 [Faker.js](https://github.com/marak/Faker.js/) 为我们生成模拟值——这是一个非常好的库。这里需要注意的是，我们作为默认值传递给 TypeFactory 构造函数的是一个函数——这确保了每次我们使用工厂来构建 Faker.js 方法的嵌套调用时都会被求值。

最后，我们还使用了一个内置的[接口 Forge](https://github.com/Goldziher/interfaceForge) helper 方法`.iterate`，它生成一个无限生成器，通过每个工厂调用为职业生成一个值。你可以在文档中读到更多关于这个[的内容。](https://goldziher.github.io/interfaceForge/)

有了这些工厂，我们现在可以像这样重写我们的测试:

或者如果我们需要很多用户:

我们产生了 10 个用户。干净利落。

## 使用复杂类作为接口的技巧

例如，如果您的实体扩展了另一个类，如 TypeORM 内置的`BaseEntity`类，那么在 TypeScript 中使用一个类作为接口可能比上面的例子更困难。在这种情况下，正在讨论的类将包含来自基类的许多我们不想包含在工厂结果中的属性和方法。以这个抽象基类为例:

为了解决这个问题，我们可以创建一个 TypeScript helper 类型，它采用两个泛型参数——实体类和它扩展的基类——然后从结果实体中省略所有“base”键:

现在我们可以这样使用这个类型:

## 创建装置

在我前面提到的新项目范围内，我和我的同事创建了一个 TypeScript monorepo，它允许我们在新应用程序的各个组件之间共享代码。

这当然是在应用程序的各个组件中使用相同语言的独特优势的一部分，NestJS 推荐的模式是创建 dto——或数据传输对象——定义后端和前端之间的接口。

假设我们的 UserDTO 类包含了由扁平对象中的 User 和 UserProfile 实体表示的大部分数据:

我们可以为这个类创建一个工厂，我们可以在后端 API 测试和前端测试中使用它。然而，对于前端测试，我们也将使用[快照测试](https://jestjs.io/docs/snapshot-testing)，这要求我们有确定性的测试数据，否则我们的快照将在每次运行时失败。为此， [Interface Forge](https://github.com/Goldziher/interfaceForge) 允许你将生成的测试数据保存为 fixture 文件。为此，我们只需使用`FixtureFactory`而不是`TypeFactory`来创建 UserDTOFactory:

或者，如果我们想重用以前的工厂并减少代码重复:

我们现在可以像使用以前的工厂一样使用这个工厂，因为`FixtureFactory`扩展了`TypeFactory`，但是我们也可以用它来创建夹具:

当上面的测试第一次运行时，一个模拟用户 DTO 对象将被创建并写入一个文件。在这个测试的后续运行中，这个文件将被读取，它的内容将在测试中使用。除非工厂的数据结构改变，否则不会改变。

这是通过对保存到磁盘的数据的对象键和工厂输出的对象进行深入比较来确定的。这种方法确保工厂中的更改反映在保存到磁盘的数据的更改中，并随后反映在失败/更新的快照中。

## 使用模拟数据进行快速原型开发

我想在这里讨论的最后一个用例是使用模拟数据，以便更快地在代码库的不同组件之间移动——例如前端和后端，或者需要通信的不同微服务。

简而言之:模拟数据允许开发人员在不同的组件上工作，以就他们各自的组件或模块之间的接口达成一致，即数据的“形状”，然后彼此独立地进行——至少在一定程度上。

假设我们同意后端在给定的 API 端点向前端提供一个用户对象。此端点尚未实现，但这不应该成为前端开发人员原型化用户配置文件页面的障碍。

例如，添加一个占位符 API 客户端方法是一个很好的起点。假设我们最终的方法看起来像这样:

我们可以从这个开始:

我们有一个接受`id`的异步方法，它使用工厂的异步`.build`返回一个符合预期接口的用户对象。

然后，我们可以在开发环境中使用这个逻辑来构建给定页面的原型。或者，我们可以使用像[故事书](https://storybook.js.org/)这样的工具，在这种情况下，我们可以这样做:

我们的 UserProfile 页面加载在 storybook 中，带有一个使用工厂生成的“用户”属性。这允许我们完全独立于后端 API 的开发来创建`UserProfile`页面以检索数据。

## 摘要

在本文中，我介绍了[Interface Forge](https://github.com/Goldziher/interfaceForge)——一个用于生成模拟数据和装置的 TypeScript/JavaScript 库。为此，我给出了一些用例及测试示例，并讨论了一些“模拟驱动开发”的示例。也就是说，使用模拟数据进行开发，促进更快的原型开发和更好的测试。

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*