# 后座力初学者指南

> 原文：<https://javascript.plainenglish.io/getting-to-know-recoil-initializing-and-maintaining-react-application-state-with-asynchronous-c5c3eb114c39?source=collection_archive---------2----------------------->

![](img/a5ea27d1591e9059d7181bdf2ee1cedb.png)

(The forest for the trees)

## 用异步数据初始化和维护 React 应用程序状态

# 背景

自从 2020 年 5 月[推出](https://youtu.be/_ISAA_Jt9kI)以来，与 [React Context](https://reactjs.org/docs/context.html) 以及更成熟的 UI 不可知库(如 [Redux](https://redux.js.org/) 和 [MobX](https://mobx.js.org/) )相比， [ReactJS](https://reactjs.org/) 应用中的[反冲](https://recoiljs.org/)作为应用状态管理的替代方法已经有了大量的报道。

最近， [DemandStar](https://demandstar.com/) 的工程团队开始在我们的一些 ReactJS / [TypeScript](https://www.typescriptlang.org/) 应用中实现反冲作为 Redux 的替代。

激励我们团队进行反冲实验的一些因素包括整体性能、与功能组件的兼容性(特别是使用 [React hooks](https://reactjs.org/docs/hooks-intro.html) )、减少状态管理样板代码和支持[代码分割](https://reactjs.org/docs/code-splitting.html)——这并不意味着 Redux 不提供这些好处；然而，赞成和反对采用后坐力的论点已经在 [和](https://medium.com/better-programming/recoil-a-new-state-management-library-moving-beyond-redux-and-the-context-api-63794c11b3a5) [其他地方](https://dev.to/chandan/recoil-vs-redux-the-ultimate-react-state-management-face-off-35b)详细 [探讨过了。因此，与其在这里重复利弊，我们将直接进入我们的例子。](https://blog.logrocket.com/refactoring-redux-app-to-use-recoil/)

# 要求

## 为了实现功能对等，我们的主要要求有两个方面:

1.  我们需要用服务调用返回的数据初始化应用程序状态。
2.  我们的应用程序状态需要与后端保持同步。

# 示例应用程序:基本用户列表

## **在我们开始编码之前**

*   为了快速设置我们的开发环境(无论是在本地机器上还是通过在线 IDE，如 [codesandbox.io](https://codesandbox.io) )，我们将依赖 [create-react-app 和附加的 TypeScript 模板](https://create-react-app.dev/docs/getting-started/)。
*   本例还假设对[设置和实施反冲](https://recoiljs.org/docs/introduction/getting-started/)有基本的了解。

## 技术堆栈

我们的用户列表应用程序由以下元素组成(您可以在这里查看 GitHub 存储库):

*   [**创建-反应-应用**](https://create-react-app.dev/) **—** 基本设置
*   **打字稿—** 打字安全
*   [**Axios**](https://github.com/axios/axios)**—**服务请求库
*   **API 调用**[**https://reqres.in/api/users**](https://reqres.in/api/users)—异步“用户”数据(补充请求输入和[发展受阻](https://en.wikipedia.org/wiki/Arrested_Development))

## 声明类型

因为我们使用的是 TypeScript，所以如果我们从类型定义开始，我们就能充分利用类型安全。这些将涵盖我们的数据从服务请求到反冲状态和反应组件的形态。

## 配置服务呼叫

接下来，让我们确保示例服务调用正常工作。

我们配置的 URL 实际上是一个函数，其目的是随机切换一个查询参数(在本例中是页码)。当然，这并不重要，但它的目的只是为了展示我们调用 API 的反冲`selector`，每当它的依赖项发生变化时，它都会发出一个新的请求——下面会详细介绍。
因此，我们在模仿不断变化的后端数据，这样，随着 API 被连续调用，我们将会周期性地看到不同的数据集。

然后，我们将设置 Axios 调用来发出实际的 API 请求(我们也可以使用 JavaScript `[fetch()](https://javascript.info/fetch)`函数或其他替代函数，但是 Axios 适合我们团队当前的堆栈)。

## 用我们的 API 调用初始化反冲状态

我们希望用服务请求的结果来初始化我们的应用程序状态:这将满足我们上述的第一个功能需求。

因此，我们将设置一个反冲`selector()`函数，并从其内部`get()`函数返回 API 调用的响应。
一个`selector` [可选地接受](https://recoiljs.org/docs/api-reference/core/selector)一个`get()`和`set()`函数，但是出于这个例子的目的，我们将通过省略 setter 来保持我们的函数是只读的。

接下来，我们将定义反冲`atom()`函数`userListState`，React 组件代码将实际使用它。
这个`atom`将使用我们之前定义为*的`allUsersState` `selector`作为它的*默认值，从而创建一个依赖项，以便在发生更改时通知任何订阅的组件。

他们在一起:

## 更新反冲状态以重新查询 API 有效负载

为了完成我们的反冲状态，我们将通过添加一个 final `atom()`并在`allUsersState` `selector`的`get`函数中使用它作为依赖项来完成我们的第二个目标——保持应用程序状态与服务请求的结果同步。

采用这种方法的原因是，每当它的一个依赖关系发生变化时，就会调用`get()`函数。
在我们的示例中，我们将在 React list 组件上设置一个`onClick`处理程序(见下文),然后在每次单击不同的项目时更新一个`selectedUserEmailState`。

这里是完整的，更新的`state.ts`。

## 将所有这些放在一起:创建我们的 React 组件

现在我们已经有了我们的类型、服务调用和反冲状态逻辑，我们将把它们放在一起构建一个简单的 React 应用程序，它将与所有这些进行交互并显示它们。

根据最佳实践，我们将使用[表示组件/容器组件](https://scotch.io/courses/5-essential-react-concepts-to-know-before-learning-redux/presentational-and-container-component-pattern-in-react)模式，并将我们的`UserList`设置为容器组件。
这是我们将利用反冲`[Loadable](https://recoiljs.org/docs/api-reference/core/Loadable/)`对象的地方，它允许我们访问反冲`atom`或`selector`的当前状态。我们用来完成这项工作的钩子是`[useRecoilStateLoadable()](https://recoiljs.org/docs/api-reference/core/useRecoilStateLoadable/)`。
我们将把来自`userListState`原子的反冲状态数据作为属性传递给视图组件。我们还将设置`onClick`处理程序`handleUserClick`，并将其传递下去。

最后，我们将创建我们的表示或视图组件`UserListView`，这是一个仅用于显示的功能组件。在这里，我们接收状态和点击处理程序作为属性，并在状态发生变化时显示结果。

# 结论

这应该就结束了。这是一个简化的实现，但是我希望这篇文章提供了一些已经存在的好的反冲资源的合理汇编。

这是已完成示例的嵌入式视图:

The sample User List app on codesandbox.io

# 链接

*   这是完成的例子，托管在 [codesandbox.io](https://codesandbox.io/s/recoil-react-async-example-b6men) 上。
*   这里是 GitHub 上的来源。