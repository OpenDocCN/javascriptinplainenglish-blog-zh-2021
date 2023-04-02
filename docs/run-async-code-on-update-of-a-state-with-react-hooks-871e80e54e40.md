# 使用 React 挂钩在状态更新时运行异步代码

> 原文：<https://javascript.plainenglish.io/run-async-code-on-update-of-a-state-with-react-hooks-871e80e54e40?source=collection_archive---------16----------------------->

![](img/d1e852717efe5574cb8c0cc7ad99d14e.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在基于类的 React 组件中，我们可以向第二个参数`setState`传递回调，以便在用`setState`更新状态时运行代码。

有了 React 钩子，我们不再有`setState`方法。

相反，我们使用用`useState`钩子创建的状态更新函数来更新状态。

这意味着我们必须在状态更新后找到新的方法来运行代码。

在本文中，我们将研究如何在用 React 钩子创建的函数组件中更新状态后运行异步代码。

# 使用效果挂钩

`useEffect`钩子让我们在组件代码中产生副作用。

我们可以提交副作用来响应一个或多个状态的变化。

为了指定要监视哪个状态，我们将一个我们想要监视的状态数组传递给第二个参数`useEffect`。

然后在我们传入第一个参数的`useEffect`回调中，我们可以在第二个参数的状态改变时运行代码，因为第一个参数中的回调将在第二个参数的状态改变时运行。

例如，我们可以写:

```
import React, { useEffect, useState } from "react";export default function App() {
  const [loading, setLoading] = useState(false);
  const [loading2, setLoading2] = useState(false); useEffect(() => {
    setTimeout(() => setLoading(true), 1000);
  }, []); useEffect(() => {
    if (loading) {
      setTimeout(() => setLoading2(true), 1000);
    }
  }, [loading]); return (
    <>
      <div>{loading.toString()}</div>
      <div>{loading2.toString()}</div>
    </>
  );
}
```

我们有两个状态，`loading`和`loading2`，我们在`useEffect`回调中更新了它们。

在第一个`useEffect`回调中，我们用一个回调来调用`setTimeout`，这个回调在 1000 毫秒后调用`setLoading`来将`loading`设置为`true`。

第二个参数中的空数组意味着`useEffect`回调只在组件被挂载时运行。

接下来，我们用获得`loading`值的回调再次调用`useEffect`。

在回调中，我们检查`loading`是否为`true`，

如果是，那么我们调用`setTimeout`并回调`setLoading2`以在 1000 毫秒后将`loading2`设置为`true`。

在第二个参数中，我们有一个状态为`loading`的数组。

这意味着每当`loading`状态改变时，`useEffect`回调就会运行。

这意味着`useEffect`允许我们在状态更新时运行代码。

在 JSX，我们渲染每个州的值。

我们应该看到它们一个接一个地出现。

# 结论

我们可以在状态改变后运行异步代码，方法是调用`useEffect`钩子，通过将我们想要监视的状态传递到`useEffect`的第二个参数中的数组来监视状态的值。

然后我们可以根据`useEffect`回调中的值变化运行代码。

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)