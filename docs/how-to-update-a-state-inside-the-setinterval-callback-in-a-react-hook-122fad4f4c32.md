# 如何在 React 钩子中更新 setInterval 回调内部的状态？

> 原文：<https://javascript.plainenglish.io/how-to-update-a-state-inside-the-setinterval-callback-in-a-react-hook-122fad4f4c32?source=collection_archive---------2----------------------->

![](img/9f59d206421c137da69c22d640012134.png)

Photo by [Julian Hochgesang](https://unsplash.com/@julianhochgesang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`setInterval`函数让我们定期运行 JavaScript 应用程序中的代码。

我们有时可能会在 React 组件中使用它来用新值定期更新状态。

在本文中，我们将看看如何在 React 钩子中更新`setInterval`回调中的状态。

# 在 React 组件中运行 setInterval

要在 React 组件中运行`setInterval`，我们应该把它放在`useEffect`钩子中。

`useEffect`钩子用于提交副作用，包括创建定时器。

因此，我们可以这样写:

```
import React, { useEffect, useState } from "react";export default function App() {
  const [gamePlayTime, setGamePlayTime] = useState(0); useEffect(() => {
    const gameStartInternal = setInterval(() => {
      setGamePlayTime((t) => t + 1);
    }, 1000); return () => {
      clearInterval(gameStartInternal);
    };
  }, []); return <div>{gamePlayTime}</div>;
}
```

我们有通过调用`setGamePlayTime`来更新的`gamePlayTime`状态。

接下来，我们用回调函数调用`useEffect`，并通过调用`setInterval`在回调函数中创建计时器。

我们将 1000 作为第二个参数传入，这样`setInterval`回调只运行 1000 毫秒。

它返回一个定时器 ID，这样我们可以在组件卸载时调用它的`clearInterval`。

我们在回调中做到了这一点，我们在`useEffect`回调中返回。

我们返回的回调是在卸载组件时运行的。

我们将一个空数组传入第二个参数，这样当组件挂载时，`useEffect`回调只运行一次。

这样，我们就不会多次创建计时器。

然后在下面，我们显示`gamePlayTime`。

现在我们应该看到屏幕上的`gamePlayTime`值每秒更新一次，并显示最新值。

# 结论

我们只是在`useEffect`回调中调用`setInterval`来创建计时器。

当我们卸载组件时，我们在回调函数中调用`clearInterval`来清除它。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)