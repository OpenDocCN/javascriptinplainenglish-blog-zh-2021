# 如何在 React 组件之间共享状态

> 原文：<https://javascript.plainenglish.io/how-to-share-states-between-react-components-5817a8d7f68b?source=collection_archive---------9----------------------->

![](img/85f2502005bbb3c33863488ae4943627.png)

Photo by [Elaine Casap](https://unsplash.com/@ecasap?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在组件之间共享状态是我们在 React 中要做的很多事情。

在本文中，我们将研究在 React 中组件之间共享状态的方法。

# 提升状态

如果两个子组件有相同的父组件，那么我们可以将想要共享的状态从子组件添加到父组件中。

例如，我们可以写:

```
import React, { useState } from "react";const DescendantA = ({ count, onCountChange }) => {
  return (
    <button onClick={() => onCountChange((count) => count + 1)}>
      Click me {count}
    </button>
  );
};const DescendantB = ({ count, onCountChange }) => {
  return (
    <button onClick={() => onCountChange((count) => count + 1)}>
      Click me {count}
    </button>
  );
};export default function App() {
  const [count, setCount] = useState(0);
  return (
    <>
      <DescendantA count={count} onCountChange={setCount} />
      <DescendantB count={count} onCountChange={setCount} />
    </>
  );
}
```

我们有`DescendantA`和`DescendantB`组件，它们都有`App`作为它们的共同祖先。

所以为了共享一个状态，我们把状态放在`App`中。

我们有在`App`中定义的`count`状态。

我们将`count`传递给`DescendantA`和`DescendantB`组件。

同样，我们将`onCountChange`传递给`DescendantA`和`DescendantB`。

在`DescendantA`和`DescendantB`中，我们调用`onCountChange`并显示`count`值。

# 上下文 API

在两个组件之间共享状态的另一种方式是使用上下文 API。

上下文 API 允许我们在上下文提供者中的任何组件之间共享状态。

例如，我们可以写:

```
import React, { useContext, useState } from "react";const CountContext = React.createContext("count");const DescendantA = () => {
  const { count, setCount } = useContext(CountContext); return (
    <button onClick={() => setCount((c) => c + 1)}>Click me {count}</button>
  );
};const DescendantB = () => {
  const { count, setCount } = useContext(CountContext); return (
    <button onClick={() => setCount((c) => c + 1)}>Click me {count}</button>
  );
};export default function App() {
  const [count, setCount] = useState(0); return (
    <CountContext.Provider value={{ count, setCount }}>
      <DescendantA />
      <DescendantB />
    </CountContext.Provider>
  );
}
```

我们调用`React.createContext`来创建上下文。

然后我们定义`DescendantA`和`DescendantB`，后者调用`useContext`来获取上下文。

`CountContext.Provider`的`value`道具就是`useContext`返回的东西。

所以我们可以从返回值中得到`count`和`setCount` getter 和 setter。

并且在每个组件中，我们都有设置`count`的按钮。

在`App`中，我们将`CountContext.Provider`包装在`DescendantA`和`DescendantB`中，这样我们就可以在两个组件中使用上下文。

# 状态管理解决方案

在多个组件之间共享数据的另一种方式是使用状态管理解决方案。

React 应用程序的一个流行的状态管理解决方案是 Redux 和 React-Redux。

要使用它，我们可以写:

`index.js`

```
import { StrictMode } from "react";
import ReactDOM from "react-dom";
import { createStore } from "redux";
import { Provider } from "react-redux";
import App from "./App";const rootReducer = (state = 0, action) => {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    default:
      return state;
  }
};const store = createStore(rootReducer);const rootElement = document.getElementById("root");
ReactDOM.render(
  <StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </StrictMode>,
  rootElement
);
```

`App.js`

```
import React from "react";
import { useDispatch, useSelector } from "react-redux";const DescendantA = () => {
  const dispatch = useDispatch();
  const count = useSelector((state) => state); return (
    <button onClick={() => dispatch({ type: "INCREMENT" })}>
      Click me {count}
    </button>
  );
};const DescendantB = () => {
  const dispatch = useDispatch();
  const count = useSelector((state) => state); return (
    <button onClick={() => dispatch({ type: "INCREMENT" })}>
      Click me {count}
    </button>
  );
};export default function App() {
  return (
    <>
      <DescendantA />
      <DescendantB />
    </>
  );
}
```

在`index.js`中，我们有`rootReducer`,它接受`state`值并基于我们分派的动作类型返回商店的最新值。

我们将`rootReducer`传递给`createStore`来创建一个 Redux 商店。

然后我们将`store`传递给 React-Redux `Provider`组件，让我们使用`Provider`中任何组件的存储。

在`App.js`中，我们有`DescendantA`和`DescendantB`，它们调用`useDispatch`钩子来获得`dispatch`函数。

`dispatch`让我们向商店发送一个动作。

同样，我们用回调来调用`useSelector`钩子，以返回回调中的值，也就是`rootReducer`的最新返回值。

当我们点击按钮时，我们调用`dispatch`并将`type`设置为`'INCREMENT'`以提交类型为`'INCREMENT'`的动作。

现在我们应该看到`count`更新了。

# 结论

有几种方法可以让我们在组件之间共享状态。

*更多内容尽在* [***说白了***](http://plainenglish.io)