# 简单指南:在 Ionic 应用程序中使用 NGXS 的状态管理

> 原文：<https://javascript.plainenglish.io/the-easy-guide-using-state-management-with-ngxs-in-an-ionic-app-4d4e61c4e78?source=collection_archive---------6----------------------->

![](img/4b84deda155376a9c290086da370c311.png)

Photo by [Shunya Koide](https://unsplash.com/@shunyakoide?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 为什么要 NGXS 状态管理？

将变量或对象的一部分保存在某个地方，随时可以调用，这不是很容易吗？类似于在整个应用程序中保持不变的变量库，可以很容易地更新和调用。

对对象的任何更改(此后称为“状态”)也可以很容易地被查看和记录，这样我们作为开发人员就可以知道是否发生了更改以及何时发生的。

在我看来，这就是 NGXS 状态管理发挥作用的地方。在这种情况下，它帮助 web 应用程序或 Ionic 应用程序商店，并有效地管理其由对象和变量组成的状态。

这一特殊内容的创意应归功于比申·帕特尔。

## 先决条件

1.  熟悉离子型和角型。如果你以前从未用 Ionic 做过开发，这是一个很好的框架，可以让你更容易地开发渐进式网络和移动应用。
2.  熟悉打字稿。许多工作将在 TypeScript 中完成，因此需要对 TypeScript 有一点熟悉。

对于这个特殊的例子，Ionic I 将使用的版本是 Ionic 版本 5 (Angular ),带有 Ionic CLI(命令行界面)版本 6.13.1

我们将从 SpaceX API 文档中提取信息，这些文档是免费的，可以在此处轻松访问:

[](https://docs.spacexdata.com/#6b74116b-c47f-4181-b7e8-4adecfa9e165) [## r/SpaceX API 文档

### 注意:从 2020 年 11 月起，V3 API 已被弃用！所有现有的链接将继续工作，但不会有新的数据…

docs.spacexdata.com](https://docs.spacexdata.com/#6b74116b-c47f-4181-b7e8-4adecfa9e165) 

别担心，我们不会用 API 来发射火箭。没什么特别的。我们将使用一个简单的 API 来提取关于 SpaceX 公司的信息。

这只是一个来自以下 URL 的简单 GET 请求:

[https://api.spacexdata.com/v3/info](https://api.spacexdata.com/v3/info)

上面的链接应该返回一个包含 SpaceX 公司信息的 JSON 对象。

## 0.开始一个离子项目

我不能强调这一点不够，如果你不熟悉离子，请到这个网站开始:

[](https://www.ionicframework.com) [## 跨平台移动应用开发:Ionic 框架

### Ionic Framework 的应用程序开发平台构建了令人惊叹的跨平台移动、web 和桌面应用程序，只需一个…

www.ionicframework.com](https://www.ionicframework.com) 

确保选择 Angular 作为 Ionic 中使用的主要框架。

## 1.安装 NGXS

接下来，我们需要安装 NGXS，这将是我们组织状态的地方。

```
npm install @ngxs/store --save
```

安装以下 NGXS 库来帮助我们注销和存储状态也是一个好主意:

*登录器插件:*

```
npm install @ngxs/logger-plugin --save
```

*商店插件:*

```
npm install @ngxs/storage-plugin --save
```

## 2.使用服务调用 API 并存储在状态中

生成一个调用 SpaceX API 的服务。我将把这个服务称为网络服务。要在 Ionic 中生成此服务，请在命令行中运行以下命令:

```
ionic g service ngxs/network
```

这将生成一个名为 *ngxs* 的文件夹，其中包含 network.service.ts 文件。

在我们的 network.service.ts 文件中，添加以下内容来调用 SpaceX API。

第 10 到 12 行是我们调用 SpaceX 服务器的函数。

请注意，为了简单起见，我将使用一个典型的 Angular/common/http 库。如果你打算建立一个移动应用程序，我推荐你使用 Ionic Capacitor HTTP 库。

## 3.设置 NGXS 文件

在上一步创建的 *ngxs* 文件夹中创建以下文件:

*ngxs/action.ts*

*ngxs/state.ts*

**注意**:在某些情况下，你可能想创建一个 interface.ts 文件来声明 interface.ts，然而，这是一个简单的指南，我想把事情简单化。我将在 state.ts 文件中声明接口，而不是使用不同的文件。

在 action.ts 中，在 action.ts 文件中声明一个操作，如下所示:

稍后将在我们的商店调度功能中调用上述操作。现在不要担心它。

接下来，在 state.ts 文件中，我们需要做 3 件事:

1.  声明接口
2.  声明模型
3.  声明在执行上述函数时将采取的操作

我们的 state.ts 文件应该如下所示:

*   请注意，我们已经在第 4 行的 action.ts 中声明了我们的操作
*   我们还为我们使用 SpaceXInfoState 声明了 Injectable()
*   第 7 行到第 30 行是我们声明接口的地方。该接口基于调用 API 时的预期结果
*   第 32 行是我们声明初始状态并给我们的状态命名的地方，在这个例子中，它是 *SpaceXInfoState*
*   我们还在第 40 行声明了我们的网络服务
*   第 42 行到第 52 行是我们执行函数并通过使用 *patchState()* 保存对我们状态的响应的地方

## 4.在 app.module.ts 设置 NGXS

现在我们已经完成了网络服务、状态和动作文件中的所有艰苦工作，我们终于准备好在 app.module.ts 文件中声明 NGXS，以便在我们的应用程序中使用 NGXS。

我们的 app.module.ts 文件应该如下所示:

*   第 9、10 和 11 行是我们将 NGXS 属性导入应用程序的地方，这些属性是我们之前安装的
*   我们将导入的模块添加到第 23 到 31 行的模块导入列表中
*   在 NgxsModule 中，我已经将 SpaceXInfoState(在第 14 行导入)添加到将在该应用程序中使用的状态列表中。如果在 action.ts 文件中声明了更多的状态，请在这里添加它们。
*   另外，请注意，我已经添加了 HttpClientModule(第 13 行和第 32 行)。如果您使用 HTTP 电容器方法，则不需要添加它。

## 5.使用 store dispatch()获取数据

现在我们需要执行我们已经创建的操作。在我的例子中，我将执行 home.page.ts 文件中的函数。我们的 home.page.ts 文件应该如下所示:

*   第 2 到 4 行是我们导入`Select, Store`我们的动作(`GET_SPACEX_DATA`)和我们的状态(`SpaceXInfoState`)的地方
*   `ionViewWillEnter()`该功能将在每次加载主页时执行。在这个函数中，我们使用`store.dispatch`来执行我们在`state.ts`中声明的动作
*   为了拉取和声明数据，我还声明了`getData()`函数，该函数将在`store.dispatch`完成运行后执行。
*   在`getData()` 函数中，我们使用`selectSnapshot`将数据分配给`cto_propulsion`变量和`founded`变量。我们现在可以在 HTML 中使用`cto_propulsion`和`founded`，就像在任何典型的 angular 项目中一样。

给你，简单的柠檬榨汁机。上面显示的是使用 NGXS 存储和使用 selectSnapshot 从您的州获取数据的简单方法。只要会话仍然有效，状态就会保持不变。

你可以在这里结束，一切都会很好，但对于额外的学分…

…还有一件事…

好处:使用存储选择器来获取数据

您还可以使用存储选择器从您的状态中获取异步数据。我们需要将以下内容添加到我们的 *state.ts* 文件中:

*   在上面的 state.ts 文件中，我已经将第 42 行的`ceo`选择器添加到了第 45 行。
*   我们现在可以像这样使用`home.page.ts`中的`ceo` 选择器:

*   在上面的 home.page.ts 示例中，我在第 14 行添加了`ceo$`。这将创建一个异步变量，您可以在 Angular HTML 文件中使用它。在`ceo`状态中的任何变化将直接反映到`ceo$`变量中，无需任何额外的函数调用。

现在你知道了。以上并不是一个详尽的方法，但这是一个简单的方法来展示如何使用 NGXS 状态管理来存储数据，这些数据可以在 Ionic 应用程序中的任何地方轻松访问。

希望上面的文章能为您在应用程序中使用 NGXS 提供有用的入门指南。

*塞拉马特·孟加图拉卡*

*更多内容请看*[*plain English . io*](http://plainenglish.io/)