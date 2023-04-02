# 如何将 setState 回调与 React 挂钩一起使用？

> 原文：<https://javascript.plainenglish.io/how-to-use-the-setstate-callback-with-react-hooks-fa5c875888f9?source=collection_archive---------15----------------------->

![](img/36f2bdfa519d648bafe37c9dee4bd877.png)

Photo by [Fabien Bazanegue](https://unsplash.com/@fbazanegue?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我们使用基于类的组件时，我们可以传入一个回调函数作为`setState`方法的第二个参数，以便在状态更新后运行代码。

因为我们转而使用钩子来创建组件，所以我们必须使用`useState`钩子来创建和更新状态。

状态设置函数不接受回调作为第二个参数来让我们在状态更新后运行代码。

因此，我们必须在一个状态更新后找到一种新的方式来运行代码。

在本文中，我们将研究如何在状态更新后运行代码。

# 使用 useEffect 挂钩

为了在状态更新后运行代码，我们可以使用`useEffect`钩子来观察状态的值并相应地运行代码。

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

用`useEffect`钩子观察`count`状态的值。

我们将`count`传递给第二个参数中的数组来观察它的值。

现在，当我们单击 increment 按钮来更新`count`时，`useEffect`回调将会运行。

同样的事情也适用于道具，因为它们也会触发组件的重新渲染。

# 结论

为了在一个状态改变后运行代码，我们可以使用`useEffect`钩子和一个状态数组或者我们想要监视其变化的属性。

然后，当数组中的任何值改变时，`useEffect`回调将运行。

*更多内容请看*[***plain English . io***](http://plainenglish.io)