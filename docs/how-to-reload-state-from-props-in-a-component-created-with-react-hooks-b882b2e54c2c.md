# 如何在用 React 钩子创建的组件中从 Props 重新加载状态？

> 原文：<https://javascript.plainenglish.io/how-to-reload-state-from-props-in-a-component-created-with-react-hooks-b882b2e54c2c?source=collection_archive---------9----------------------->

![](img/d91702a0af4609b1572599b64ed769f7.png)

Photo by [ASIA CULTURECENTER](https://unsplash.com/@asiaculturecenter?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须根据传入的属性值重新加载一个状态。

在本文中，我们将了解如何在使用 React 钩子创建的组件中从 props 重新加载状态。

# 观看道具随着使用效果而变化

挂钩让我们观察反应值的变化，包括道具。

因此，我们可以使用`useEffect`钩子来观察属性值的变化，并相应地更新我们的状态。

例如，我们可以写:

```
import { useEffect, useState } from "react";const Counter = ({ count }) => {
  const [countState, setCountState] = useState(count); useEffect(() => {
    setCountState(count);
  }, [count]); return <p>{countState}</p>;
};export default function App() {
  const [count, setCount] = useState(0); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <Counter count={count} />
    </div>
  );
}
```

我们有带`count`道具的`Counter`组件。

在组件内部，我们将`countState`状态设置为`count`的值作为初始值。

接下来，我们用回调函数调用`useEffect`钩子，回调函数用`count`调用`setCountState`，将`countState`的值设置为与`count`的值相同。

在`useEffect`的第二个参数中，我们传入一个带有`count`属性的数组来观察`count`属性的变化，并触发要调用的`useEffect`回调。

然后在`App`组件中，我们将`count`状态初始设置为 0。

我们有一个按钮，它调用一个函数，这个函数调用`setCount`来更新`count`状态，方法是用我们传入的回调将它加 1。

回调获取当前值`count`作为参数，并返回增加了 1 的新值。

在按钮下方，我们显示了`Counter`组件，我们通过将`count`道具设置为`count`状态作为其值来传入该组件。

现在，当我们点击增量按钮时，我们看到通过`count`道具渲染的最新`countState`。

# 结论

我们可以根据道具的变化来更新状态，方法是用`useEffect`钩子观察道具，然后调用状态改变函数，根据`useEffect`回调中的道具值来更新状态。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)