# 使用 next-API-decorator 的 Awesome Next.js API 路由

> 原文：<https://javascript.plainenglish.io/awesome-next-js-api-routes-with-next-api-decorators-d6117f963bee?source=collection_archive---------4----------------------->

![](img/a692ff5daa5d1096110fcbfe8e59d130.png)

Photo by [Matt Duncan](https://unsplash.com/@foxxmd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

构建一个现代的 web 应用程序可能是一项复杂的任务——如果你想构建某个东西，你可能会开始考虑架构，以及如何分离你的关注点，并且有许多方法可以实现。传统上来说，这意味着有一个独立的前端和后端，有独立的代码库，可能使用不同的语言、框架或技术来完成工作。

在本文中，我们将使用前端开发领域的优秀工具 Next.js 来研究一个替代方案。我们将研究一个整体架构如何变得方便和强大，而不一定会受到通常与这种方法相关联的紧耦合的影响。但是首先，快速入门一下 Next.js 是如何工作的。

# Next 如何工作

如果你是这项技术的新手，Next.js 是一个 [Jamstack](https://jamstack.org/) 框架，旨在解决一些与构建传统单页面应用程序(spa)相关的问题。它不仅支持服务器端渲染，还支持静态站点生成，允许开发者用一些静态页面构建应用(想想 marketing / about pages！)和一些加载速度超快的、SEO 友好的动态页面。根据您的用例，您通常可以使用 Next.js 来满足您的需求，很少有警告。

简而言之，这是可行的，因为当你“运行”一个 Next.js 应用程序时，你实际上是在运行一个 Node.js 服务器(尽管如果你正在构建一个完全静态的站点，你可以导出所有的静态文件并在任何地方托管它们，但我们在这里不会讨论这种方法)。因此，你的应用程序是“活的”，这与 Create React 应用程序形成对比，在 Create React 应用程序中，JS 包托管在某个地方并下载到客户端，整个应用程序仅在客户端呈现。

那又怎样？

因此，有可能定义一些只在服务器上运行的代码，而客户端永远看不到。考虑到我们只有服务器端的代码，我们可能开始做一些以前不能(更像是*不应该*)在客户端做的事情，例如，直接与数据库对话，执行需要几次单独调用的操作，等等。这听起来是不是越来越像 HTTP API 了？

Next.js 在其架构中以一等公民的身份支持这一理念。路由是自以为是的，并使用文件系统来确定应用程序中的页面路由，使用名为`pages`的目录中的文件和文件夹来建立这一点——例如，如果你在`pages/todos`中创建了一个名为`mine.tsx`的文件，你将能够在`<your-domain>/todos/mine`时在浏览器中找到该页面。路径`pages/api`下的任何东西都只会在服务器上运行。我们做到了！我们称之为[的下一个 API 路由](https://nextjs.org/docs/api-routes/introduction)。这意味着我们可以用一个代码库构建一个全栈的应用，一个“单片”架构。马上，我们免费得到了几个好东西:

*   整个应用的单一构建流程和易于运行的开发环境(只需运行`next dev`)
*   更简单的部署(在任何节点兼容的环境中，`next build`然后是`next start`)
*   默认情况下，没有 CORS 担心，前端和后端是相同的起源！
*   默认情况下类似 Monorepo 的共享(同样考虑`tsconfig`、`jest`、`eslint`)，无需使用类似`lerna`的 monorepo 管理器

更有经验的开发人员可能会认为这样的方法是一种倒退，但它更像是朝着更好地整合代码和资源迈出的一步，这是有争议的。逻辑关注点可以被分离，而无需物理分离本身，整体架构开始对 Web 应用程序更有意义，最显著的是增量静态再生和服务器端呈现的兴起。

## API 路线

如文档中所列，用 Next 构建 API 路由看起来很像用 Node.js 构建基本 API:

Taken from the Next.js docs (linked above!)

简单明了。您可以使用这种方法非常快速简单地构建一些服务器端功能！

但是，如果我们想开始构建一个 REST API，在同一个端点上区分不同的 HTTP 方法，根据资源对我们的 API 建模，会怎么样呢？如果我们想开始将行为组合到我们的 API 端点中会怎么样？

我们的例子很快扩展成这样:

Not super nice…

这可能是最好的情况，因为我们已经能够将所有实际的业务逻辑分解到函数`doSomething`、`checkAuth`、`doSomethingElse`和`doAThirdThing`中。一旦我们开始接收请求体，情况可能会变得更糟。并不可怕，但是我们可以使它更容易阅读，更容易维护。

## NestJS

通常，开发人员在构建 API 时会选择框架，因为它们提供了表示资源的替代方法，以及许多旨在简化这一过程的工具和实用程序。一个这样的例子是 [NestJS](https://nestjs.com/) (不要与 Next.js 混淆！).这是一个内置电池的强大“构建高效、可伸缩的服务器端应用程序的框架”。深受 [Angular](https://angular.io/) 的启发，这个框架允许开发者使用抽象来表示 API 路线，包括可重用的服务、控制器、模块等等。

下面是从其文档中复制的一个简单示例:

正如我们所看到的，这种方法使用 OOP 思想和 decorators 来实现前面描述的目标。我们只指定我们打算作为类上的方法使用的 HTTP 方法，而不是函数中的控制流路径。声明性更强一点，如果我们希望构建 REST API，这是一个很好的基础。

那么接下来我们如何利用这种方法。JS API 路由？

## 下一个 api 装饰者

这个库是由阿姆斯特丹的电子商务技术机构 AMS 的 [Story 的优秀人员编写的，他们决定使用这些概念开发一个解决方案，使构建 API 更容易与 Next.js 一起扩展。](https://storyofams.com/)

让我们重温一下我们之前使用他们的库重写的复杂示例，以演示它是如何工作的:

正如我们所看到的，我们改变了表达资源处理器的方式，用一个类替换了一个函数。最重要的是，该类的方法用 decorators 进行了注释，以表达它们的目的。

现在，由你决定你更喜欢哪一个，因为这种方法并不会使它更简洁。但是，如前所述，它确实将我们描述资源的方式从命令式转变为声明式。我在构建 Next.js APIs 时发现，这种方法更容易维护，因为随着应用程序的增长，最终每条路线和每个处理程序**会**和**会**变得更加复杂。

## 定制装饰

这个例子中我想看的最后一件事是我们现在在这个处理程序中的一些方法上看到的`requiresAuth`装饰器。我最近为一个项目写了类似这个自定义处理程序的东西，它被证明非常有用。这是通过使用由`next-api-decorators`提供的`createMiddlewareDecorator`工具完成的:

Instant, composable protection for any route + method combo!

很强的东西💪

这种方法非常灵活，可以应用于这两个类及其方法，以适应各种用例并理清您的实际业务逻辑。

# 包扎

我在这里展示的例子非常简单，只是让您了解使用 Next.js 及其 API routes 构建全栈应用程序的实用方法，以及如何使用`next-api-decorators`使其成为可伸缩的服务器端应用程序。

如果你有兴趣了解更多，请查看这个惊人的库的[文档](https://next-api-decorators.vercel.app/)和[回购](https://github.com/storyofams/next-api-decorators)。

感谢阅读！

💙

*更多内容请看*[***plain English . io***](http://plainenglish.io/)