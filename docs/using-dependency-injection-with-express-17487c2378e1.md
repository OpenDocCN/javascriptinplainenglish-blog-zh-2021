# 通过 Express 使用依赖注入

> 原文：<https://javascript.plainenglish.io/using-dependency-injection-with-express-17487c2378e1?source=collection_archive---------4----------------------->

![](img/61832566bc39254e2bf0dc0dfa92e887.png)

Photo Illustration by David Fekke

*原发布于*[*https://fek . io*](https://fek.io/blog/use-dependency-injection-with-express)*。*

我最近写了一篇关于在 JavaScript 中使用[依赖注入](/should-you-use-dependency-injection-in-javascript-3751bdf3f198)的博文。这种技术非常方便，并且在使用像 [Express](https://expressjs.com) 这样的 web 应用程序框架时非常有用。

Express 使得通过中间件向您的 web 应用程序或单个路由注入依赖关系变得非常容易。在我的 Express 应用程序中，当我需要一个依赖项时，我通过将它作为请求对象上的一个服务直接注入到一个路由中。但在此之前，让我们将我们的应用程序分解成不同的模块化组件。

# 服务

对于这个应用程序的第一部分，我们将使用 [axios](https://github.com/axios/axios) 库创建实际的 HTTP 请求。我们将使这些请求异步。

我用[星球大战 API](https://swapi.dev/) 作为我的例子。我为`getVehicles`、`getPlanets`和`getStarships`创建了三个函数。这些方法使用了`async/await`语法，这将允许导入这些函数的模块异步使用它们。

# 路线

对于我的快速路线，我喜欢将处理程序分解到它们自己的模块中。然后，我们可以在实际的路由中使用这些处理程序，这将使它们更容易测试。

从上面的例子可以看出，每个处理程序都可以通过`req`参数发出服务请求，我们并没有将服务显式地导入到我们的处理程序中。现在，我们可以为我们的 API 调用在它自己的模块中创建路由。

上例显示了本模块中的样板快速路线设置。我们现在可以在我们的主 express 应用程序模块中引用它。

# **注入服务**

为了注入我们的服务，我们需要创建一个可以附加到`req`对象的服务对象，并创建一个中间件组件，将服务注入到我们的 API 路径中。

从上面的例子中我们可以看到，我们现在正在导入使用`axios`创建的单个 API 函数，并创建一个服务工厂，将所有三个函数合并成一个服务对象。然后，我们创建`exposeService`中间件，它将把这个服务注入到我们的路由中。

我们完成的应用程序应该看起来像下面的例子；

在示例应用程序中，我们已经将服务注入到我们的`api`路线中，因此它可以访问`req`参数的`service`属性上的星球大战 API。我们还有一个默认的指向'/'路由的索引路由。这个“索引”路由不能访问服务，因为我们没有全局传递中间件，我们只是将它传递到“api”路由中。

# **结论**

依赖注入是一个非常强大的工具，它允许我们分离我们的应用程序。通过将这些服务分解到它们自己的模块中，我们也使得我们的应用程序更容易使用 JavaScript 可用的众多测试框架之一进行测试。愿国庆日与你同在！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)