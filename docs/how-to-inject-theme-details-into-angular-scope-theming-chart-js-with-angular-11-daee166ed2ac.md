# 如何将主题细节注入角度范围

> 原文：<https://javascript.plainenglish.io/how-to-inject-theme-details-into-angular-scope-theming-chart-js-with-angular-11-daee166ed2ac?source=collection_archive---------15----------------------->

## 使用角度 11 对 Chart.js 进行主题化

![](img/8f96504dc438225f4de00f405241d2c0.png)

**Nature, The Best Theme Creator** ❤ — Photo by [zero take](https://unsplash.com/@zerotake?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Angular 本身是一个非常强大和饱和的框架。它是成熟的，能够实现从概念到精心制作的实际应用程序的任何用户需求。在这种情况下，让第三方库兼容并直接使用是很容易的，因为它适用于许多其他基于 JavaScript 的框架。

在日常的实现中，有时我们会遇到这样的用例，社区中的某个人已经开发了一个解决方案，同时许多贡献者对其进行了大量的改进。所以没有必要重新发明轮子。

作为例子，

1.  对于可视化仪表板实现，设计良好的图表/图形解决方案已经存在于开放云中，即使考虑到数据量，这些解决方案也实现得很好。(有些甚至延迟加载数据，这意味着能够在缩放或平移图表时按需获取数据)
2.  位置/地图解决方案
3.  画布解决方案
4.  增强的功能部件——日期选择器、日期范围选择器等等

即使预期的业务需求或最终的功能/目标可以很容易地用这些专门制作的库部件来管理，但是在制作与主题兼容的部件时，我们仍然面临一个困难。这是因为有些库不支持通过样式类来控制主题，相反，它们期望的是注入颜色和印刷值作为输入参数。

以上的主要技术原因，在这样的一些库中

1.  他们执行一些画布渲染，其中画布上的颜色和排版在渲染时是需要的，并且不能通过主题化来控制。
2.  外部主题化方面还没有被考虑，但是主题变量注入已经被简化了。

我们可以利用$theme 实体和 mixins，但是 canvas 涉及到 Chart.js 这样的用例，没有本地支持来克服这一点。

作为一个解决方案，我过去所做的是在将 [**角度素材**](https://material.angular.io/) 主题变量扩展到角度附近的情况下进行讨论。

基于 ViewChild 的主题细节注入机制是我的首选解决方案，我想推广它，甚至在完全独立的应用程序中利用它，因为我在实现基于图表和图形的应用程序时经常遇到实际的用例。在寻找解决方案时，我发现了这个美妙的[功能请求](https://github.com/angular/components/issues/11315)由 [pjmagee](https://github.com/pjmagee) 提交，但是直到今天我写这篇文章时，它仍然是开放的和未分配的。这意味着该问题对于原生支持仍然是开放的。

于是我决定把它编译成一个小 [npm 包](https://www.npmjs.com/package/theme-emitter)发布。如果您对已发布的 npm 库满意，那么您可以跳过步骤 1 来创建库。

让我们过一遍。

![](img/bd0f31b8fdb6b7e5e0654e947c2d637f.png)

Photo by [Maik Jonietz](https://unsplash.com/@der_maik_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 1.主题-发射器库项目

让我们从库模块创建步骤开始。您可以在您的项目用例中实现这一部分，或者直接导入并利用发布的 npm 包。

> ng 新主题-发射器-演示--创建-应用=假
> 
> cd 主题-发射器-演示
> 
> ng 生成库主题-发射器

1.1 在库组件 HTML 中，我们可以如下定义主题属性映射视图子 id。让我们如下定义检索占位符的主要、强调和警告主题参数。

1.2 然后如下定义样式 mixin，因为它可以检索主题，该主题应该从基本主题设置器样式文件传递到这里。现在，我们已经将主题属性检索到了自定义组件中。

1.3 然后，可以定义一个小型模型类，用于承载和类型保护主题细节，如下所示

1.4 接下来，我们可以读出 component.ts 文件中的主题属性。

*   为此，我们可以使用本机方法“ *getComputedStyle* ”，该方法使用目标元素(因为它是文档中所有对象继承的最通用的基类)
*   然后，它将返回一个“ *CSSStyleDeclaration* ”对象，这是一个 CSS 声明块，它公开了样式信息和各种与样式相关的方法和属性。
*   然后可以在服务设置器中分配已解析的主题属性。

1.5 然后应该定义主题发射器服务，它将负责向所有服务消费者发射那些旋转的主题值。

1.6 然后应该定义模块，组件应该像往常一样在 ngModule 下声明和导出。

1.7 主题发射器组件 scss 应该在最终的库发行版中公开，否则我们将无法在应用程序主题化中导入它。

现在一切都好于图书馆项目的创建。接下来我们要做的是，在实际使用案例中利用它。

# 2.主题-发射器利用

2.1 在 base.scss 文件中定义材质主题详细信息，如下所示。我将在后面的另一篇文章中详细讨论主题化的最佳实践。您也可以在共享的 git 位置找到更多关于颜色和配置的详细信息。

然后，已定义的主题应该在组件主题混合下注入到主题发射器中。

2.2 同时，我们需要在应用程序的根级别初始化主题发射器自定义组件。

2.3 现在一切就绪。如果任何人在应用程序中的任何地方订阅了主题发射器服务，就可以获取主题属性，并准备好在 Angular 组件附近使用。

如 *initTheme* 函数所示，颜色细节来自主题发射器服务订阅。

2.4 现在那些素材主题链接的样式参数可以传递给第三方组件了。在我的演示中，它是一个 Chart.js 组件。但可以是引言中提到的任何东西。

Git repo 用于 Angular lib 模块的创建和使用

[](https://github.com/sajithahd/angular-theme-emitter-lib) [## github-sajithahd/angular-theme-emitter-lib:用 StackBlitz ⚡️创建

### 由斯塔克布里兹·⚡️.创作为 sajithahd/angular-theme-emitter-lib 开发创建一个帐户…

github.com](https://github.com/sajithahd/angular-theme-emitter-lib) 

Stackblitz 工作演示—角度库模块的创建和使用

# 3.来自 npm 的主题发射器

我在 npm 中发布这个库模块，然后它可以直接导入到 package.json 中。

[](https://www.npmjs.com/package/theme-emitter) [## 主题发射器

### 这个库是用 Angular CLI 版本 11.0.9 生成的。运行 ng 生成组件组件名称项目…

www.npmjs.com](https://www.npmjs.com/package/theme-emitter) 

针对上述 npm 包利用率的 Git repo

[](https://github.com/sajithahd/angular-theme-emitter) [## github-sajithahd/angular-theme-emitter:用 StackBlitz ⚡️创建

### 此项目是使用 Angular CLI 版本 11.0.6 生成的。为开发服务器运行 ng serve。导航到…

github.com](https://github.com/sajithahd/angular-theme-emitter) 

Stackblitz 工作演示— npm 模块利用率

可能有比这更好的方法来处理同样的问题。可能本地支持也会存在。如果是这样我邀请大家，请在这里分享你们的经历。

[](/promises-vs-observables-what-is-ahead-of-the-pack-7567d5f6582a) [## 承诺与观察——领先的是什么？

### 在本文中，我将讨论两个主要的异步支持框架工具及其区别——承诺…

javascript.plainenglish.io](/promises-vs-observables-what-is-ahead-of-the-pack-7567d5f6582a) 

*更多内容看*[***plain English . io***](http://plainenglish.io)