# 如何用 React useEffect 钩子比较旧值和新值？

> 原文：<https://javascript.plainenglish.io/how-to-compare-old-values-and-new-values-with-the-react-useeffect-hook-5a3385e5fc8b?source=collection_archive---------12----------------------->

![](img/1921c5ca61d5ad9dcd5c3435b3a73f68.png)

Photo by [Efe Kurnaz](https://unsplash.com/@efekurnaz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要比较用 React 钩子创建的 React 组件中状态的新旧值。

在本文中，我们将研究如何比较用 React 钩子创建的组件的新旧状态值。

# 在 Ref 中存储旧值

我们可以将旧值存储在 ref 中，因为给它们赋值不会触发组件的重新渲染，但该值会在每次渲染循环后保持不变。

因此，我们可以这样写:

```
import React, { useEffect, useRef, useState } from "react";const usePrevious = (value) => {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  });
  return ref.current;
};export default function App() {
  const [count, setCount] = useState(0);
  const prevCount = usePrevious(count);
  useEffect(() => {
    console.log("prevCount: ", prevCount, "count: ", count);
  }, [prevCount, count]); return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
      <p>{count}</p>
    </div>
  );
}
```

创建`usePrevious`钩子来存储状态的前一个值。

钩子接受带有我们想要存储的状态或属性值的`value`参数。

我们用一个回调函数调用`useEffect`来设置`ref`的`current`属性，以在其中存储`value`。

我们没有传入第二个参数，所以`useEffect`回调将在每个渲染周期运行。

我们返回`ref.current`的值，这样我们可以将它赋给组件中的一个值并使用它。

在`App`中，我们用`useState`钩子创建了`count`状态。

我们用`count`调用`usePrevious`钩子将`count`的前一个值存储在`ref`中，

接下来，我们通过将`prevCount`和`count`作为第二个参数传入一个数组，用`useEffect`钩子观察`prevCount`和`count`的值。

然后在那下面，我们有一个按钮，当我们点击它来更新`count`时，它会调用`setCount`。

然后我们展示了`count`。

在控制台日志中，我们应该看到`prevCount`应该具有`count`的先前值。

# 结论

我们可以通过将值存储在 ref 中来存储状态或属性的旧值，这样我们就可以在组件中使用它。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)