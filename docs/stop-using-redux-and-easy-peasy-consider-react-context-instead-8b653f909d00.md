# 停止使用 Redux，改用这个

> 原文：<https://javascript.plainenglish.io/stop-using-redux-and-easy-peasy-consider-react-context-instead-8b653f909d00?source=collection_archive---------6----------------------->

## 在你的应用中使用 React 上下文来减少样板代码

![](img/559853cd406f42cef236c27d91b233a8.png)

Source: Pexels

之前我写了[停止使用 Redux——如果你想要](https://betterprogramming.pub/stop-using-redux-consider-easy-peasy-if-you-want-3214c41bcce5),那就简单了，它像病毒一样传播开来，我的一些读者发表了评论，要求我将它与 React 上下文进行比较。

这就是了。

嗯，我是一个创建网站的全栈式 web 开发人员。有时候，我得到的项目可以在一周内完成，有些则需要几个月。

这是因为客户有一些基本的需求，比如一些人喜欢 Redux、Easy Peasy 或 Context，而另一些人说你可以自由使用任何状态管理工具。

为此，我必须学习和实现特定的状态管理工具。

所以今天，我将用一个简单的例子来比较 Context、Redux 和 Easy Peasy。

我们开始吧。

## 为什么我们要使用 React Context、Redux 和 Easy Peasy？

其实问题是“道具钻”。简单来说，当我们想要在不同的组件中使用特定的道具时，我们必须在众多的组件中手动传递道具，以便在特定的组件中使用。

![](img/5bfe423a8f172d34cc392882e1079845.png)

Source: Author

假设我们想要组件 2、5 和 7 中的特定道具。为此，我们必须通过不同的组成部分。

有点烦人。因此，我们使用了 React Context、Redux 和 Easy Peasy。

# 使用 Redux

Redux 是一个状态管理工具(容器)，我们在其中创建一个 store，定义一个 action 和 reducer，调用 dispatch 函数。

但是什么是*储存*、*动作*、*减速*、*调度*？

一个*存储库*仅仅是一个保存所有状态的状态容器。

一个*动作*顾名思义，会做一些事情。简单来说，就是说要做什么。

*减速器*知道怎么做动作。

最后， *dispatch* 是一个分派动作的函数。

就这样，再简单不过了。

现在让我们举一个简单的例子。这里的示例将数字增加 1。

为此，您需要创建一个 React 应用程序。

```
npx create-react-app myapp
```

这将创建一个名为`myapp`的 React 应用程序。你可以根据自己的选择来命名任何东西。

现在安装使用 Redux 所需的依赖项。

```
npm install redux react-redux
```

它将安装两个依赖项，Redux 和 [React-Redux](https://react-redux.js.org/) 。Redux 是状态管理工具，React Redux 会将你的 React app 与 Redux 绑定。

在`src`文件夹中，你可以看到`index.js`文件。这里我们将创建商店，所以复制并粘贴下面的代码。

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { createStore } from "redux";
import { Provider } from "react-redux";// Storelet store = createStore();ReactDOM.render(
<Provider store={store}>
<App />
</Provider>,document.getElementById("root"));
```

这里我们导入了`createStore`，会创建一个商店。并且`Provider`将为我们提供商店。

商店会带一个减压器。我们将在后面定义它。

简单来说，我们创建了一个商店。

```
let store = createStore();
```

然后我们将它应用到我们的应用程序组件中。

```
<Provider store={store}>
<App />
</Provider>
```

现在在你的`src`文件夹中创建两个文件夹。一个是`actions`，另一个是`reducers`。

`actions`文件夹将包含一个动作文件，而`reducers`文件夹将包含一个减速器文件。

在`actions`文件夹中创建一个文件`index.js`。

```
export const increment = () => {
return {
 type: "INCREMENT",
};
};
```

这是一个告诉减速器增加的功能。

现在在`reducers`文件夹中，创建一个文件`add.js`。

这里将产生增加状态的逻辑。我们也将状态定义为等于 0。

简单地说，我们已经定义了一个将状态增加 1 的情况。

```
const add = (state = 0, action) => {switch (action.type) {
case "INCREMENT": return state + 1;
default: return state;
}};export default add;
```

在`reducers`文件夹中创建一个`index.js`文件，并粘贴以下代码。

```
import add from "./add";
import { combineReducers } from "redux";const everyReducers = combineReducers({
add: add
});export default everyReducers;
```

这里，我们已经导入了我们的 add reducer。

但是为什么是这个文件？将每个减速器组合起来，放在一个文件中。

简单来说，你需要在全局存储内部传递 reducer。但是如果你有不止一个减速器呢？那你可以这样做。

**将减速器交给商店**

既然定义了动作和还原器，那就传给店家吧。

在您的`src`文件夹中，您可以看到`index.js`文件(不要进入您的 actions 文件夹)。

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { createStore } from "redux";
import everyReducers from "./reducers/index";
import { Provider } from "react-redux";// Storelet store = createStore(everyReducers);ReactDOM.render(
<Provider store={store}>
<App />
</Provider>,document.getElementById("root"));
```

我们已经从`reducers`文件夹中导入了`everyReducers`并将其传递给了商店。

**在我们的应用程序中显示**

到目前为止，我们已经完成了创建商店的逻辑，但是还没有显示它。

在您的`src`文件夹中，您可以看到`App.js`文件。打开它，粘贴下面的代码。

```
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { increment } from "./actions/index";
import "./App.css";function App() {
const add = useSelector((state) => state.add);
const dispatch = useDispatch();return (
<div className="App">
<h1> Increment the count {add} </h1>
<button onClick={() => dispatch(increment())}>+</button></div>
);
}
```

这里我们导入了`useSelector`和`useDispatch`，`useSelector`来使用我们想要使用的减速器，`useDispatch`来调度动作。

仅此而已。我们已经实施了。

Src: Giphy

# 使用简单的豌豆

现在让我们用 Redux 的替代方案 Easy Peasy 实现相同的功能。

如果你已经清楚地阅读了上面的 Redux 概念，你将在几分钟内学会简单。为此，你不需要行动和减速器文件夹。

我正在创建一个新的文件夹以方便使用。您还可以在您的首选目录中创建新的 React 应用程序。

```
npx create-react-app learneasypeasy
```

在里面，安装简单的软件包。

```
npm install easy-peasy
```

**创建存储文件夹**

在您的`src`文件夹中创建一个存储文件夹。在其中，创建一个`add.js`文件。

```
import { createStore, action } from "easy-peasy";const store = createStore({
increment: {
counter: 0,
add: action((state) => {
state.counter = state.counter + 1;
}),
},
});export default store;
```

这里我们在一个文件中定义了所有的东西，一个带有状态和动作的存储。

我们已经将计数器初始化为 0，一个名为`add`的动作将递增计数器。

**将商店打包至你的应用**

现在是时候用你的应用来包装商店了。

在`src`文件夹中，转到`index.js`文件并粘贴下面的代码。

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { StoreProvider } from "easy-peasy";
import store from "./store/add";ReactDOM.render(
<StoreProvider store={store}>
<App />
</StoreProvider>,document.getElementById("root")
);
```

**在你的应用中显示**

我们已经创建了商店，应用了动作，甚至用商店包装了我们的应用。

现在是展示的时候了。

访问`src`文件夹内的`App.js`，粘贴以下代码。

```
import React from "react";
import { useStoreState, useStoreActions } from "easy-peasy";
import "./App.css";function App() {
const increment = useStoreState((state) => state.increment.counter);const add = useStoreActions((actions) => actions.increment.add);return (
<div className="App">
<h1> Increment the count {increment} </h1>
<button onClick={add}>+</button>
</div>
);}export default App;
```

要使用状态，必须导入`useStoreState`，要使用动作，必须导入`useStoreActions`。

要了解更多信息，您可以访问 npm 上的 [Easy Peasy。](https://www.npmjs.com/package/easy-peasy)

输出将保持不变。

# 使用反应上下文

在这里，我也将创建一个新文件夹。

```
npx create-react-app learncontext
```

它将比上面所有的状态管理工具更简单。

在 src 文件夹中创建一个`Context.js`文件。并定义上下文初始化。

```
import React, { useState, createContext } from "react";export const IncrementContext = createContext();export const IncrementProvider = ({children}) => {
const [increment, setIncrement] = useState(0);return (
<IncrementContext.Provider value={{ increment, setIncrement }}>
{children}
</IncrementContext.Provider>);};
```

这里，increment 和 setIncrement 将传递给每个孩子。

最后在你的 App.js 里面粘贴下面的代码。

```
import { IncrementProvider, IncrementContext } from "./Context";
import { useContext } from "react";
import "./App.css"const Child = () => {
const { increment, setIncrement } = useContext(IncrementContext);return (
<div className="App">
<h1>{increment}</h1>
<button onClick={() => setIncrement(increment+1)}>+</button>
</div>
);};export default function App() {
return (
<div className="App">
<IncrementProvider>
<Child />
</IncrementProvider>
</div>);}
```

就这样，我们实现了使用 React 上下文的增量功能。

您还可以为操作创建一个文件夹，为使用 React 上下文创建一个 reducer，但我发现这更简单。

# 让我们结束吧

嗯，我不反对任何状态管理工具，选择一个适合你的是你的愿望。

我刚刚比较了三种状态管理工具，让您对它们的工作原理有一个大致的了解。

就这样——谢谢。

[](/11-web-development-tools-i-use-every-day-because-they-make-my-life-easier-54ede59743c2) [## 我每天都在使用的 11 个 Web 开发工具，因为它们让我的生活变得更加轻松

### 他们也一定会为你做同样的事情。

javascript.plainenglish.io](/11-web-development-tools-i-use-every-day-because-they-make-my-life-easier-54ede59743c2) [](/8-life-lessons-a-programmer-with-30-years-of-experience-taught-me-2a9fb090a398) [## 一个有 30 多年经验的程序员教给我的 8 条人生经验

### 就连千禧一代也在放弃六位数的技术工作。

javascript.plainenglish.io](/8-life-lessons-a-programmer-with-30-years-of-experience-taught-me-2a9fb090a398) 

# 常见问题:

1.  能不能用 Redux-Toolkit 之类的其他库？

= >是的，我的朋友，概念是相似的，所以你可以自由使用它。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)