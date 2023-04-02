# 深入了解 Angular 12

> 原文：<https://javascript.plainenglish.io/angular-12-in-depth-7741e759c72?source=collection_archive---------0----------------------->

Angular 12 刚刚发布。是时候发现新的东西了！

![](img/37f9e3f8b944d331fb0f7bcf7ed15af6.png)

在本文中，我将回顾这个全新版本中(几乎)所有值得注意的地方。我还将强调 Angular 的变化，就像我以前关于 [Angular 11](https://medium.com/swlh/angular-11-in-depth-9a7372b4a600) 和 [Angular 10](/angular-10-in-depth-a48a3a7dd1a7) 的文章一样。

如果你只是在寻找鸟瞰图，那么看看[官方发布的公告](https://blog.angular.io/angular-v12-is-now-available-32ed51fbfd49)。在这里，我将更深入地研究发行说明。

# 加入常春藤联盟…

Angular 团队从 2018 年开始致力于 [Ivy](https://angular.io/guide/ivy) (新编译&渲染流水线)。终于用 Angular 8 发布了。自 Angular 9 以来，Ivy 一直是新项目的默认设置，生态系统正在慢慢向它迁移。在 Angular 12 中，*旧的视图引擎现已正式废弃*。它将在未来的主要版本中被删除。此外，使用视图引擎创建新的应用程序也是不可能的。最后，Ivy 现在是新库项目的默认选项。

在这一点上，由于`ngcc`(Angular 的兼容性编译器)，库作者仍然可以依赖 View Engine，但现在真的是他们评估是否可以将库迁移到 Ivy 的时候了。几周前，Minko Gechev 发表了一篇文章来详细解释这一点。另外，检查相关的 [RFC](https://github.com/angular/angular/issues/38366) 。

如果您不知道，`ngcc`是在您创建一个 Angular 项目或安装依赖项之后运行的小进程。当你看到像`Compiling ... : es2015 as esm2015`这样的消息时，是`ngcc`在做它的工作。`ngcc`所做的是编译依赖视图引擎的库，这样常春藤就可以使用它们。

像我一样，你可能已经注意到`ngcc`需要很多时间来执行，并且对开发者体验有非常负面的影响。这就是为什么有角生态系统尽快迁移到常春藤是至关重要的。第二，直到生态系统的大部分已经转移，Angular 团队将不得不保留视图引擎，这是有问题的，原因有很多。最后，依赖视图引擎的库不能依赖常春藤。

库作者大概不能太快迁移到 Ivy，但是他们应该明确地推动不情愿的用户升级。无论如何，前进的道路是尽快将所有的东西迁移到 Ivy-)

顺便说一下，如果你不熟悉 Angular 的内部结构，那么可以看看下面的视频。

卡拉·埃里克森的《角度是如何工作的》:

深入了解 Alex Rickabaugh 的 Angular 编译器:

那边还有一篇关于常春藤[的优秀文章](https://medium.com/angular-in-depth/all-you-need-to-know-about-ivy-the-new-angular-engine-9cde471f42cf)。

# 再见量角器

4 月，Angular 团队已经宣布计划在 2022 年底结束对[量角器](https://www.protractortest.org/)的支持。

从 Angular 12 开始，量角器将不会默认包含在新项目中。相反，Angular CLI 将提供使用其他解决方案的选项，如 [Cypress](https://www.cypress.io/) 、 [WebdriverIO](https://webdriver.io/) 或 [TestCafe](https://testcafe.io/) 。这意味着将来应该继续支持`ng e2e`命令。

正如[公告](https://github.com/angular/protractor/issues/5502)中所解释的，早在 2013 年创建量角器的时候， [WebDriver](https://developer.mozilla.org/en-US/docs/Web/WebDriver) 就不是[标准](https://www.w3.org/TR/webdriver/)，端到端(e2e)测试很难编写，维护起来也是一场噩梦。量角器通过包装 [selenium-webdriver](https://www.npmjs.com/package/selenium-webdriver) 带来了创新的解决方案，并提供了控制执行流程的方法。

当然，从那以后，很多事情都发生了变化。我们现在有了`WebDriver` API、`async`和`await`(甚至顶级`await`，woah)。还有，生态系统也进化了。像[赛普拉斯](https://www.cypress.io/)、[剧作家](https://playwright.dev/)、[木偶师](https://pptr.dev/)这样的解决方案获得了很多(当之无愧的)人气。例如，像 Cypress 这样的工具提供了比量角器更好的开发体验，利用了现代标准，甚至支持跨浏览器测试(以及其他强大的功能)。当前事实上的 e2e 测试工具的另一个好处是它们是框架不可知的，这是非常有价值的。

长话短说，维护量角器对于棱角分明的团队来说意义不大。进化量角器现在将需要太多的努力，并导致大量的突破性变化。你可以在 RFC 中找到更多的细节，这是一篇有趣的文章。

对于已经投入大量时间和精力用量角器编写 e2e 测试的团队/项目来说，时间表很重要。Angular 团队仍在忙于评估通过 RFC 收集的反馈，所以今年晚些时候我们可能会知道更多。

不管怎样？如果你还没有尝试过 Cypress，你不会失望的！对了，我一直推荐大家开始使用 [Nrwl NX](https://nx.dev/) ，一个很棒的解决方案，包括对 Angular、React、Next.js、Cypress 等等的支持；-)

# 无效合并

Angular 12 支持在角度模板中使用[无效合并运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)。这太棒了。从版本 3.7 开始，TypeScript [就支持该操作符。](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#nullish-coalescing)

如果你没有听说过这个操作符，那么让我给你简单解释一下。这个想法是为了能够定义一个回退值，以防出现`null`或`undefined`。这里有一个例子:

```
let x = foo ?? true;
```

如果`foo`是`null`或`undefined`，那么`x`将被设置为`true`(即回退值)，我们可以将其设置为任何我们喜欢的值。

如果没有这个令人敬畏的`??`操作符，我们将不得不这样写:

```
let x = foo !== null && foo !== undefined ? foo : true;
```

既然 Angular 也支持它，我们最终可以编写这样的表达式:

```
{{ age ?? calculateAge() }}
```

而不是旧的和更冗长的替代方案。整洁！

你可以在这里了解更多关于这个变化[。](https://github.com/angular/angular/issues/36528)

你可以在 [TypeScript 手册](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#nullish-coalescing)和 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) 中找到更多关于 nullish 合并的信息。

# TypeScript 4.2 支持

Angular 12 引入了对 [TypeScript 4.2](https://devblogs.microsoft.com/typescript/announcing-typescript-4-2/) 的支持，这意味着我们现在可以使用大量*新的精彩语言特性。此外，对 TypeScript 4.0 和 4.1 的支持也已取消。*

下面是 TS 4.2 包括的内容的简要概述:

*智能类型别名保留*:代码编辑器显示预期类型，而不是之前出现的原始类型。你可以在这里了解更多。

*Tuple 类型中的前导/中间 rest 元素*:我们现在可以在 Tuple 中的任何地方包含 Rest 元素(有一些注意事项)。对于我们这些经常依赖元组的人来说，这很酷。点击了解更多信息。

*理解你的项目结构* : TS 4.2 包括[一个名为`--explainFiles`的新标志](https://devblogs.microsoft.com/typescript/announcing-typescript-4-2/#explain-files)，它指示打字稿输出关于为什么一个文件被包含在你的程序中的信息。这对于故障排除非常有用。

未调用函数检查的改进:TypeScript 现在可以检测更多函数未被调用的情况。例如当写`foo`而不是`foo()`时。更多细节和例子可以在这里找到[。](https://github.com/microsoft/TypeScript/issues/40197)

*析构变量现在可以显式标记为未使用的* : `let [_first, second] = getValues();` ，太牛逼了；`noUnusedLocals`启用时不再出错！

实际上还有很多，比如对`in`操作符更严格的检查，以及一些可能会影响你的突破性变化。因此，请务必查看[发行说明](https://devblogs.microsoft.com/typescript/announcing-typescript-4-2)。

# Webpack 5 支持

Angular 11 为我们带来了对 Webpack 5 的[实验支持。在 Angular 12 中，Webpack 5 支持现已投入生产。w00t！](https://medium.com/swlh/angular-11-in-depth-9a7372b4a600)

如果你没有看过 Webpack 5，你会感到惊讶。Webpack 5 早在 2020 年 10 月就发布了，所以到目前为止还是相当稳定的。Webpack 目前是[版本 5.37](https://github.com/webpack/webpack/releases/tag/v5.37.0) (前几天发布)。

这里有一个简短的解释，关于 Webpack 5 的变化，以及为什么我对此如此高兴！

首先，如您所知，Webpack 是 Angular CLI 难题的关键部分，它在包大小、构建性能等方面起着重要作用。

第二，Webpack 5 是一个重要的版本，这是有原因的。它包含了许多突破性的变化，这解释了为什么 Angular 和生态系统中的大量实用程序/库需要一段时间才能升级。

在发行说明中，Webpack 团队指出 Webpack 5 侧重于:

*   使用*持久*缓存提高构建性能
*   用更好的算法和默认值改进长期缓存
*   通过更好的树抖动和代码生成来提高包的大小
*   提高与网络平台的兼容性
*   清理内部结构
*   现在引入突破性的改变(哈哈),允许他们尽可能长时间地留在 v5 上

Webpack 5 最酷的特性是其对模块联盟的[支持，这为](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#module-federation)[创建微型前端](https://levelup.gitconnected.com/micro-frontends-step-by-step-using-react-webpack-5-and-module-federation-e4b9d840ec71)提供了必要的基础。这有点超出了本文的范围，但是很快，模块联盟使得不同的构建可以表现得像一个巨大的连接的模块图，并且允许我们从远程构建导入和使用模块。查看[官方文件](https://webpack.js.org/concepts/module-federation/)了解更多。

如果你好奇的话，那你应该看看[曼弗雷德·施泰尔](https://twitter.com/ManfredSteyer)关于这个主题的演讲:

在主要的变化中，Webpack 5 删除了所有之前被否决的东西(例如`NoEmitOnErrorsPlugin`、`ModuleConcatenationPlugin`、`NamedModulesPlugin`)，以及`IgnorePlugin`和`BannerPlugin`。

此外，先前自动注射的 Node.js 聚合填料已被移除；这是该版本中最大的变化之一。这些聚合文件最初允许 Webpack 允许我们在浏览器中使用为 Node.js 制作的模块。这很酷，但也有一个主要的缺点:捆绑包更大。此外，这些聚合文件越来越没用了，因为有浏览器兼容的替代库或支持浏览器的特定发行版。从 Webpack 5 开始，由于这些聚合填料将不再自动添加，我们可能会偶然发现一些惊喜。例如，如果我们在浏览器中使用为 Node.js 制作的模块，却没有意识到它以前的工作得益于 Webpack。您可以在这里了解更多关于[的信息。](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#automatic-nodejs-polyfills-removed)

Webpack 5 引入了对长期缓存的更好支持。在生产模式下，它现在默认包含新算法:

*   `chunkIds: "deterministic"`
*   `moduleIds: "deterministic"`
*   `mangleExports: "deterministic"`

如该值所示，这些算法为块和模块分配确定性标识，为导出分配确定性名称。

Webpack 5 能够通过跟踪对导出的嵌套属性的访问来执行嵌套的树抖动(欢迎使用 Matrix)，这将进一步改进树抖动。此外，它现在可以[分析模块](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#inner-module-tree-shaking)的导出和导入之间的依赖关系。还有对[普通树摇动](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#commonjs-tree-shaking)的改进。此外还有大量的优化。

Webpack 5 还包括许多改进开发者体验的变化。例如，有一个新的命名为块 id 算法[在开发模式下默认启用。这种新算法给组块起了人类可读的名字。`target`属性也得到了极大的](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#named-chunk-ids)[提升](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#improved-target-option)。

老实说，我在这里没有足够的空间来涵盖 Webpack 5 的所有新内容，[那里](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#json-modules)的[只是](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#asset-modules) [方式](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#uris) [太](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#async-modules) [太多](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#resolving)。所以我就讲到这里。-)

如果您只是通过 Angular CLI 间接使用 Webpack，那么大部分对您来说应该是“透明”的。但是如果你在你的项目中使用了一个[定制的 Webpack 版本](/customizing-your-angular-apps-webpack-configuration-4099144949fc)，那么你可能应该看一下[迁移指南](https://webpack.js.org/migrate/5)。

最后，如果你对 Webpack 的下一步很好奇，那么看看 2021 年的[路线图，当然还有](https://webpack.js.org/blog/2020-12-08-roadmap-2021/)[的最新发布说明](https://github.com/webpack/webpack/releases/)。

# IE11 支持已被否决

听起来很悲伤(我在骗谁呢？)，Angular 12 是在贬低对 IE11 的支持。对于我们大多数人来说，Internet Explorer 已经死了，但不幸的是，许多组织仍然在生产中使用它。IE 11 的支持将因此被 Angular 13 移除，这意味着那些组织确实需要开始远离 IE(无论如何这是一件好事)。别再找借口了！；-)

一旦 IE 支持消失，Angular 将变得更小、更快，从而对我们所有人都更好。此外，一旦保持向后兼容传统浏览器的负担消失(IE11 是最后一个！)，那么 Angular 将能够利用现代 API(例如， [CSS 变量](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)、[交集观察者](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)、 [CSS 网格](https://css-tricks.com/snippets/css/complete-guide-grid/)、[代理](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)、[网页动画](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API)，以及[更多](https://github.com/angular/angular/issues/41840))。

真恨不得 IE 支持都没了！

# 默认情况下严格

是的——是的——是的！从 Angular 12 开始，CLI 中默认启用 Angular 的[严格模式。这太棒了。](https://angular.io/guide/strict-mode)

如你所知，我是 TypeScript 的严格模式的忠实粉丝，但也是 Angular 的严格模式的忠实粉丝。如果你想知道更多，那么看看我去年写的文章和 Minko Gechev 的文章[解释这个变化](https://blog.angular.io/with-best-practices-from-the-start-d64881a16de8)。

# 默认生产版本

到目前为止，运行`ng build`命令创建了一个开发版本。从 12 年开始，`ng build`将默认为生产版本。

希望它能帮助一些团队避免犯在生产环境中构建和部署开发构建的错误。虽然，我担心犯那个错误的团队仍然会有其他的问题要处理；-)

# 内联样式的 Sass 支持

Angular 很久以前就支持 Sass，但是到目前为止，我们只能在外部样式表中使用 Sass。有了 Angular 12，现在可以将 Sass 与内联组件样式一起使用(即在`styles`属性中)。

这需要通过将新的`inlineStyleLanguage`属性设置为`angular.json`中的`true`来启用。

# 顺风支架

[顺风](https://tailwindcss.com/)现已获得 Angular 官方支持。实际上，支持是在 11.2 版的 Angular CLI 中引入的。

tailwind[正忙着接管世界](/why-tailwind-just-in-time-mode-is-a-game-changer-and-how-to-use-it-right-now-dubois-sébastien-182db2e64e26)，尤其是现在它有了一个 [rad JIT 编译器](/why-tailwind-just-in-time-mode-is-a-game-changer-and-how-to-use-it-right-now-dubois-sébastien-182db2e64e26)，Angular 中有对它的内置支持真是太棒了。

以前，向 Angular 项目添加 Tailwind 需要[定制 Webpack 构建](/adding-tailwind-support-to-a-nrwl-nx-workspace-with-angular-and-storybook-bf890ea882e)。不再是了！现在，添加 Tailwind 就像安装软件包一样简单，使用`npx tailwindcss init`创建`tailwind.config.js`文件，并确保启用 [Tailwind 的 JIT 模式](/why-tailwind-just-in-time-mode-is-a-game-changer-and-how-to-use-it-right-now-dubois-sébastien-182db2e64e26)。

# Http 改进

Angular 12 围绕其 HTTP 支持引入了许多改进。

## 请求和拦截器的元数据

首先，`HttpClient`现在可以用于存储和检索请求的定制元数据。这对 HTTP 拦截器特别有用。这个功能可以通过新的`HttpContext`使用。

以前，为拦截器提供上下文很复杂，但现在简单多了。现在，`HttpClient`提供的不同 HTTP 方法包括一个新的`context: HttpContext`选项，我们可以用它来传入一个 map。

[Netanel Basal](https://twitter.com/NetanelBasal) 写了一篇关于这个的文章，[想了解更多的话可以去看看](https://netbasal.com/new-in-angular-v12-passing-context-to-http-interceptors-308a1ca2f3dd)。

## HttpParams 上的 appendAll

`HttpParams`类现在有了一个新的`appendAll`方法，可以很容易地一次添加一组参数:

```
appendAll(params: {[param: string]: string|string[]}): HttpParams
```

## 参数现在可以作为数字和布尔值传递

以前，数字和布尔值不能直接用作 HTTP 参数。我们必须把它们转换成字符串。不再是了！

## HttpStatusCode

Angular 以 const enum 的形式为 HTTP 状态代码引入了自己的可读名称列表。

以前，如果我们想拥有人类可读的名称，我们必须引入自己的解决方案。多亏了这个新功能，我们现在可以使用`HttpStatusCode`。

例如:

```
if (response.status === HttpStatusCode.Ok) { 
  ... 
}
```

对于那些在后端和前端都使用 TypeScript 的人来说，这不是非常有用(因为我们可能都已经有了自己的抽象)，但是如果您的项目只在前端使用 TypeScript/Angular，那么这是一个很好的改进。

## xhr 工厂

`XhrFactory`类已经被移动到一个不同的包中。现在由`angular/common`曝光，而不是`angular/common/http`。

注意，升级中已经包含了一个迁移，所以即使运行`ng update`您也不会注意到；-)

# 路由器变更

角度路由器在角度 12 中有一点改变。

首先，增强了`routerLinkActiveOptions`指令。现在，可以指定我们是否需要 URL 的不同部分精确匹配，以便向链接添加 CSS 类。

以前，我们只需要完全匹配(或不匹配)整个 URL:

```
<a
  routerLink="/products/foo"
  routerLinkActive="highlight-product"
  [routerLinkActiveOptions]="{ exact: true }"
>
  foo
</a>
```

现在，我们可以为路径、查询参数、矩阵参数和片段提供细粒度的匹配规则:

```
<a
  routerLink="/products/foo"
  routerLinkActive="highlight-product"
  [routerLinkActiveOptions]="{ paths: 'exact', queryParams: 'subset', matrixParams: 'ignored', fragment: 'ignored' }"
>
  foo
</a>
```

支持的值有`exact`、`ignored`和`subset`，可用于`queryParams`和`matrixParams`。对于路径，可以传入`exact`或`subset`，传入`fragment`的`exact`或`ignored`。

注意，路由器的`isActive`方法也接受这些新选项。

## 片段可为空

到目前为止，`ActivatedRouteSnapshot.fragment`不可为空。这已经随着 Angular 12 而改变了。不过不要太担心；`ng update`为您提供保障。

# 形式

## 对发射事件的更多控制

`emitEvent`选项被添加到`FormGroup`和`FormArray`的各种方法中。由于这一改变，现在在更多的情况下可以控制是否需要发出事件。

例如，以前当使用`FormGroup`的`removeControl`方法移除控件时，总是会发出一个事件。有了这个改变，我们现在将能够避免这样的问题。

`emitEvent`选项被添加到`FormGroup`的以下方法中:

*   `addControl`
*   `removeControl`
*   `setControl`

以及以下`FormArray`的方法:

*   `push`
*   `insert`
*   `removeAt`
*   `setControl`
*   `clear`

## 最小和最大验证器支持模板驱动的表单

Angular 的`min`和`max`验证器现在可以用于模板驱动的表单:

```
<input [(ngModel)]="foo.bar" [min]="min" [max]="42" />
```

请注意，这是一个突破性的变化，因为这些在以前会被忽略。

# i18n

Angular 的 i18n 系统在此版本中发生了变化。

正如公告博客中指出的，目前有许多遗留消息 id 格式正在使用。这些都很脆弱，可能会因为空白、格式化模板和 ICU 表达式而出现问题。

Angular 12 引入了一种新的规范消息 id 格式(即一种格式来管理它们)。这种格式更有弹性，也更直观。

这种格式将减少应用程序中不必要的翻译无效和相关的重新翻译成本，例如，在应用程序中，由于空白改变，翻译不匹配。

从 v11 开始，新的项目被自动配置为使用新的消息 id，现在已经有工具可以用现有的翻译迁移现有的项目。如果您担心，那么您可以使用`localize-migrate`工具来迁移您的消息 id:

```
ng extract-i18n --format=legacy-migrate npx localize-migrate --files=*.xlf --map-file=messages.json
```

你可以在这里找到更多关于[的信息。](https://angular.io/guide/migration-legacy-message-id)

# 性能改进

在此版本中，有许多性能改进。最明显的一个是 Webpack 5 的升级，但还有更多:

许多未使用的方法已从`DomAdapter`中删除。它很酷，因为它的方法不是树摇动的，并且被包含在所有的角度应用中，正如在[相应的 PR](https://github.com/angular/angular/pull/41102) 中解释的。

Angular 现在为安全的属性访问生成更少的代码；例如像`a?.b`这样的模板表达式和新支持的空合并:`a ?? b`。

Angular 编译器现在支持增量编译，即使存在重定向的源文件。以前，在对经过重复数据消除的源文件进行类型脚本编写时，先前编译的工作无法重用。你可以在这里阅读更多关于那个[的内容。](https://github.com/angular/angular/issues/41475)

Angular 编译器现在缓存源文件的文件系统路径。之前反复调用`fs.resolve()`，耗时。

`getDirectives`功能得到了改进。随着这一变化，`ng`名称空间也进行了扩展，包括了一个新的`getDirectiveMetadata`实用程序。

还有更多。

# ng API 改进

Angular 12 改进了我们可以从浏览器开发工具中使用的`ng` [调试 API](https://juristr.com/blog/2019/09/debugging-angular-ivy-console/) 。

有一个叫做`getDirectiveMetadata`的新函数，可以用来检索关于组件和指令的信息。我不认为我们会经常需要它，但是未来的开发工具改进很可能会依赖于它。你可以在这里找到更多的。

还实现了一个名为`esetProfiler`的新分析器功能，它在生产模式下也是可用的。这个新函数可以在许多场景中调用。例如，它可以用来跟踪模板创建持续时间、模板更新、生命周期挂钩处理等。同样，这个 API 将被即将到来的开发工具所利用，为我们提供更多关于我们的应用程序在运行时如何执行的信息。

在这一点上，这仍然是实验性的，但是我想我们以后会听到更多关于它的内容。我很好奇是否/何时像 Sentry 这样的工具会集成对收集这种信息的支持，以便为我们提供有用的性能仪表板。

# 新的开发工具

Angular 12 发布几天后，Angular 团队[宣布](https://blog.angular.io/introducing-angular-devtools-2d59ff4cf62f)为谷歌 Chrome 提供全新的 Angular 开发工具。你可以在这里下载那些。

使用这个全新的浏览器扩展，您可以在开发过程中轻松检查您的 Angular 应用程序。它支持:

*   可视化应用程序的结构(例如，检查组件树)
*   浏览和编辑组件
*   剖析性能

使用嵌入式概要分析器，我们可以记录变更检测事件，并在事件发生时进行预览。对于每个变化检测周期，我们可以查看花费了多长时间，哪些组件花费了最长时间，该周期是否导致了帧丢失。

Angular 以前通过[占卜](https://augury.rangle.io)项目拥有半官方开发工具(这是新工具的基础！)，但这些与常春藤不兼容。所以这对 Angular 社区来说是个好消息！

# 还有更多…

在这个版本中还有很多小的变化。这里有一个快速概述。

## APP_INITIALIZER 现在支持可观测量

到目前为止，还不能通过`APP_INITIALIZER`使用 Observables。从 Angular 12 开始，我们现在可以这样做了，这将允许更干净的代码！

如果您还不知道 Angular 的这个特性，`APP_INITIALIZER`是[的一个标记](https://angular.io/api/core/APP_INITIALIZER)，我们可以用它来定义在应用程序初始化期间需要执行的函数。如果这个函数是异步的，返回一个`Promise`或者一个`Observable` (new :p)，那么 Angular 在启动应用程序之前等待它完成。

这一变化非常受欢迎，因为这意味着我们可以使用 RxJS 编写更多的代码，而不是“退回到”T4 API。

你可以在这里阅读更多关于那个[的内容。](https://github.com/angular/angular/issues/15088)

## 动画的运行时控制

以前，禁用动画的唯一方法是提供`NoopAnimationsModule`。从 Angular 12 开始，现在可以基于运行时信息禁用动画，使用`BrowserAnimationModule.withConfig`方法，并向其传递`disableAnimations`布尔属性。

## 一种新的位置服务历史查询方法

Angular 的`LocationService`现在包含了一个`historyGo`方法，可以用来导航到会话历史中的特定页面，通过它与当前页面的相对位置来识别。该方法对应于原生的`window.history.go`方法。[查看 MDN](https://developer.mozilla.org/en-US/docs/Web/API/History_API#moving_to_a_specific_point_in_history) 中的一些例子。

## 语言服务改进

语言服务为 ide 提供了所有关于角度代码的有用见解，在这个版本中也得到了改进。

在 Angular 12 中，语言服务是默认启用的(以前需要我们选择加入)。

从 Angular 12 开始，它还会检测[严格模板类型检查](/angular-template-type-checking-e2c99c50f999)是否未启用，并且[会建议您启用那些](https://github.com/angular/angular/pull/40423)。

语言服务现在还包括性能跟踪功能，可以用来跟踪性能。这可以在 VSCode，[中启用，如这里所解释的](https://github.com/angular/angular/pull/41319)(尽管这是相当低的级别)。

如果你还不知道语言服务，看看官方文件，或者忍者小队写的博客，或者视频介绍。

## 直接从 HTML 模板禁用 lint 规则

Angular 模板编译器现在跟踪 HTML 注释。

以前，不可能从 HTML 模板中禁用 linter 规则，因为 Angular 模板编译器会忽略注释。解决方法是从组件的控制器中禁用整个模板的那些规则。由于这一改变，现在可以从模板中更精确地完成这项工作:

```
<!-- eslint-disable-next-line @angular-eslint/template/no-any -->
<span>{{ $any(foo).bar }}</span>
```

干净代码万岁！

## 数据管道现在支持 ICU 标准的独立一周

以前，[不可能使用 DatePipe 将日期格式化为独立的一周中的某一天。](https://github.com/angular/angular/issues/26922)

由于这一改变，现在支持芬兰语的日期格式，我确信这对于 Angular 社区的一小部分人来说是个好消息。

## 在可注入的装饰器的字段中提供对 forwardRef 的支持

现在可以在`@Injectable`装饰器的`providedIn`字段中使用`forwardRef`。

## ResourceHost 接口上的新 transformResource 挂钩

一个`transformResource`方法被添加到了`ResourceHost`接口中。得益于此，工具现在可以做一些事情，比如为内联样式引入预处理支持。这就是为什么能够用内联样式支持 SASS 的原因。

你可以在这里和[这里](https://github.com/angular/angular/commit/1de04b124e1e92ea21a070c9d928664f193d220c)了解更多。

## 可以创建自定义路由器插座实现

到目前为止，创建自定义路由器插座是可能的，但是需要通过一些关卡(例如，用`ChildrenOutletContexts`注册自定义插座)。

角度 12 为定制的刳刨机出口提供了[清洁器支撑。](https://github.com/angular/angular/commit/a82fddf1ce6166e0f697e429370eade114094670)

# 错误修复

像往常一样，这个版本中包含了大量的错误修复。

以下是发行说明的副本:

*   动画:确保一致的过渡名称空间顺序([# 19854](https://github.com/angular/angular/issues/19854))([01cc 995](https://github.com/angular/angular/commit/01cc99589bc449eaf3b1de2c94636de878843fba))
*   动画:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([e 918250](https://github.com/angular/angular/commit/e918250a0624cff9bbbbdb016a069303a99fb8cc))
*   动画:移除根视图时清理 DOM 元素([# 41059](https://github.com/angular/angular/issues/41059))([c49b 280](https://github.com/angular/angular/commit/c49b28013a6c017c9afc73bbc00bb4fdcf15c70e))
*   动画:允许阴影 DOM([# 40134](https://github.com/angular/angular/issues/40134))([dad 42 c 8](https://github.com/angular/angular/commit/dad42c8cd669357f9c862023abc5f4695863040d))，关闭 [#25672](https://github.com/angular/angular/issues/25672) 中元素的动画
*   动画:移除根视图时清理 DOM 元素( [#41001](https://github.com/angular/angular/issues/41001) ) ( [a31da48](https://github.com/angular/angular/commit/a31da4850788800ba9735d617e7e3bb621a79c93) )
*   bazel:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([8503246](https://github.com/angular/angular/commit/85032460f133162cc712ab3b9f04d42ff3b6d6d9))
*   bazel:为 rules _ nodejs([# 40710](https://github.com/angular/angular/issues/40710))([696 F7 BC](https://github.com/angular/angular/commit/696f7bc))中的最新变更更新构建工具
*   bazel:更新集成测试以使用[rules _ nodejs @ 3 . 1 . 0](mailto:rules_nodejs@3.1.0)([# 40710](https://github.com/angular/angular/issues/40710))([34de 89 a](https://github.com/angular/angular/commit/34de89a))
*   bazel:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([2c 90391](https://github.com/angular/angular/commit/2c90391))
*   benchpress:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([e 721 a5d](https://github.com/angular/angular/commit/e721a5d))
*   常用:为带有 HttpClient 请求体的布尔值添加右 content type([# 38924](https://github.com/angular/angular/issues/38924))([# 41885](https://github.com/angular/angular/issues/41885))([922a 602](https://github.com/angular/angular/commit/922a60283183c47a268fd084302b2bc87267a73e))
*   通用:更新支持的节点版本范围，仅包括 LTS 版本( [#41822](https://github.com/angular/angular/issues/41822) ) ( [f2b6fd8](https://github.com/angular/angular/commit/f2b6fd87056cf3159e8ecc275ce654e47fdfa6f0) )
*   常见:视口滚动条在阴影 DOM([# 41644](https://github.com/angular/angular/issues/41644))([c 0 F5 ba 3](https://github.com/angular/angular/commit/c0f5ba3d36b2509a71d09c436d247211a58ee80d))中找不到元素，关闭 [#41470](https://github.com/angular/angular/issues/41470)
*   普通:临时再出口折旧`XhrFactory`([# 41393](https://github.com/angular/angular/issues/41393))([7 DFA 446](https://github.com/angular/angular/commit/7dfa446c4ace99f4b64069cf672dcaa3665a1f5b))
*   常见:清除位置变化监听器当根视图被移除([# 40867](https://github.com/angular/angular/issues/40867))([38524 C4](https://github.com/angular/angular/commit/38524c4d29290d3339ad2d7335a0ea84f5701d26))，关闭 [#31546](https://github.com/angular/angular/issues/31546)
*   common:允许数字或布尔值作为 http 参数([# 40663](https://github.com/angular/angular/issues/40663))([91 CDC 11](https://github.com/angular/angular/commit/91cdc11aa0347d1b71f2f732e00af9c3ff8078fc))，关闭 [#23856](https://github.com/angular/angular/issues/23856)
*   常用:避免 ngtemplate outlet([# 40360](https://github.com/angular/angular/issues/40360))([d 3705 B3](https://github.com/angular/angular/commit/d3705b3284113f752ee05e9f0d2f6e75c723ea5b))中上下文对象的变异，关闭 [#24515](https://github.com/angular/angular/issues/24515)
*   编译器:在封装样式中保留@page 规则( [#41915](https://github.com/angular/angular/issues/41915) ) ( [3e365ba](https://github.com/angular/angular/commit/3e365ba81e313ee31af7a8e9042e33fc046067e0) )，关闭 [#26269](https://github.com/angular/angular/issues/26269)
*   编译器:从`@font-face`规则中剥离作用域选择器([# 41815](https://github.com/angular/angular/issues/41815))([2a 11 CDA](https://github.com/angular/angular/commit/2a11cdab51a2d8d7f644ceca744568a1617f5242))，关闭 [#41751](https://github.com/angular/angular/issues/41751)
*   编译器:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([BAE 8126](https://github.com/angular/angular/commit/bae81269c7461063821be7beb66b516e5a8995ce))
*   编译器:非文字内联模板在部分编译中被错误处理([# 41583](https://github.com/angular/angular/issues/41583))([ab 257 B3](https://github.com/angular/angular/commit/ab257b370127dce70bd3ee7ad6d64d3a9ad5ae95))
*   编译器:没有为替代名称空间内的 ng-template 生成更新指令([# 41669](https://github.com/angular/angular/issues/41669))([2 bcbbda](https://github.com/angular/angular/commit/2bcbbda78913be014534fde72318ab09795350f9))，关闭 [#41308](https://github.com/angular/angular/issues/41308)
*   编译器:避免用向后的跨度( [#41581](https://github.com/angular/angular/issues/41581) ) ( [e1a2930](https://github.com/angular/angular/commit/e1a29308933e99ee3e0d92aae42b33834f20f50a) )解析 EmptyExpr
*   编译器:处理区分大小写的 CSS 自定义属性( [#41380](https://github.com/angular/angular/issues/41380) ) ( [e112e32](https://github.com/angular/angular/commit/e112e320bf6c2b60e8ecea46f80bcaec593c65b7) )，关闭 [#41364](https://github.com/angular/angular/issues/41364)
*   编译器:在部分组件声明([# 41353](https://github.com/angular/angular/issues/41353))([ff 9470 b](https://github.com/angular/angular/commit/ff9470b0a0196a3638f19028bba15e002cb0ff27))的 JIT 编译中包含使用的组件，关闭 [#41104](https://github.com/angular/angular/issues/41104) [#41318](https://github.com/angular/angular/issues/41318)
*   编译器:支持多个`:host-context()`选择器([# 40494](https://github.com/angular/angular/issues/40494))([07 B7 af 3](https://github.com/angular/angular/commit/07b7af3))，关闭 [#19199](https://github.com/angular/angular/issues/19199)
*   编译器:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([f 728490](https://github.com/angular/angular/commit/f728490))
*   编译器-cli:对间接模板([# 41973](https://github.com/angular/angular/issues/41973))([7a4d 980](https://github.com/angular/angular/commit/7a4d9805ea73d1b6a7659987da77d266d5e01b88))的源映射 URL 使用“”，关闭 [#40854](https://github.com/angular/angular/issues/40854)
*   编译器-cli:将链接器公开为一个 Babel 插件( [#41918](https://github.com/angular/angular/issues/41918) ) ( [8fdac8f](https://github.com/angular/angular/commit/8fdac8f4361fd4ac0f20c21c98289c19e8864347) )
*   编译器-cli:在引用发射器( [#41866](https://github.com/angular/angular/issues/41866) ) ( [75bb931](https://github.com/angular/angular/commit/75bb931889b946c243161a6ce0503bc7d08a6565) )，关闭 [#41443](https://github.com/angular/angular/issues/41443) [#41277](https://github.com/angular/angular/issues/41277) 中优先使用无别名导出
*   编译器-cli:允许链接器处理缩小的布尔值([# 41747](https://github.com/angular/angular/issues/41747))([1fb 6724](https://github.com/angular/angular/commit/1fb6724b1f66c4681ddb201bc9b5441d20f5b920))，关闭 [#41655](https://github.com/angular/angular/issues/41655)
*   编译器-cli:匹配字符串索引的部分声明([# 41747](https://github.com/angular/angular/issues/41747))([f 885750](https://github.com/angular/angular/commit/f8857507642f5d12eebf4ef1ca68b63cc51f4f81))，关闭 [#41655](https://github.com/angular/angular/issues/41655)
*   编译器-cli:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([5b 463 F4](https://github.com/angular/angular/commit/5b463f4541946c795835c9d9cfd7a21e7b0caffc))
*   编译器-cli:自动完成模板中的文字类型。([# 41456](https://github.com/angular/angular/issues/41456))([# 41645](https://github.com/angular/angular/issues/41645))([8 B2 b5 ef](https://github.com/angular/angular/commit/8b2b5ef903a21b599dfc4bfe8b0c64f7c136c3a9))
*   编译器-cli:如果组件没有内联样式，请不要出错( [#41602](https://github.com/angular/angular/issues/41602) ) ( [a5fe8b9](https://github.com/angular/angular/commit/a5fe8b95893798467c4eea2b3d38d49f6d0ce1b3) )
*   编译器-cli:确保编译器正确跟踪`ts.Program`([# 41291](https://github.com/angular/angular/issues/41291))([deac 74](https://github.com/angular/angular/commit/deacc741e0ee41666292d2e2c07812a78daf5d6f))
*   编译器-cli:防止在增量重新编译中省略默认导入([# 41557](https://github.com/angular/angular/issues/41557))([7f 16515](https://github.com/angular/angular/commit/7f1651574ee95eaaa5f636fc37be7b07d1a808e5))，关闭 [#41377](https://github.com/angular/angular/issues/41377)
*   编译器-cli:将`rootDirs`解析为绝对([# 41359](https://github.com/angular/angular/issues/41359))([3 E0 FDA 9](https://github.com/angular/angular/commit/3e0fda96b827e577cc300f46e8497cb6c810ad61))，关闭 [#36290](https://github.com/angular/angular/issues/36290)
*   编译器-cli:在类型检查配置([# 41043](https://github.com/angular/angular/issues/41043))([09 aefd 2](https://github.com/angular/angular/commit/09aefd29045db77689f4dc16a6abae09a79cfb81))中添加`useInlining`选项，关闭 [#40963](https://github.com/angular/angular/issues/40963)
*   编译器-cli: `readConfiguration`现有选项应覆盖 tsconfig 中的选项([# 40694](https://github.com/angular/angular/issues/40694))([b7c4 d 07](https://github.com/angular/angular/commit/b7c4d07e81277f7aed566e443d1d4e1395c5a2f4))
*   编译器-cli:从节点( [#40694](https://github.com/angular/angular/issues/40694) ) ( [5eb1954](https://github.com/angular/angular/commit/5eb195416bf73f2fa59de52531724d8d19392975) )扩展 tsconfig 中的`angularCompilerOptions`，关闭 [#36715](https://github.com/angular/angular/issues/36715)
*   编译器-cli:针对 rules _ nodejs([# 40710](https://github.com/angular/angular/issues/40710))([d7f 5755](https://github.com/angular/angular/commit/d7f5755))中的最新更改更新 ngcc 集成测试
*   编译器-cli:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([b 75d 7 CB](https://github.com/angular/angular/commit/b75d7cb))
*   核心:不保留动态编译的组件和模块([# 42003](https://github.com/angular/angular/issues/42003))([1449 c5c](https://github.com/angular/angular/commit/1449c5c8ff3bf706c501130fe261627effe5d212))，关闭 [#19997](https://github.com/angular/angular/issues/19997)
*   核心:围绕 ngOnDestroy 生命周期挂钩调用分析器([# 41969](https://github.com/angular/angular/issues/41969))([e9ddc 57](https://github.com/angular/angular/commit/e9ddc57f948f0cb18e3e334aeb3084d1b49689b1))
*   核心:异步管道现在与 RxJS 7([# 41590](https://github.com/angular/angular/issues/41590))([9759 BCA](https://github.com/angular/angular/commit/9759bca339b44ed78ec6aafab0336d531d285f90))兼容
*   核心:用表达式绑定([# 41882](https://github.com/angular/angular/issues/41882))([73c 6 c 64](https://github.com/angular/angular/commit/73c6c64f82d45c34203d4d18d759ad0c33a6b221))处理多个 i18n 属性，关闭 [#41869](https://github.com/angular/angular/issues/41869)
*   核心:更新支持的节点版本范围，仅包括 LTS 版本( [#41822](https://github.com/angular/angular/issues/41822) ) ( [f9c1f08](https://github.com/angular/angular/commit/f9c1f089573e0158eb5e4443658cfd25aeeeb091) )
*   核心:检测已经使用 TS 4.2([# 41305](https://github.com/angular/angular/issues/41305))([274 dc15](https://github.com/angular/angular/commit/274dc15452739e4fab2f647804a64d5b797cfed5))降级的合成构造函数，关闭 [#41298](https://github.com/angular/angular/issues/41298)
*   核心:将`emitDistinctChangesOnlyDefaultValue`切换到 true([# 41121](https://github.com/angular/angular/issues/41121))([7096246](https://github.com/angular/angular/commit/70962465b5795f0a192f745016b1c461e7c8790b))
*   核心:删除重复的空 _OBJ 常量([# 41066](https://github.com/angular/angular/issues/41066))([BF 158 e 7](https://github.com/angular/angular/commit/bf158e7ff0715aabeae3c2c1ac923bf8cc7e4cfd))
*   core:删除重复的 EMPTY_ARRAY 常量([# 40991](https://github.com/angular/angular/issues/40991))([e12d 9 de](https://github.com/angular/angular/commit/e12d9dec64bc3d02e58f8f85a65a939394fb9531))
*   核心:允许更新 EmbeddedViewRef 上下文([# 40360](https://github.com/angular/angular/issues/40360))([a3e 1719](https://github.com/angular/angular/commit/a3e17190e7e7e0329ed3643299c24d5fd510b7d6))，关闭 [#24515](https://github.com/angular/angular/issues/24515)
*   核心:使 DefaultIterableDiffer 保持副本的顺序([# 23941](https://github.com/angular/angular/issues/23941))([a 826926](https://github.com/angular/angular/commit/a826926))，关闭 [#23815](https://github.com/angular/angular/issues/23815)
*   核心:NgZone 加煤选项应正确触发 on stable([# 40540](https://github.com/angular/angular/issues/40540))([22f9e 45](https://github.com/angular/angular/commit/22f9e45))
*   元素:更新支持的节点版本范围，仅包括 LTS 版本( [#41822](https://github.com/angular/angular/issues/41822) ) ( [4f5d094](https://github.com/angular/angular/commit/4f5d094f3a385cdc6d93c7676457484e3d8b6b09) )
*   元素:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([EFD 4149](https://github.com/angular/angular/commit/efd4149))
*   表单:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([DC 975 ba](https://github.com/angular/angular/commit/dc975bac93a8087d1f31a31db60ef313147e589f))
*   http:完成超时请求([# 39807](https://github.com/angular/angular/issues/39807))([61a 0b 6d](https://github.com/angular/angular/commit/61a0b6d))，关闭 [#26453](https://github.com/angular/angular/issues/26453)
*   http:XMLHttpRequest 中止事件发出错误([# 40767](https://github.com/angular/angular/issues/40767))([3897265](https://github.com/angular/angular/commit/3897265))，关闭 [#22324](https://github.com/angular/angular/issues/22324)
*   语言-服务:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([9b 6198 c](https://github.com/angular/angular/commit/9b6198c16f122dd934ac6a66d2ada21df26839b5))
*   语言服务:使用脚本版本进行增量编译([# 41475](https://github.com/angular/angular/issues/41475))([78236 BF](https://github.com/angular/angular/commit/78236bfdcaeb66c5846eb0435d727942bb88f7c5))
*   语言-服务:仅在模板中提供角度属性完成( [#41278](https://github.com/angular/angular/issues/41278) ) ( [0226a11](https://github.com/angular/angular/commit/0226a11c185da2d1e6f7833972d3f12205a6ae59) )
*   语言-服务:添加插件选项强制 strict templates([# 41062](https://github.com/angular/angular/issues/41062))([e9e7c 33](https://github.com/angular/angular/commit/e9e7c33f3c170648ec8c86d859980c7fe78fba39))
*   语言-服务:使用 Ivy 和视图引擎的单一入口点([# 40967](https://github.com/angular/angular/issues/40967))([e986a 97](https://github.com/angular/angular/commit/e986a9787b7787c3cffef69d06a2e7e1228e3f40))
*   localize:将错误放松为目标丢失警告([# 41944](https://github.com/angular/angular/issues/41944))([35 ceed 2](https://github.com/angular/angular/commit/35ceed2061a890a70576dc7afa0b779f3779ae7b))，关闭 [#21690](https://github.com/angular/angular/issues/21690)
*   本地化:更新支持的节点版本范围，只包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([658 ed1f](https://github.com/angular/angular/commit/658ed1f904ef0013c3b08e2b2182cf246ef55b2b))
*   localize:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([4b 469 c 9](https://github.com/angular/angular/commit/4b469c9))
*   ngcc:检测已经使用 TS 4.2([# 41305](https://github.com/angular/angular/issues/41305))([8d 3d a56](https://github.com/angular/angular/commit/8d3da56eda12070df1fb473c8609f3a94d77bfd6))降级的合成构造函数，关闭 [#41298](https://github.com/angular/angular/issues/41298)
*   平台浏览器:如果使用影子 DOM 封装( [#42005](https://github.com/angular/angular/issues/42005) ) ( [d555555](https://github.com/angular/angular/commit/d5555558d00774520dbda40d48721bda2cb9dd1a) )，关闭 [#36655](https://github.com/angular/angular/issues/36655) ，防止样式节点内存泄漏
*   平台浏览器:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([ea 05 CFD](https://github.com/angular/angular/commit/ea05cfd0c5a99840f4522b604c33a5b2f7f25f7d))
*   平台浏览器:配置`XhrFactory`使用`BrowserXhr`([# 41313](https://github.com/angular/angular/issues/41313))([e 0028 e 5](https://github.com/angular/angular/commit/e0028e57410281e190caa74e0986320f6591d27b))，关闭 [#41311](https://github.com/angular/angular/issues/41311)
*   平台浏览器:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([7 ecfd 2d](https://github.com/angular/angular/commit/7ecfd2d))
*   平台-浏览器-动态:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([BC 45029](https://github.com/angular/angular/commit/bc45029a5437bcea45fa00549241685a1a3f32d0))
*   平台-服务器:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([4b 9 D4 fa](https://github.com/angular/angular/commit/4b9d4fa3e729a3af13fb5b50de3e5c73c1d6923f))
*   路由器:更新支持的节点版本范围以仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([0067 edd](https://github.com/angular/angular/commit/0067edd1469a428c11bbe6358fd5650e79abf774))
*   路由器:仅当重用策略指示它应该重新连接( [#30263](https://github.com/angular/angular/issues/30263) ) ( [a4ff071](https://github.com/angular/angular/commit/a4ff071e3f08e3de6d4d3f97c747c2f42b827c49) )，关闭 [#23162](https://github.com/angular/angular/issues/23162) 时，才检索存储的路由
*   路由器:递归合并空路径匹配( [#41584](https://github.com/angular/angular/issues/41584) ) ( [1179dc8](https://github.com/angular/angular/commit/1179dc8cb32c9fc451d2af9215c4740af9d2e291) )，关闭 [#41481](https://github.com/angular/angular/issues/41481)
*   路由器:片段可以为空([# 37336](https://github.com/angular/angular/issues/37336))([b 555160](https://github.com/angular/angular/commit/b5551609fe02787641bdfdb0a6edfded413a3b52))，关闭 [#23894](https://github.com/angular/angular/issues/23894) [#34197](https://github.com/angular/angular/issues/34197)
*   路由器:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([350 dada](https://github.com/angular/angular/commit/350dada))
*   服务人员:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([6b 823d 7](https://github.com/angular/angular/commit/6b823d7071d59234ab52bdf7eaa248df6b7d9faa))
*   service-worker:更新 JSON.parse 用法的类型转换([# 40710](https://github.com/angular/angular/issues/40710))([4 F7 ff 96](https://github.com/angular/angular/commit/4f7ff96))
*   升级:在使用 ngMocks 时保留$ interval . flush([# 30229](https://github.com/angular/angular/issues/30229))([87dc 851](https://github.com/angular/angular/commit/87dc8511ccb9c75d78866ebd2c250ea96fc91bd0))
*   升级:更新支持的节点版本范围，仅包括 LTS 版本([# 41822](https://github.com/angular/angular/issues/41822))([10c 4523](https://github.com/angular/angular/commit/10c45239a68e82ea52c1601fae09953aa7843351))

对了，你有没有注意到`AsyncPipe`已经被本·莱什[打了](https://github.com/angular/angular/commit/9759bca339b44ed78ec6aafab0336d531d285f90)的补丁，可以同时兼容 RxJS 6 和 7？多酷啊。；-)

# 重大变化

和往常一样，这个版本有许多突破性的变化。

由于[官方发布说明](https://github.com/angular/angular/blob/master/CHANGELOG.md#breaking-changes)非常清楚，我只是将它们复制/粘贴到这里:

*   小型 UMD 软件包不再包含在分布式 NPM 软件包中。
*   *动画*:移除根视图时，DOM 元素现在被正确移除。如果您使用 SSR 并使用应用程序的 HTML 进行渲染，您需要确保在销毁应用程序之前将 HTML 保存到变量中。还有一种可能是，测试可能会意外地依赖旧的行为，试图找到一个在之前的测试中没有被删除的元素。如果是这种情况，应该更新失败的测试，以确保它们有正确的设置代码来初始化它们所依赖的元素
*   *公共*:用于返回`void`的`PlatformLocation`类的方法，即`onPopState`和`onHashChange`。现在，这些方法返回可以被调用来移除事件处理程序的函数
*   common:`HttpParams`类的方法现在接受`string | number | boolean`而不是`string`作为参数值。如果您在应用程序中扩展了这个类，您必须更新方法的签名来反映这些变化
*   *编译器-cli* :链接库不再生成传统的 i18n 消息 id。任何为这些消息提供翻译的下游应用程序都需要使用`localize-migrate`命令行工具来迁移它们的消息 id
*   *核心* : Angular 不再保持对 node v10 的支持，所以如果你还在为你的开发环境使用它，那真的是时候升级了！
*   *核心*:以前，如果给定的 DOM 节点没有关联的角度上下文(例如，如果在角度应用程序之外为 DOM 元素调用函数)，那么`ng.getDirectives`函数会抛出错误。这种行为与`ng`名称空间下的其他调试实用程序不一致，后者处理这种情况时没有引发异常。现在，为这样的 DOM 节点调用`ng.getDirectives`函数将导致从该函数核心返回一个空数组:切换默认的`emitDistinctChangesOnlyDefaultValue`，这将改变默认行为，并可能导致一些依赖不正确行为的应用程序失败

`emitDistinctChangesOnly`标志也已被弃用，并将在未来的主要版本中删除

之前的实现会在重新计算`QueryList`时触发变更`QueryList.changes.subscribe`。这导致了人为的大量变更通知，因为重新计算`QueryList`可能会导致相同的列表。`QueryList`何时被重新计算是一个实现细节，它不应该决定 change 事件触发的频率。

不幸的是，彻底修复这种行为会导致太多现有的应用程序失败。出于这个原因，Angular 认为这个修复是一个破坏性的修复，并在`@ContentChildren`和`@ViewChildren`中引入了一个控制行为的标志。

```
export class QueryCompWithStrictChangeEmitParent {
  @ContentChildren('foo', {
    // This option is the new default with this change.
    emitDistinctChangesOnly: true,
  })
  foos!: QueryList<any>;
} 
```

为了在 v12 `emitDistinctChangesOnlyDefaultValue`设置为`false`之前向后兼容。这一更改将默认值更改为`true`。

*   **核心**:改变了`APP_INITIALIZER`令牌的类型，以更准确地反映 Angular 处理的返回值的类型。以前，每个初始化器回调都被类型化为返回`any`，现在是`Promise<unknown> | Observable<unknown> | void`。万一您的应用程序使用`Injector.get`或`TestBed.inject` API 来注入`APP_INITIALIZER`令牌，您可能需要更新代码来考虑更严格的类型。

此外，如果在表达式中使用了`APP_INITIALIZER`标记，而该表达式的推断类型必须发送到. d.ts 文件中，则 TypeScript 可能会报告 TS2742 错误。为了解决这个问题，需要一个显式的类型注释，通常是`Provider`或`Provider[]`。

*   **核心:**最低支持的`zone.js`版本是`0.11.4`。因此，这意味着如果您使用的是旧版本，也是时候升级项目中的 zone.js 了！
*   **表单:**`emitEvent`选项被添加到以下`FormArray`和`FormGroup`方法中:
*   `FormGroup.addControl`
*   `FormGroup.removeControl`
*   `FormGroup.setControl`
*   `FormArray.push`
*   `FormArray.insert`
*   `FormArray.removeAt`
*   `FormArray.setControl`
*   `FormArray.clear`

如果您的应用程序有扩展`FormArray`或`FormGroup`类的自定义类，并覆盖上述方法，您可能需要更新您的实现以考虑新选项，并确保覆盖从类型角度来看是兼容的。

*   **表单:**先前在`<input type="number">`上定义的`min`和`max`属性被表单模块忽略。现在，这些属性的存在将触发最小/最大验证逻辑(在给定输入上还存在`formControl`、`formControlName`或`ngModel`指令的情况下)，相应的表单控制状态将反映这一点。
*   **平台浏览器:** `XhrFactory`从`@angular/common/http`移动到`@angular/common`。

**在**之前

```
import { XhrFactory } from '@angular/common/http';
```

**在**之后

```
import { XhrFactory } from '@angular/common';
```

*   **路由器:**严格的空检查将报告可能为空的片段。迁移路径:添加空检查。
*   **路由器:**`RouterLinkActive.routerLinkActiveOptions`输入的类型被扩展以允许更多的微调控制。以前读取此属性的代码可能需要更新，以考虑新的类型。

# 更新的路线图

根据目前棱角分明的[路线图](https://angular.io/guide/roadmap)，团队目前正忙于以下改进:

*   在调试和分析时改善开发人员的体验。这应该有助于我们理解组件结构(我想象 React Dev 工具允许 React)，以及变更检测
*   改进测试时间和自动拆卸调试:这应该改进测试和测试时间之间的隔离。[测试床](https://angular.io/api/core/testing/TestBed)也将被改变，以便在每次测试执行后自动清理和拆除测试环境
*   使用 ES2017+作为默认输出:他们将识别障碍并移除它们，以便默认输出语言可以升级
*   将 MDC 网整合到角形材料中
*   提高角形材料部件的可接近性
*   发布关于高级概念的指南，如变更检测、性能分析、与 Zone.js 的交互等
*   更新 e2e 测试策略(参见上文)
*   正在准备升级到 RxJS v7+。你可能知道，RxJS 7 最近已经[发布](https://medium.com/volosoft/whats-new-in-rxjs-7-a11cc564c6c0)。希望我们很快就能升级

在未来，Angular 团队计划:

*   研究一下微前端架构:他们可能会介绍一些方法，让我们使用 Angular
*   通过对有角度的表单进行严格的输入来改善开发人员的体验(我们非常需要这一点)
*   使 Zone.js 成为可选的，这将简化框架，改进调试，减少包的大小，甚至允许利用原生的 async/await 语法
*   通过将 Angular 编译器(`ngc`)集成为 TypeScript 编译器插件来提高构建性能
*   允许向宿主元素添加指令。这也是社区长期以来的要求！
*   使 NgModules 成为可选的，以缓解学习曲线
*   为我们提供了在组件级实现代码拆分的更简单的方法

# 角形材料和角形 CDK

## Sass 迁移

在内部，角状材料和 CDK 都已经移植到[新的 Sass 模块系统](https://sass-lang.com/blog/the-module-system-is-launched)。

如果你的应用程序使用其中的任何一个，那么你需要确保你已经用 https://www.npmjs.com/package/sass 的`sass`:替换了`node-sass`。`node-sass`包不再维护！

通过这次迁移，Sass 主题化 API 得到了增强，现在它允许我们利用 Sass 的`@use`实用程序。

现在`@angular/material`和`@angular/cdk`只有一个入口。

最后，为了清晰起见，API 也进行了更改。许多函数、混合和变量都被重新命名。

你可以在新的主题指南中找到更多关于这些变化的信息:[https://github . com/angular/components/blob/master/guides/theming . MD](https://github.com/angular/components/blob/master/guides/theming.md)。此外，请注意[https://material . angular . io](https://material.angular.io)上的指南已经重写，以展示新的 API，并包括解释。

升级过程会自动将代码迁移到新的 Sass API。您可以在此处找到前/后示例。

## 角度 CDK 变化

版本 12 包括对角度 CDK 的许多[变化](https://github.com/angular/components/blob/master/CHANGELOG.md#cdk)。

在这里，我将只列出新特性，但是如果您想了解关于错误修复和性能改进的详细信息，可以查看发行说明:

*   *拖放*:dropped 事件现在包含了一个`dropPoint`属性，它决定了项目被放下时鼠标指向的确切位置。更多信息[点击此处](https://github.com/angular/components/pull/22410)
*   *下拉*:预览容器[现在可以定制](https://github.com/angular/components/issues/13288)
*   *表*:一个新的指令允许[启用循环视图中继器](https://github.com/angular/components/pull/21508)，它缓存被处理的行，并在数据集改变时重用它们。这有助于提高性能(减少延迟)
*   *表* : [在`StickyUpdate`界面增加了](https://github.com/angular/components/pull/21886)粘性元素的偏移量
*   *步进器*:当用户试图离开一个步进时，现在会发出[事件](https://github.com/angular/components/issues/19918)
*   *步进器*:现在可以[改变方向](https://github.com/angular/components/issues/21874)
*   *可访问性*:一个`FocusOptions`对象[现在可以被传递](https://github.com/angular/components/issues/21767)到各种焦点陷阱方法中
*   *测试*:新的 WebDriver 线束环境。我还没有深入研究过这个，所以我不能告诉你更多。检查[PR](https://github.com/angular/components/pull/22410)

## 角度材料变化

角形材料也有许多[变化。同样，请查看发行说明，获取错误修复的完整列表。](https://github.com/angular/components/blob/master/CHANGELOG.md#material)

新功能:

*   *日期选择器*:不再依赖[对话框](https://github.com/angular/components/pull/22383)
*   *步进器*:方向现在可以动态改变(类似 CDK 的变化)
*   *步进器*:允许内容[延迟呈现](https://github.com/angular/components/issues/12339)
*   *菜单*:允许编程更新菜单位置
*   *Mat 错误*:现在使用`aria-live="polite"`代替`role="alert"`。更多详情[此处](https://github.com/angular/components/issues/21781)
*   *选项卡*:向[添加方法，以编程方式将焦点设置在特定选项卡](https://github.com/angular/components/pull/15228)上
*   *列表*:现在从`selectAll`和`deselectAll`方法返回一个改变了选项的数组。查看[公关](https://github.com/angular/components/pull/21358/files)了解详情
*   *滑动切换*:允许[通过提供者全局配置默认颜色](https://github.com/angular/components/pull/22047)
*   *工具提示*:现在通过组件上的一个类显示工具提示的有效位置
*   *单选*、*复选框*和*滑块*:在[打印样式表](https://github.com/angular/components/issues/22298)中包含这些组件的背景颜色

实验版上也有多处改动:[https://github . com/angular/components/blob/master/changelog . MD # material-experimental](https://github.com/angular/components/blob/master/CHANGELOG.md#material-experimental)。

# 角度通用

Angular Universal 12 也是刚出炉的。

在这个版本中，默认情况下，Universal now [内嵌关键 CSS](https://github.com/angular/universal/commit/3dddb758fa6e89ca1b857b7a7a17a21bc474618c)，这非常酷。

Universal 现在包括一个新的`proxyConfig`选项，为`ssr-dev-server`构建器提供定制的代理配置。

在这个版本中，有一个新的(实验性的)SSR 引擎叫做 *Clover* (让我想起了 Java 生态系统中的一个质量工具)。这台新引擎似乎很有前途。它旨在简化事情，让我们摆脱`Window is undefined`错误，消除对 SSR/prerender 的多次构建的需要，无需额外构建即可生成应用程序外壳，等等。稍后我们可能会听到更多关于它的消息。如果你好奇，那就去看看[的公关](https://github.com/angular/universal/commit/c4b7be3bbdbc7334f5cf7049c644e185cf15d0bb)。

这个版本包括一个[构建器](https://github.com/angular/universal/commit/2066f18a23eecce6dd485c19bc1ed10a4c3be497)，可以使用新的通用 Clover 方法生成静态页面(即预渲染)。

最后，这个版本还包括对开发服务器的 TLS 支持。

# 谷歌地图

如你所知，Angular 包括谷歌地图和 Youtube 的组件。版本 12 对谷歌地图组件进行了一些改进:

*   现在包括一个`icon`输入，可轻松定制标记
*   现在当点击一个集群[时会发出一个`clusterClick`事件](https://github.com/angular/components/issues/22020)
*   包括围绕 Google Maps Geocoder API 的包装器，并导出以前没有公开的`MapDirectionsResponse`
*   介绍对[渲染热图](https://github.com/angular/components/pull/21489)的支持
*   增加了`MapDirectionsRenderer`，允许在地图上绘制方向；增加了`MapDirectionsService`，包裹`google.maps.DirectionsService`计算两点之间的[路线。](https://github.com/angular/components/pull/21736)
*   新的`options`输入在[标记集群器](https://github.com/angular/components/pull/21861)上，类似于其他指令

# 升级

和往常一样，我们提供了完整的升级指南，`ng update`将为您提供帮助:[https://update.angular.io/?l=3&v = 11.0-12.0](https://update.angular.io/?l=3&v=11.0-12.0)

如果你正在使用 [Nrwl NX](https://nx.dev/) (你真的应该这么做)，请注意 Nx 12.3 已经支持 Angular 12 了！在此进一步了解[。作为一项额外的好处，Nx 还将帮助您从 TSLint 迁移到 ESLint(它的时间！)](https://blog.nrwl.io/incremental-build-improvements-angular-12-distributed-task-execution-and-more-in-nx-12-3-48b5e4722056)

# 结论

在本文中，我探讨了 Angular 12 的新特性。

像往常一样，这是**放出的*英雄气概——***还能是什么？

常春藤正在茁壮成长，随着生态系统的迁移，我们“很快”就不会那么担心了。这个版本有很多很棒的变化，所以现在就来看看并升级吧！

今天到此为止！

**PS:** 如果你想了解大量关于产品/软件/Web 开发的其他很酷的东西，那么[去看看 Dev Concepts 系列](https://dev-concepts.dev)、[订阅我的通讯](https://mailchi.mp/fb661753d54a/developassion-newsletter)，以及[来 Twitter 上打个招呼吧！](https://twitter.com/dSebastien)

*原载于 2021 年 5 月 13 日 https://dsebastien.net*[](https://dsebastien.net/blog/2021-05-13-angular-12-in-depth)**。**

**更多内容请看*[*plain English . io*](http://plainenglish.io/)*