# 用 Node.js、Express 和 TypeScript 构建一个 API

> 原文：<https://javascript.plainenglish.io/create-a-typescript-express-server-in-minutes-7d34c306f60?source=collection_archive---------4----------------------->

用 Express 和 TypeScript 构建下一个 Node.js API

如果你已经开发了一个网站数周或数年，你可能已经构建了一些应用程序，为你的网站后端提供标准的 CRUD(创建、读取、更新、删除)功能。这些后端服务的核心往往非常相似，所以为什么不创建一个可重用的样板/模板来帮助您立即启动并运行呢？

**剧透提示:**这篇文章会给你样板，或者给你一些如何写快递申请的想法，让他们做得更好！如果您是 Express 或 TypeScript 新手，这将是一个用大量代码示例深入框架和语言的好机会。

![](img/02bf6e9309c7b458737d54bb75e43224.png)

Source: [Pexels](https://www.pexels.com/photo/person-using-macbook-pro-574077/)

按照本文的思路，[从 GitHub](https://github.com/MR-DS-20/express-template) 克隆代码。如果您有任何更改或建议，请随时参与项目合作。

这里将解释样板文件:

*   环境
*   应用和服务器
*   路由器和控制器
*   模型

样板文件的文件结构:

# 创建环境文件

有几种方法可以引入应用程序的变量和设置。项目中的`dotenv` npm 包和`.env`文件是一个很好的方法。不过，这可能不是最干净的打字稿方式。您可以创建一个环境函数，这将允许您根据部署阶段或其他变量进行文件替换。

例如:

这个函数查看从执行节点的 shell 传递来的`ENVIRONMENT`变量，并加载适当的文件。在函数的声明中，可以看到`env: () => IEnv`。这是在声明该函数将返回一个类型为`IEnv`的对象，该对象是一个如下所示的接口:

```
export interface IEnv {
    port: number;
    db:{
        name: string;
        user: string;
        pw: string;
        account: string;
    };
    apiPath: string;
    staticPath: string;
}
```

使用 env 函数时，使用接口将为您提供 Typescript 的类型检查功能。本质上，当你使用这个对象的值时，你会得到自动完成的建议，如果你犯了一个错误，你的 IDE 会为你突出显示它。

您的`dev.ts`文件可能看起来像这样，以保存您在开发时使用的变量:

```
export const ENV:IEnv = {
    port:8082,
    apiPath: '/api/v1',
    staticPath: 'public',
    db:{
        name: 'COLLECTION_NAME',
        user:'UNAME',
        pw: 'P@%%W()RD',
        account: '@mongo-account',
    },
}
```

请记住将它添加到您的`.gitignore`文件中，这样它就不会被提交到存储库中，您的凭证也会保持安全。

# 创建应用程序实例

拥有一个处理 express 应用程序的所有配置的类有助于保持服务器文件的整洁和易读，还可以确保应用程序类可重用，因为它没有任何与特定项目相关的内容。

通读一下这个文件， [application.ts](https://github.com/MR-DS-20/express-template/blob/master/src/application.ts) 。构造函数部分如下所示:

该类处理所有 express 应用程序的构造配置，并将应用程序呈现为公共的，随时可供使用。

Express 服务器(索引)文件可能会很快失控，需要重构才能保持可维护性。这种方法从一开始就确保了可维护性。下面是`server.ts`文件的样子:

很干净，对吧？使用简单的 import 语句添加新路由器，并将它们放入阵列中。在单独的文件中处理中间件。由 app 类处理的 MongoDB 连接逻辑。

如果您正在查看那一行`dbConString ? app...: console...;`并且不确定发生了什么，它是一个三元运算符，其功能本质上类似于 if-else 语句。它的语法是`(ifTrue) ? (doThis) : (elseThis);`。

# 创建模型

通常，路由器、控制器和型号之间可能存在一对一的关系。然而，根据您的使用情况，您可以在一个路由器中使用多个控制器，或者在一个控制器中使用多个型号。

这种意义上的模型表示 MongoDB 中的一个集合。如果你正在寻找一个免费的托管数据库解决方案，请前往[cloud.mongodb.com](http://cloud.mongodb.com)。

请参见下文，了解如何定义模式(声明字段及其类型)和模型(提供与数据库交互的方法)。

`BaseModel`是一个助手类，它接受模型并提供通用函数，如`create()`或`delete()`，一旦您的应用程序中有几个模型，这些函数将大大减少重复代码的数量。

例如，您必须为每个模型编写`model.findById(id).exec()`,并且您将为所有不同的读/写操作这样做。相反，扩展`BaseModel`，你就不必为你的任何模型编写它们。继续学习控制器，看看如何实现这一点。[点击此处查看基础模型文件](https://github.com/MR-DS-20/express-template/blob/master/src/models/base.model.ts)

# 创建控制器

控制器可以在来自路由器的请求和与模型交互的逻辑之间创建一个分离，帮助您遵守单一责任原则。

为了帮助减少重复，这里的建议是采用与模型相似的方法，创建一个`BaseController`类，处理所有需要的通用 CRUD 函数。

下面的摘录是 [base.controller.ts](https://github.com/MR-DS-20/express-template/blob/master/src/controllers/base.controller.ts) 文件的开始。

`jsonRes()`和`errRes()`函数提供了一个简单的可重用方法来适当地完成 HTTP 响应。现在，这个类可以为每个控制器扩展，其中可以实现独特的逻辑。下面的例子是一种使用`BaseController`类和适当的模型类创建控制器的方法。

在你看到尖括号(<，>)的`putFunction()`中，一个类型被传入。这种类型启用了 Typescript 的强大功能，有助于加快开发速度。

当您调用`findById()`或任何返回文档的方法时，您会得到一个承诺，它包含文档，但也为您提供了许多对给定文档执行的数据库功能。

传入该类型会告诉编译器和 IDE 正在发生什么，因此当您处理该对象时，您会看到可用的方法。[点击此处查看接口是如何构建的](https://github.com/MR-DS-20/express-template/blob/master/src/interfaces/example.interface.ts)。请继续阅读，更好地了解这是如何在路由器中实现的。

如果您不确定`this.model`或`this.create`是如何工作的，因为您看不到它们的声明，请记住它们是在 BaseController 类中声明的。

控制器的功能接受快速请求和响应对象，因为它们是路由调用时从快速路由器传递的对象。

# 路由器

这是发送到应用程序 HTTP 请求与路由器匹配的地方。基于类的方法创建 express 应用程序的能力在这里大放异彩，因为您可以用最少的努力为所有模型编写路线。请参见下面的 example.router.ts 文件:

前两个路由是在控制器中声明的，因为需要一些定制逻辑，然而，删除和获取路由使用由`BaseController`类声明的函数，所以不需要额外的编码。

将这些路由器导入您的服务器，您就可以开始了！

希望这已经给了你一些关于如何改进 Node.js Express 服务器的想法，我欢迎任何关于如何改进它的建议。编码快乐！

*更多内容看*[***plain English . io***](http://plainenglish.io/)