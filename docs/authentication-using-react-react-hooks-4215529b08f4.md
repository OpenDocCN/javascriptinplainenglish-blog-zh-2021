# 使用 React 挂钩将基类组件迁移到功能组件

> 原文：<https://javascript.plainenglish.io/authentication-using-react-react-hooks-4215529b08f4?source=collection_archive---------12----------------------->

![](img/6362b545392d064b2abdf497bac51547.png)

React 是目前可用的最著名的库之一。目前有数百家公司在使用 React，数百家公司选择 React 作为他们下一个产品和服务的下一个平台。

React 提出了两种类型的组件，即无状态组件和有状态组件。无状态组件通常是没有本地状态和不能访问生命周期方法的功能组件。有状态组件具有本地状态，可以访问生命周期方法。

在 React 16.8 之前，我们编写有状态组件的唯一选择是使用 JavaScript 基类组件。然而，React 16.8 引入了钩子概念，允许我们将功能组件编写为有状态组件。

我们将在这篇博文中使用的钩子如下所列。

1.  **使用状态**
2.  使用效果
3.  使用显示器
4.  使用选择器

useState 钩子允许我们在函数组件中有一个本地状态。我们在组件中声明 useState 的方式如下。

```
const [stateVariable, setStateVariable] = useState('');
```

useState 使用[数组析构](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)概念。useState 函数返回一个这样的数组`['', function]`。这个数组中的第一项是我们传递给 useState 的参数，它被赋值给`stateVariable`。而第二项是一个函数，它被分配给`setStateVariable`，我们稍后将在代码中调用它来设置、更新或更改组件的状态。

1.  使用状态
2.  **使用效果**
3.  使用显示器
4.  使用选择器

useEffect 是一个生命周期方法，在组件挂载时、状态或属性更改时以及组件卸载时或之前调用。要完全理解什么是 useEffect 以及它是如何工作的，请点击这个博客[帖子](https://daveceddia.com/useeffect-hook-examples/)了解更多细节。

1.  使用状态
2.  使用效果
3.  **使用 Dispatch**
4.  使用选择器

它相当于将调度映射到基类组件中的道具。要使用 useDispatch 钩子，我们将触发 useDispatch 函数并将其存储在一个变量中。当我们调用这个变量时，我们传递一个动作，这个动作是一个函数，它返回一个带有类型和有效负载属性的对象，作为一个带有数据的参数。Dispatch 将获取该对象，并搜索 reducer 以匹配其类型，并基于该类型执行操作。

1.  使用状态
2.  使用效果
3.  使用显示器
4.  **使用选择器**

useSelector 相当于将状态映射到基类组件中的 props。它接受一个函数参数并返回所需的状态部分。

这就是我们要用的钩子。在这篇博文中，我将把我的一篇[博文](https://medium.com/free-code-camp/login-using-react-redux-redux-saga-86b26c8180e)从类库组件迁移到功能组件，以便使用 react 进行用户认证和注册。这篇博文的代码可以在这里找到[。](https://github.com/zafar-saleem/react-login-hooks)

在这篇博文中，我将只迁移我以前博文中的组件，即页面，其余的 redux 和 redux saga 概念，如`store`、`actions`、`reducers`和`sagas`将保持原样，不需要更改。请到博客上继续关注，让这个项目成功。

说到这里，让我们来看看我们的第一个组件/页面`src/components/loginPage.js`。下面是这个组件/页面的代码。

在这个组件中，我从 React 导入了`useState`和`useEffect`钩子。我也从`react-redux`进口`useDispatch`和`useSelector`挂钩。然后在`loginPage`函数内部，我调用`useDispatch`函数并将其赋给`dispatch`变量。我们稍后将使用这个变量来调度一个动作。

接下来，我声明两个状态变量，即`notification`和`success`及其各自的状态方法，即`setNotification`和`setSuccess`，它们是方法，用于设置其各自变量的值。我们正在分配`useState`钩子来为它们设置默认值，即`empty string`和`false`被分配给各自的变量。

接下来我们调用`useSelector` hook，它返回这个组件所需的部分状态。

接下来我们调用`useEffect`方法，我们传递一个回调函数作为第一个参数，传递一个带有`login`的数组，这个数组有这个组件的必要状态信息，我们通过调用上面的`useSelector`钩子来获得。这意味着每当 login 中的属性被更新时，这个`useEffect`钩子将被调用。`useEffect`中的第二个论点可以被视为依赖关系。

在这里，我们基于从`useSelector`接收的值设置`notification`和`success`，如果`success`为真，我们用令牌设置 cookie。如果`login`不是未定义的，所有这些都会发生。

接下来是一个方法`onHandleLogin`,它基本上从登录表单获取电子邮件和密码，并以电子邮件和密码作为有效载荷发送一个`loginUserAction(email, password)`。

接下来，我们再次调用`useEffect`将`notification`和`success`重置回其初始值。这种效应称为卸载阶段。

最后，我们在 JSX 有一个登录表单，其中有电子邮件和密码作为输入字段和一个按钮来触发登录过程。

下一个组件是`src/components/registerPage.js`。下面是这个组件的代码。

在这个组件中，我们正在做与在`loginPage.js`中完全相同的事情。我们正在从各自的包中导入`useState, useEffect, useDispatch and useSelector`钩子。

在`registerPage`中，我们用状态方法声明了两个状态变量`notification`和`success`，用状态钩子声明了`setNotification`和`setSuccess`。

接下来我们通过分别调用`useDispatch`和`useSelector`钩子来声明`dispatch`和`register`变量。

然后我们调用`useEffect` hook，每当`register`更新时就会被调用。在这里面，我们设置了`success`和`notification`。

我们还在处理注册表，在注册表中我们获得所有详细信息，即用户的`email`、`password`和`name`以及派遣`registerUserAction(name, email, password)`。

还有第二个`useEffect`钩子，我们在其中重新设置`notification`。

最后，我们有 JSX 格式的登记表。

这就是这篇博文的基本内容。要做到这一点，你需要实现 redux 和 redux saga。请阅读[这篇博客](https://medium.com/free-code-camp/login-using-react-redux-redux-saga-86b26c8180e)来实现这些概念。顺便说一句，你仍然需要为这个项目运行后端。这个项目的后端解释[在这里](https://medium.com/free-code-camp/writing-scalable-architecture-for-node-js-2b58e0523d7f)。

[](https://github.com/zafar-saleem/react-login-hooks) [## 扎法尔-萨利姆/react-登录-挂钩

### 在使用这个项目之前，请确保你的服务器端运行，可以在这里找到克隆这个…

github.com](https://github.com/zafar-saleem/react-login-hooks) 

## 来自 [Zafar](https://zafarsaleem.medium.com) 的更多文章

1.  [AWS DynamoDB & Nextjs 建筑现实世界 App](https://www.webwinx.com/2023/01/28/building-real-world-app-by-combining-aws-dynamodb-nextjs/)
2.  [如何破解 Algolia 搜索增强 React](https://www.webwinx.com/2023/02/03/how-to-hack-algolia-search-to-enhance-react/)
3.  [使用 Grafbase 实现 GraphQL 后端的无服务器化](https://www.webwinx.com/2023/01/30/go-serverless-for-graphql-backend-with-grafbase/)
4.  [使用 React 的基于事件的架构](https://www.webwinx.com/2023/01/29/event-based-architecture-using-react/)

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。*

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.com/invite/GtDtUAvyhW) *

****用*** [***电路***](https://circuit.ooo/?utm=publication-post-cta) *为你的科技创业建立认知和采用。**