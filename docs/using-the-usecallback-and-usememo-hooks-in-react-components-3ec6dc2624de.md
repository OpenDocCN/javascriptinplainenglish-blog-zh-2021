# 在 React 组件中使用 useCallback 和 useMemo 挂钩

> 原文：<https://javascript.plainenglish.io/using-the-usecallback-and-usememo-hooks-in-react-components-3ec6dc2624de?source=collection_archive---------15----------------------->

![](img/3826150db4441c70f3a94d9bc14989d4.png)

Photo by [Paolo Chiabrando](https://unsplash.com/@chiabra?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`useCallback`和`useMemo`挂钩是除了基本的`useState`和`useEffect`挂钩之外增加的两个更高级的挂钩。

它们在不同的方面都很有用。

在本文中，我们将看看如何在 React 组件中使用`useCallback`和`useMemo`钩子。

# `useCallback`

`useCallback`钩子用于记忆我们可能多次调用的回调。

使用`useCallback`钩子，我们可以缓存组件中的回调，这样它们就不会被创建多次，除非状态或属性发生改变。

例如，不写:

```
import React from "react";export default function App() {
  const handleClick = () => {
    console.log("Clicked");
  };
  return <button onClick={handleClick}>Click Me</button>;
}
```

我们可以写:

```
import React, { useCallback } from "react";export default function App() {
  const handleClick = useCallback(() => console.log("Clicked"), []); return <button onClick={handleClick}>Click Me</button>;
}
```

我们将回调函数传递给`useCallback`钩子，这样当我们点击按钮时，我们在第一个参数中传递的函数就会被调用。

但是`handleClick`函数只创建一次，而不是每次渲染。

第二个参数是一个数组，在这里我们可以传入在函数中可以观察到的项目。

例如，如果我们写:

```
import React, { useCallback, useState } from "react";export default function App() {
  const [num, setNum] = useState(0); const increment = useCallback(() => setNum((c) => c + 1), []);
  const handleClick = useCallback(() => console.log(num), []); return (
    <>
      <button onClick={increment}>Increment</button>
      <button onClick={handleClick}>Click Me</button>
    </>
  );
}
```

`handleClick`函数将总是记录 0，因为该函数仅在安装组件时创建，因为我们在第二个参数中有一个空数组。

但是，如果我们将`[num]`传递给`useCallback`:

```
import React, { useCallback, useState } from "react";export default function App() {
  const [num, setNum] = useState(0); const increment = useCallback(() => setNum((c) => c + 1), []);
  const handleClick = useCallback(() => console.log(num), [num]); return (
    <>
      <button onClick={increment}>Increment</button>
      <button onClick={handleClick}>Click Me</button>
    </>
  );
}
```

然后，当我们单击 Click Me 时，控制台日志显示`num`的最新值。

这是因为自从我们在`useCallback`的第二个参数中传递`[num]`后，当`num`发生变化时，会重新创建`handleClick`函数。

# `useMemo`

当它所依赖的任何一个状态改变时，`useMemo`钩子让我们计算一个从现有状态得到的值。

例如，我们可以写:

```
import React, { useCallback, useMemo, useState } from "react";export default function App() {
  const [num1, setNum1] = useState(0);
  const [num2, setNum2] = useState(0); const increment1 = useCallback(() => setNum1((c) => c + 1), []);
  const increment2 = useCallback(() => setNum2((c) => c + 1), []);
  const sum = useMemo(() => num1 + num2, [num1, num2]); return (
    <>
      <button onClick={increment1}>increment 1</button>
      <button onClick={increment2}>increment 2</button>
      <p>num1: {num1}</p>
      <p>num2: {num2}</p>
      <p>sum: {sum}</p>
    </>
  );
}
```

我们有`num1`和`num2`状态，当我们点击按钮时它们会改变。

然后我们定义`sum`变量，它是从`useMemo`钩子赋值的。

我们传入一个函数，返回加在一起的`num1`和`num2`。

在`useMemo`的第二个参数中，我们传入了我们正在观察的`num1`和`num2`。

意味着当`num1`或`num2`发生变化时，`useMemo`回调的返回值将被赋给`sum`。

因此，当我们点击其中一个按钮时，`sum`就会发生变化。

# 结论

我们可以使用`useCallback`来缓存函数，只在状态或属性改变时重新创建它们。

`useMemo`让我们创建从状态或属性值派生的变量，并缓存它们，直到任何相关值发生变化。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)