# 如何修复 React useState 钩子不设置初始值的问题？

> 原文：<https://javascript.plainenglish.io/how-to-fix-the-react-usestate-hook-not-setting-initial-value-problem-7def65b44362?source=collection_archive---------2----------------------->

![](img/3abc4dd4f37c83e0319c83d1f9ad3973.png)

Photo by [Dalal Nizam](https://unsplash.com/@dilson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`useState`钩子让我们在 React 组件中创建状态变量。

它需要一个参数作为状态的初始值。

有时候，我们可能想从道具中设置一个状态的初始值。

我们想在 prop 值改变时更新初始值。

在本文中，我们将看看如何用最新的属性值来修复 React `useState`钩子。

# 当 Prop 更新时更新状态

为了在道具更新时更新状态，我们必须用`useEffect`钩子来观察道具值。

然后在`useEffect`回调中，我们可以调用 state setter 函数用道具的值更新状态值。

例如，我们可以写:

```
import React, { useEffect, useState } from "react";const Count = ({ count }) => {
  const [num, setNum] = useState(count); useEffect(() => {
    setNum(count);
  }, [count]); return <p>{num}</p>;
};export default function App() {
  const [count, setCount] = useState(0); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <Count count={count} />
    </div>
  );
}
```

在`Count`组件中，我们有一个带有`count`值的`useState`钩子作为参数。

这最初将`num`设置为`count`。

然后我们有一个`useEffect`钩子，它通过将值传递给第二个参数中的数组来监视`count`值。

然后在回调中，我们调用`setNum`来更新`num`值，并在该值下面的返回语句中呈现该值。

在`App`中，我们用`useState`钩子创建了`count`状态。

然后，我们在按钮的`onClick`处理程序中调用`setCount`，更新`count`状态的值。

我们将`count`值作为`Count`组件中`count`道具的值进行传递。

现在，当我们点击增量按钮时，我们看到`num`值更新，并显示其最新值。

# 结论

我们可以通过用`useEffect`钩子观察属性的值，然后用属性的值作为参数调用`useEffect`回调中的 state setter 函数，确保 React 组件状态在属性的值改变时更新。