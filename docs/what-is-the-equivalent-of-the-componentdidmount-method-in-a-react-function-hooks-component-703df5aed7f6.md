# 在反应函数/钩子组件中，什么是组件安装方法的等价物？

> 原文：<https://javascript.plainenglish.io/what-is-the-equivalent-of-the-componentdidmount-method-in-a-react-function-hooks-component-703df5aed7f6?source=collection_archive---------8----------------------->

![](img/52936a7f69ec37756ccd9a44e1ff47bd.png)

Photo by [Michael Yero](https://unsplash.com/@_yero?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我们用类创建反应组件时，我们运行我们的代码，当组件装入`componentDidMount`钩子时加载。

但是，对于反应组件，这是不可用的。

在本文中，我们将看看如何使用 React 函数组件中的`componentDidMount`钩子产生相同的结果。

# useEffect 钩子

只有当组件挂载时才能运行代码，我们可以使用`useEffect`钩子。

如果我们传入一个空数组作为第二个参数，那么第一个参数中的`useEffect`回调将只在组件挂载时运行。

例如，我们可以写:

```
import React, { useEffect } from "react";export default function App() {
  useEffect(() => {
    console.log("mounted");
  }, []); return <div className="App"></div>;
}
```

现在我们应该只在安装组件时看到记录的`'mounted'`字符串。

# 反应挂钩等同于组件更新

`componentDidUpdate`生命周期方法的等价物也是`useEffect`钩子。

`componentDidUpdate`当状态或道具改变值时运行。

我们也可以对`useEffect`做同样的事情，将我们想要观察的状态或属性值传递到数组中，就像传递到`useEffect`的第二个参数中一样。

例如，我们可以写:

```
import React, { useEffect, useState } from "react";const Count = ({ count }) => {
  useEffect(() => {
    console.log(count);
  }, [count]); return <p>{count}</p>;
};export default function App() {
  const [count, setCount] = useState(0); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <Count count={count} />
    </div>
  );
}
```

用`Count`组件中的`useEffect`挂钩观察`count`支柱的更新。

要观察一种状态，我们可以写:

```
import React, { useEffect, useState } from "react";export default function App() {
  const [count, setCount] = useState(0); useEffect(() => {
    console.log(count);
  }, [count]); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <p>{count}</p>
    </div>
  );
}
```

我们用`useEffect`钩同样的方式观察`count`状态。

# 等效于组件的反作用挂钩将卸载

反应类组件中的`componentWillUnmount`生命周期方法允许我们在卸载组件时运行代码。

我们可以再次用`useEffect`钩子做同样的事情。

我们只需要在`useEffect`回调中返回一个函数就可以了。

我们返回的函数将在组件卸载时运行。

例如，我们可以写:

```
import React, { useEffect } from "react";export default function App() {
  useEffect(() => {
    console.log("mounted");
    return () => {
      console.log("unmounted");
    };
  }, []); return <div className="App"></div>;
}
```

在第`useEffect`回调中返回一个函数。

当我们卸载`App`组件时，应该会看到`'unmounted'`。

# 结论

我们可以使用反应函数组件中的`useEffect`钩子来做生命周期方法可以在类组件中做的事情。