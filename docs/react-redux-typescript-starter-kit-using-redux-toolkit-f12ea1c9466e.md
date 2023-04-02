# 使用 Redux 工具包的 React、Redux、TypeScript 初学者工具包

> 原文：<https://javascript.plainenglish.io/react-redux-typescript-starter-kit-using-redux-toolkit-f12ea1c9466e?source=collection_archive---------5----------------------->

你正在开始一个新项目？你想同时使用所有最新的技术达到生产水平的标准。到本文结束时，您将拥有一个生产就绪的 react 应用程序，它使用 redux、redux-thunk 和 TypeScript。

![](img/8ea1c1336429e73ed105a6baac995965.png)

最初，这篇文章是基于我在过去三年构建 react 应用时学到并构建的一组模式而写的。该模式本质上是一个动作文件，是该文件的缩减器，然后是一个根缩减器来包装所有这些文件。在团队中，我们会花时间决定/辩论/争论我们的 react/redux 应用程序使用的最佳模式，并最终采用一种“科学怪人”方法，这种方法有效，但固执己见，尽管团队与团队之间一直不同步。

然后 [@acemarke](https://twitter.com/acemarke) 一个 redux 维护人员联系我，跟我分享了他们的 Redux 工具包。

Redux Toolkit 是一套帮助在 web 应用程序中集成和使用 Redux 的最佳实践、模式和功能。是的，它固执己见，起初感觉很奇怪，但它是由 redux 的创造者维护的，所以我认为我们可以相信工具包的发展方向。这也让你远离了很多元决策，让你可以更专注于重要的事情:用户和性能的 UX。

所以我们开始吧！有一个`create-react-app`类型脚本模板，所以将使用它开始。

```
npx create-react-app my-app — template redux-typescript
```

这个`create-react-app`模板将为您设置一个简单的计数器应用程序。它将包含一个名为`counter`的减速器切片。

在这篇文章中，我将扩展模板，这样我们可以更好地了解正在发生的事情。我还将介绍 Redux thunk，并从服务器请求一些数据。

在我们使用`create-react-app`成功创建了我们的项目之后，我们将拥有一个闪亮的新项目。

如果您想查看源代码，您可以在此处查看:

[](https://github.com/davidjamescarter/react-redux-thunk-typescript-redux-toolkit-starter-kit) [## David jamescarter/react-redux-thunk-typescript-redux-toolkit-starter-kit

### 这个项目是用 Create React App 引导的，使用了 Redux 和 Redux Toolkit 模板。在项目中…

github.com](https://github.com/davidjamescarter/react-redux-thunk-typescript-redux-toolkit-starter-kit) 

# 商店

下面是我们的`store.ts`,我们从`@reduxjs/toolkit`导入三个对象，让它们通过。

## `configureStore`

`configureStore({reducer, middleware, devTools, preloadedState, enhancers})`

所以`configureStore`函数接受单个配置对象参数，有以下选项:`reducer, middleware, devTools, preloadedState, enhancers` [此处阅读更多。](https://redux-toolkit.js.org/api/configureStore)

> 对标准 Redux `createStore`函数的友好抽象，为商店设置添加了良好的默认值，以获得更好的开发体验。

## `Action`

`Action`是一个内置在 Redux 库中的动作类型。

## 思维活动

`ThunkAction`是一个动作类型，内置于 Redux Thunk 库中。Redux thunk 是一个通用的中间件，Redux 推荐使用它来编写与存储交互的同步和异步逻辑。[点击此处阅读更多内容。](https://github.com/reduxjs/redux-thunk)

> thunk 是一个包装表达式的函数，用于延迟该表达式的求值。在 Redux 中，thunk 接受参数`dispatch`和`getState`。

正如 redux 所推荐的，一个可重用的`AppThunk`类型在`store.ts`中定义一次，每当你写一个 thunk 时就被重用。我们将在下一节看到更多这方面的内容。

# 部分

现在，我们已经建立了一个正常运行的商店，我们可以更仔细地看看这些商店的每一部分。这是 Redux Toolkit 引入的新概念。`slice`是一个工厂功能，当给定一个`name`、`initialState`和一组减速器功能时，它产生一个减速器并自动产生动作。

> 一个函数，它接受一个初始状态、一个充满 reducer 函数的对象和一个“片名”，并自动生成与 reducer 和状态对应的动作创建者和动作类型。

切片的好处在于，它允许我们编写更少的代码，并将相关的代码放在一起。我们不再需要 6–7 个文件来创建存储片。这是我们的`weatherSlice.ts`:

这里我们有一个完整的存储片，它在一个可读、可管理的文件中创建了一个缩减器、操作和选择器。

在这个例子中，我们将特别关注 thunk 操作。然而，我已经包含了一个简单的非异步动作`increment`来演示如何做，这将会减少工具包，见第 28 行。

# 使用 Redux thunk 的 API 请求

我们想要做的是通过 thunk 动作从 api 请求一些数据，就像在现实世界中一样。管理 JS 应用中的异步行为有很多解决方案，但是 redux 团队推荐 thunks 用于简单的异步行为。

> 我们推荐[使用 Redux Thunk 中间件作为标准方法](https://github.com/reduxjs/redux-thunk)，因为它足以满足大多数典型用例(比如基本的 AJAX 数据获取)。此外，在 thunks 中使用`async/await`语法使得它们更容易阅读。

## `createAsyncThunk`

所以让我们使用 Redux Toolkit `createAsyncThunk`函数创建一个 thunk 动作。您可以在第 5 行看到这个函数被导入到了`weatherSlice.ts`文件中。

使用`createAsyncThunk`的好处之一是它返回一个 Redux thunk 动作创建器。该函数将为附加的`pending`、`fulfilled`和`rejected`案例提供普通操作创建器。这些可以用作管理组件加载状态的方法，例如渲染加载微调器和错误处理。

通过使用`extraReducer`——这是`createSlice`工厂功能的最后一个特征。它允许我们编写逻辑，而本质上不产生动作。这对于基于“外部”动作编写逻辑非常有用。

需要记住的一点是，如果动作类型字符串在`reducers`和`extraReducers`中都被引用，那么来自`reducers`的函数将被用来处理动作类型。

# 在组件中调度 Thunk 操作

现在我们已经设置了我们的`weatherSlice`,让我们在`Weather.ts`切片组件文件中调用我们的新 thunk 动作`fetchWeatherForecast()`。

这是相当标准的东西，我们使用`react-redux` `useDispatch()`函数来调度我们的`fetchWeatherForecast()`动作。

然而正如你所看到的，我们没有使用非类型化版本的`useDispatch()`和`useSelector()`钩子。可以将`RootState`和`AppDispatch`类型导入到每个组件中。然而，正如 Redux 团队所建议的，最好创建预键入版本。[点击此处阅读更多内容。](https://react-redux.js.org/using-react-redux/usage-with-typescript)

这是一个简单的 React TypeScript 应用程序，它利用了 Redux 工具包。它使用 Redux thunks 和 async/await 发出一个简单的异步请求。然后用键入的选择器选择该数据。没什么特别的，但它确实做到了这是一种干净、规定的方式，几乎没有样板文件，比过去的 redux 设置更具凝聚力。

这是连续系列的一部分。接下来，我将扩展 Thunk 操作以使用`Promise.all()`,并更详细地介绍 TypeScript 和 React 的其他方面。

如果你有任何问题，或者你想被记录的事情，请留下评论。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)