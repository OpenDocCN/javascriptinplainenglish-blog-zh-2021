# 如何让 React useState 钩子 Setter 函数立即反映变化

> 原文：<https://javascript.plainenglish.io/how-to-make-the-react-usestate-hook-setter-function-reflect-changes-immediately-2780deda7d3b?source=collection_archive---------6----------------------->

![](img/5d70816a7d23a3b26fba70a306e0877e.png)

Photo by [Bill Stephan](https://unsplash.com/@billstephan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能会看到我们用`useState` hook 的状态设置函数所做的状态改变并没有在我们期望的时间反映出来。

在本文中，我们将看看如何让 React `useState`钩子的状态设置函数在我们需要时得到反映。

# 正确使用 useState 状态设置器函数

为了确保我们在运行了`usetState`状态设置器函数后选择了状态的最新变化，我们应该用`useEffect`钩子观察状态的最新值。

例如，我们可以写:

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

我们调用`useState`钩子返回`setCount`函数来设置状态。

我们用一个回调函数调用`setCount`,这个回调函数获取之前的状态值，并基于这个值返回新的状态值。

当`count`的值改变时`useEffect`回调运行。

所以我们可以看到在`useEffect`回调中记录的`count`的最新值。

当我们点击增量按钮时，我们显示`count`的值。

我们必须使用`useEffect`钩子来观察状态值，因为 React 的`useState`状态设置函数是异步的。

我们作为`useEffect`的第二个参数传入的数组具有我们想要观察的状态或属性值。

因此，我们无法在调用`setCount`函数后立即获取`count`的值。

state setter 函数将在被调用时触发重新渲染。

并且`count`的最新值将在下一次渲染后可用。

# 结论

为了获得状态的最新值并对其进行处理，我们必须使用带有回调的`useEffect`钩子和我们想要观察的值的数组。

然后在`useEffect`回调中，我们得到我们正在观察的任何东西的最新值。

*更多内容请看*[***plain English . io***](http://plainenglish.io)