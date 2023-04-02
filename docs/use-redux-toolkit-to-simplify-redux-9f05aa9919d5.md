# 使用 Redux 工具包简化 Redux

> 原文：<https://javascript.plainenglish.io/use-redux-toolkit-to-simplify-redux-9f05aa9919d5?source=collection_archive---------11----------------------->

## 包含代码示例

![](img/75e1bbd679a363b9c2935e167608fd20.png)

# **简介**

## 什么是 Redux

Redux 是一个用于管理应用程序状态的开源 JavaScript 库。它通常与 React 或 Angular 等库一起用于构建用户界面。类似于脸书的通量建筑，它是由丹阿布拉莫夫和安德鲁克拉克。

## 什么是国家管理

状态管理是指对一个或多个用户界面控件(如文本字段、OK 按钮、单选按钮等)的状态的管理。在图形用户界面中。在这种用户界面编程技术中，一个 UI 控件的状态依赖于其他 UI 控件的状态

## 什么是 [Redux Toolkit](https://redux-toolkit.js.org/introduction/getting-started)

Redux Toolkit 是一个自以为是的、包含电池的工具集，用于高效的 Redux 开发。

## 为什么 Redux 不再流行了

React 和 Redux 被认为是大型 React 应用程序中管理状态的最佳组合。然而，由于以下原因，Redux 的受欢迎程度下降；

*   “配置 Redux 存储太复杂”
*   “我必须添加许多包才能让 Redux 做任何有用的事情”
*   “Redux 需要太多样板代码”

## Redux 拯救工具包

Redux toolkit 旨在解决上述问题。Redux 工具包的特性包括:

**Simple:** 包括简化常见用例的实用程序，比如存储设置、创建 reducers、不可变更新逻辑等等。

**固执己见**:为商店设置提供良好的默认设置，包括最常用的内置 Redux 插件。

**功能强大:**从 Immer 和 Autodux 等库获得灵感，让您编写“可变的”不可变更新逻辑，甚至自动创建完整的状态“切片”。

**有效**:让您专注于应用程序所需的核心逻辑，这样您就可以用更少的代码做更多的工作。

# Redux 工具包包括什么

Redux Toolkit 包括这些 API:

*   `[configureStore()](https://redux-toolkit.js.org/api/configureStore)`:如果你熟悉原始的 Redux，你会知道我们使用`createStore`来创建实际的商店。在 Redux Toolkit 中，我们将使用`[configureStore()](https://redux-toolkit.js.org/api/configureStore)`来代替。它做的事情和`createStore`一样，但是它以一种容易理解的方式自动组合一些减速器。默认情况下，它还包括`redux-thunk`，并支持使用 Redux DevTools 扩展。
*   通过将 Redux reducer 函数定义为函数的查找表来处理每种动作类型，简化了 Redux reducer 函数的创建。它还允许您通过在 reducers 中编写“可变的”代码来大大简化不可变的更新逻辑。
*   `[createAction()](https://redux-toolkit.js.org/api/createAction)`:接受动作类型字符串并返回使用该类型的动作创建函数。
*   `[createSlice()](https://redux-toolkit.js.org/api/createSlice)`:接受一个 reducer 函数的对象、一个切片名称、一个初始状态值，自动生成一个切片 reducer，并带有相应的动作创建者和动作类型。
*   `[createAsyncThunk](https://redux-toolkit.js.org/api/createAsyncThunk)`:接受一个动作类型字符串和一个返回承诺的函数，并基于该承诺生成一个调度`pending/fulfilled/rejected`动作类型的 thunk。
*   `[createEntityAdapter](https://redux-toolkit.js.org/api/createEntityAdapter)`:生成一组可重用的归约器和选择器，管理存储中的规范化数据。
*   [中的](https://github.com/reduxjs/reselect)`[createSelector](https://redux-toolkit.js.org/api/createSelector)` [实用程序](https://redux-toolkit.js.org/api/createSelector)重新选择库，重新导出以方便使用。

# 让我们再深入一点

## 配置存储()

`configureStore`接受单个配置对象参数，具有以下选项

## getdefaultMiddleware()

默认情况下，`[configureStore](https://soyoung210.github.io/redux-toolkit/api/configureStore)`会自动向 Redux store 设置添加一些中间件。

```
const store = configureStore({
  reducer: rootReducer
})
// Store has one or more middleware added, because the middleware list was not customized
```

如果您想要定制中间件列表，您可以向`configureStore`提供一组中间件函数:

```
const store = configureStore({
  reducer: rootReducer,
  middleware: [thunk, logger]
})
// Store specifically has the thunk and logger middleware applied
```

然而，当您提供`middleware`选项时，您需要负责定义*所有您想添加到商店中的中间件。`configureStore`除了您列出的以外，我不会增加任何额外的中间件。*

`getDefaultMiddleware`如果你想添加一些定制的中间件是有用的，但也仍然希望有默认的中间件被添加:

```
const store = configureStore({
  reducer: rootReducer,
  middleware: [...getDefaultMiddleware(), logger]
})
// Store has all of the default middleware added, _plus_ the logger middleware
```

## createReducer()

redux[reduce](https://redux.js.org/basics/reducers)通常使用`switch`语句来实现，每个已处理的动作类型都有一个`case`。

```
function counterReducer(state = 0, action) {
  switch (action.type) {
    case 'increment':
      return state + action.payload
    case 'decrement':
      return state - action.payload
    default:
      return stat
  }
}
```

这种方法效果很好，但容易出错，也容易遗忘`default`情况或设置初始状态。

**创建减速器()进行救援**

`createReducer`有两个论点。第一个是初始状态。第二个是从动作类型到*用例缩减器*的对象映射，每个用例缩减器处理一个特定的动作类型。

```
const counterReducer = createReducer(0, {
  increment: (state, action) => state + action.payload,
  decrement: (state, action) => state - action.payload
})
```

## createAction()

如前所述，`createAction`助手将这两个声明合并为一个。它采用一个动作类型，并返回该类型的动作创建者。可以在没有参数的情况下调用动作创建器，也可以将`payload`附加到动作中。此外，动作创建者覆盖[到字符串()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)以便动作类型成为其字符串表示。

```
const increment = createAction('counter/increment')
const decrement = createAction('counter/decrement')
const counterReducer = createReducer(0, {
  [increment]: (state, action) => state + action.payload,
  [decrement]: (state, action) => state - action.payload
})
```

## 创建虱子()

一种接受初始状态、充满缩减器功能的对象和“切片名称”的功能，并自动生成与缩减器和状态相对应的动作创建者和动作类型。

**示例**

## createAsyncThnuk()

一个接受 Redux 操作类型字符串的函数和一个应该返回承诺的回调函数。它基于所提供的动作类型生成承诺生命周期动作类型，并返回一个 thunk 动作创建者，该创建者将运行承诺回调并基于返回的承诺分派生命周期动作。

**用法**

# 结论

如果你开始使用 reaction-redux，我会建议你使用 redux 工具包，因为它更容易阅读和理解。它还抽象了许多样板代码，这些代码通常会导致不必要的复杂情况，尤其是对于初学者来说。

总之，Redux 是一个很棒的状态管理库，它不仅仅是为 React 生态系统而构建的。它可以被整合到其他框架中，比如 [Angular](https://angular.io/) 和 [Vue。](https://vuejs.org/)

在他们的 [*文档*](https://redux-toolkit.js.org/introduction/getting-started) 中阅读更多关于 Redux Toolkit 的信息

**快乐编码！**