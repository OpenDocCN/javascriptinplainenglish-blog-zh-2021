# Angular 应用程序如何启动

> 原文：<https://javascript.plainenglish.io/how-angular-applications-boot-dubois-s%C3%A9bastien-d3eacbdc41b4?source=collection_archive---------9----------------------->

## 你有没有想过角度应用是如何开始的？

![](img/37f9e3f8b944d331fb0f7bcf7ed15af6.png)

在本文中，我将概述如何引导 Angular 应用程序。请注意，这是一篇针对初学者的文章，而不是深入探讨。

# 高级流程

要启动 Angular 应用程序，必须在 Web 浏览器中完成多项工作:

*   必须加载入口点的 HTML
*   必须加载应用程序的不同 JavaScript 包
*   必须执行应用程序的主包
*   主包必须加载 Angular 并触发根 Angular 应用模块的引导
*   Angular 必须引导根 Angular 应用程序模块，并呈现应用程序

让我们更详细地看一下这些步骤。

# HTML 入口点

首先，Web 浏览器下载并评估`index.html`文件:

至少，HTML 文件的主体必须包含*根组件*(即它的*入口点*组件)；在这种情况下`<app-root></app-root>`。一旦 Angular 应用程序被加载和执行，Angular 就会识别它，并使用插值/渲染模板更新 DOM。

那其实就是故事的“结局”。让我们倒回去一点。

# JS 捆绑包加载

如果你在一个全新的 Angular 应用程序的源代码中打开`index.html`文件，你不会找到上面看到的任何脚本。为什么？因为它们是由*构建过程*添加的。当您使用 [Angular CLI](https://cli.angular.io) 时，它首先读取`angular.json`文件(或`angular-cli.json`)来了解项目的配置。然后，在此基础上，它构建整个应用程序。

在幕后，Angular CLI 使用模块捆绑器 [Webpack](https://webpack.js.org) 。除此之外，Webpack(在许多插件的帮助下)将项目代码和资产转换成 JavaScript 包。这些包包含应用程序的所有代码，以及第三方的代码(例如 Angular 和您可能使用的其他库)。

当使用`ng build --prod`构建 Angular 应用程序时，在`dist/<application_name>`下会生成一些文件:

```
├── 3rdpartylicenses.txt
├── favicon.ico
├── index.html
├── main.1feaffbe857aaf7ee0db.js
├── polyfills.a4021de53358bb0fec14.js
├── runtime.e227d1a0e31cbccbf8ec.js
└── styles.09e2c710755c8867a460.css
```

我们已经讨论过了`index.html`文件。让我们来看看 JavaScript 文件:

*   `main.js`:您的应用程序代码和您导入的所有内容
*   `vendor.js`:您的应用程序所依赖的第三方代码
*   `polyfills.js`:允许在旧环境中使用新功能的聚合插件(例如，在过时的网络浏览器上使用 Angular)
*   `runtime.js`:Webpack 在运行时用来加载代码的实用程序代码

这些 JavaScript 包由 Webpack 生成，并作为`<script>`标签添加到`index.html`文件中，正如我们之前看到的。

请注意，如果您使用诸如[延迟加载角模块](https://angular.io/guide/lazy-loading-ngmodules)之类的特性，您可能会有额外的捆绑包。

由于这些脚本标签是`index.html`文件的一部分，网络浏览器也会加载这些。但是装载这些并不足以让事情发生。必须执行代码才能启动应用程序。让我们看看下一个。

# 主入口点执行

`main`捆绑包是这里值得关注的一个。正如我在上一节中提到的，它包含了我们的 Angular 应用程序的代码。

这个捆绑包实际上包含了我们的整个应用程序代码。但是它的哪一部分应该被执行呢？这是在`angular.json`文件中配置的:

上面代码片段中的`main`属性(第 19 行)决定了运行时一旦加载了主 JavaScript 捆绑包，就应该加载并执行该模块。

如上图所示，默认为`main.ts`模块。由于这种配置，Angular CLI 将确保相应的模块由 Webpack 加载，并在包加载后尽快执行。

现在，您知道`main.ts`文件是 Angle 应用程序的入口点，以及*为什么加载*并执行&了。现在让我们看看它是干什么的！

# 角度应用引导

如果您没有更改任何内容，那么`main.ts`文件应该如下所示:

这里有很多需要注意的事情。

首先，有一些重要的声明。一旦编译器将代码转换成 JavaScript 代码，这些就会保留。在运行时，这些导入将由 Webpack 处理。一旦导入被*执行*，其余的代码将被执行。

第二，如果项目已经建成投产，那么将启用[生产模式的](https://angular.io/api/core/enableProdMode)。这对性能非常重要。

最后，也是最重要的，将执行以下行:

```
platformBrowserDynamic().bootstrapModule(AppModule);
```

这是一个单独的行，但是它做了很多。`platformBrowserDynamic`是一个能够在网络浏览器环境中加载 Angular 的模块。它加载框架的必要元素并配置需要的内容。鉴于 Angular 可以在其他环境中运行(例如移动、服务器端等)，请注意还有其他方式来加载 Angular。

所以，第一部分，`platformBrowserDynamic()`负载角。一旦完成，第二部分`bootstrapModule(...)`指示 Angular 引导给定的模块。默认情况下，所有角度应用至少包括*和*和`AppModule`。

此时，Angular 接管、加载组件、服务、指令、管道以及您的`AppModule`可能导入、引用、声明的任何其他东西。最后，它将寻找与`app-root` *选择器*匹配的组件。通常，该组件是`AppComponent`:

一旦 Angular 找到了组件，它将为您呈现它，并更新包含呈现内容页面的 DOM。

如果你很好奇，想知道更多，那么看看下面的文章:

*   [https://angular . io/guide/bootstrapping # launching-your-app-with-a-root-module](https://angular.io/guide/bootstrapping#launching-your-app-with-a-root-module)
*   [https://stack overflow . com/questions/48942691/how-angular-build-and-runs](https://stackoverflow.com/questions/48942691/how-angular-builds-and-runs)
*   https://medium . com/angular-in-depth/angular-platforms-in-depth-part-2-application-bootstrap-process-8be 461 b 4667 e

# 结论

在本文中，我简要解释了如何引导 Angular 应用程序。这不是整个故事(我已经把所有血淋淋的细节都省略了)，但是它应该可以帮助你更清楚地理解这个过程的重要步骤。

今天到此为止！

PS:如果你想了解大量关于产品/软件/Web 开发的其他很酷的事情，那么[看看开发概念系列](https://dev-concepts.dev)，[订阅我的时事通讯](https://mailchi.mp/fb661753d54a/developassion-newsletter)，还有[来 Twitter 上打个招呼吧！](https://twitter.com/dSebastien)

*原载于 2021 年 3 月 28 日*[*https://dsebastien.net*](https://dsebastien.net/blog/2021-03-28-angular-application-bootstrap)*。*