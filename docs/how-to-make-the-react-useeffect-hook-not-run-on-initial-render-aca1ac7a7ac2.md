# 如何让 React useEffect 钩子在初始渲染时不运行？

> 原文：<https://javascript.plainenglish.io/how-to-make-the-react-useeffect-hook-not-run-on-initial-render-aca1ac7a7ac2?source=collection_archive---------9----------------------->

![](img/acabb7883cc88472fd285b478ec0ba78.png)

Photo by [Daniel DiNuzzo](https://unsplash.com/@ddinuzzo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想让我们的`useEffect`回调在初始渲染时不运行。

在本文中，我们将看看如何让 React `useEffect`回调在初始渲染时不运行。

# 将呈现状态存储在 Ref 中

我们可以在运行我们想要的代码之前创建一个钩子来检查第一次渲染是否已经完成。

为此，我们写道:

```
import React, { useEffect, useRef, useState } from "react";const useDidMountEffect = (func, deps) => {
  const didMount = useRef(false); useEffect(() => {
    if (didMount.current) {
      func();
    } else {
      didMount.current = true;
    }
  }, deps);
};export default function App() {
  const [count, setCount] = useState(0); useDidMountEffect(() => {
    console.log("second render");
  }); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <p>{count}</p>
    </div>
  );
}
```

我们创建了`useDidMountEffect`钩子来跟踪第一次渲染是否完成。

我们用`didMount` ref 来做这件事。

当`deps`数组改变时，我们有运行的`useEffect`钩子。

如果是第一次渲染，我们将`didMount.current`设置为`true`。

否则，我们运行`func`函数。

在`App`中，我们有`count`状态，当我们点击增量按钮时，它被更新。

我们还向我们创建的`useDidMountEffect`钩子传递一个回调。

当我们点击增量按钮时，我们看到第一次渲染后记录的`'second render'`。

# 结论

我们可以通过创建一个跟踪第一次渲染是否完成的 ref 来使 React `useEffect`回调不在第一次渲染时运行。

然后我们可以检查 ref 的值，看看第一次渲染什么时候完成，并在第一次渲染完成时运行我们想要的函数。