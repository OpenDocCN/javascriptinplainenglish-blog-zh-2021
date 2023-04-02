# 惰性加载角度应用

> 原文：<https://javascript.plainenglish.io/lazy-loading-angular-applications-62ee1518b219?source=collection_archive---------10----------------------->

![](img/ed5f8400d0967166319650fc17acaab6.png)

Picture courtesy of [Kevin Grieve](https://unsplash.com/@grievek1610begur)

在*非常罕见的*情况下，您可能想要延迟加载您的 Angular 应用程序。在本文中，我将向您展示如何做到这一点。

***警告*** *:不要轻举妄动。仔细评估你是否真的需要这样做，因为这会对用户体验产生毁灭性的影响！*

# 角度模块导入副作用

在我的[上一篇文章](https://dsebastien.net/blog/2021-03-28-angular-application-bootstrap)中，我简要解释了 Angular 应用程序的引导过程。我在那里提到的一件事是，导入语句保留在运行时，由 Webpack 处理。

但是我没有提到的是，当 Webpack 导入一个 Angular 模块时会发生什么；例如，使用以下代码行:

```
import { AppModule } from './app/app.module';
```

当您看到这一行时，您可能会认为除了`AppModule`被加载并可用于当前模块的其余部分之外，没有发生什么。实际上这里有一个副作用！

只要 Webpack 加载一个 Angular 模块，附加到 Angular 模块的类的装饰器就会被执行。我通过一个例子来解释一下:

如您所见，这是角度 1–01 模块。这是一个简单的类，带有包含元数据的装饰器。但是你可能不知道的是，decorators 不仅仅是*元数据。*

装饰者实际上是附加在元素上的[函数](https://www.typescriptlang.org/docs/handbook/decorators.html)(例如，类、方法、访问器等)。它们接收修饰元素作为参数，并可以随意修改它们。TypeScript/JavaScript 装饰器实际上是[装饰器设计模式](https://en.wikipedia.org/wiki/Decorator_pattern)的实例。

但是这里有趣的问题是*装饰函数何时执行！当附加到一个类时，一旦类声明被执行，装饰器就被执行[。由于 Angular 模块类通常是在顶层声明的，所以 Webpack 一加载 es 模块，类声明就会被执行*！*](https://stackoverflow.com/questions/50182601/when-does-decorator-code-execute)*

因此，回到这一行:

```
import { AppModule } from './app/app.module';
```

这显然是*而不是*无副作用的代码！模块一加载，就执行模块的类声明，相关的装饰函数也是如此！记住这一点很重要；我一会儿会回到这个话题。

# 有问题的情况

在开始“如何做”之前，让我描述一下延迟加载 Angular 应用程序有意义的情况。

在我目前从事的项目中，我们使用了 [Auth0 Angular SDK](https://github.com/auth0/auth0-angular) 。该库负责认证过程。此外，它还提供了一个 Angular HTTP 拦截器，可用于将 OAuth 访问令牌附加到相关的传出 HTTP 请求(例如，后端 API 调用)。

为了让 HTTP 拦截器工作，必须加载 SDK 的`AuthModule`，并配置:

```
AuthModule.forRoot({
  domain: 'YOUR_AUTH0_DOMAIN',
  clientId: 'YOUR_AUTH0_CLIENT_ID',
  httpInterceptor: {
      allowedList: [ ... ],
      ...
  },
  ...
}),
```

到目前为止，一切顺利。你可能会问的问题在哪里？上面的`allowedList`是一个 URL/URL 模式列表，HTTP 拦截器将使用它来确定访问令牌是否应该附加到请求上。在我们的应用程序中，我们不想简单地硬编码这个列表，因为它在不同的环境中会有所不同。在配置 `AuthModule`之前，我们首先需要加载环境配置文件。环境配置文件是一个静态 JSON 文件，包含当前环境的配置。

幸运的是，Auth0 Angular SDK 提供了一种方法来[推迟模块](https://github.com/auth0/auth0-angular#dynamic-configuration)的配置，使用一个`APP_INITIALIZER`:

很好，问题解决了…还是没有？

不幸的是，我们的情况不是这样！为什么？因为我们的应用程序已经有了其他的应用程序初始化器，其中一些需要注入一个`HttpClient`实例。这就是开箱即用的解决方案让我们失望的地方。一旦需要在应用程序中的某个地方注入`HttpClient`，Auth0 HTTP 拦截器就会被实例化。如果在那个时间点 Auth0 模块还没有配置，那么拦截器就会崩溃，出现错误[解释配置丢失。多。](https://github.com/auth0/auth0-angular/issues/70)

经典的鸡和蛋的问题！

不幸的是，我们不能轻易地摆脱对其他初始化器中的`HttpClient`的依赖；我们唯一的解决方案是在 Angular 应用程序启动之前加载配置，并延迟对`AppModule`装饰器的评估，以确保我们的配置在运行时已经加载/可用。

这是为什么呢？正如我们所看到的，因为模块一导入，`AppModule`上的`@NgModule`装饰器就会被执行，默认情况下`main.ts`会导入它。

好了，现在让我们看看*如何*延迟角度应用的自举。

# 延迟加载和执行角度

延迟加载/执行角度应用的关键在默认入口点:`main.ts`。

这个想法是推迟`platformBrowserDynamic().bootstrapModule(...)`被召唤的时刻。但是正如我之前在这篇文章中暗示的，光有*还不够。如果我们想避免由`AppModule`导入引起的副作用，我们也需要去掉那个 import 语句。*

但是如果我们不导入`AppModule`，那么如何引导它呢？幸运的是，Angular 支持[延迟加载模块](https://angular.io/guide/lazy-loading-ngmodules):

```
const routes: Routes = [
  {
    path: 'items',
    loadChildren: () =>
      import('./items/items.module').then((m) => m.ItemsModule),
  },
];
```

使用[动态导入](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#dynamic_imports)完成角度模块的延迟加载。此类导入仅在需要时执行。

我们现在已经有了拼图的所有部分:

*   移除`AppModule`顶层导入
*   将呼叫延迟到`platformBrowserDynamic().bootstrapModule(...)`

现在让我们来看看解决方案:

让我解释一下这是如何工作的。首先，如前所述，我们不导入`AppModule`。其次，我们使用`runtimeConfigLoader$` observable 加载应用程序的运行时配置。一旦加载了配置(第 32+行)，我们将配置存储在`sessionStorage`中——这是一个任意的选择；也可能是`localStorage`或其他方式。

最后，我们使用以下公式切换到不同的可观察值:

```
return from(import('./app/app.module')).pipe(
  concatMap((mod) => {
    platformBrowserDynamic().bootstrapModule(mod.AppModule);
    return of(void 0);
  })
);
```

`import`语句返回一个`Promise`，它为我们提供了 es 模块。一旦 ES 模块可用(第 49+行)，我们最后使用`platformBrowserDynamic().bootstrapModule(...)`加载 Angular 并引导`AppModule`。

现在你有了它，一个角度应用程序的延迟加载。当然，上面的代码对应于一个特定的场景，但是同样的方法也可以用来按需加载 Angular 应用程序。

# 结论

在本文中，我解释了导入 Angular 模块会有副作用，我还解释了如何避免这些副作用，以及如何惰性地引导 Angular 应用程序。

请记住，应该避免这种情况，因为它会降低应用程序的启动速度，并且会对用户体验产生非常负面的影响。

今天到此为止！

PS:如果你想了解大量关于产品/软件/web 开发的其他很酷的事情，那么[看看开发概念系列](https://dev-concepts.dev)，[订阅我的时事通讯](https://mailchi.mp/fb661753d54a/developassion-newsletter)，还有[来 Twitter 上打个招呼吧！](https://twitter.com/dSebastien)

*原载于 2021 年 3 月 28 日 https://dsebastien.net**[*。*](https://dsebastien.net/blog/2021-03-28-loading-an-angular-app-lazily)*