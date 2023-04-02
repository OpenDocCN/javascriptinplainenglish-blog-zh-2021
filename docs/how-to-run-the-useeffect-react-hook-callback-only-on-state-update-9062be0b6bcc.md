# 如何只在状态更新时运行 useEffect React 钩子回调？

> 原文：<https://javascript.plainenglish.io/how-to-run-the-useeffect-react-hook-callback-only-on-state-update-9062be0b6bcc?source=collection_archive---------11----------------------->

![](img/a479d761d5d2825ef480dfc7a126ce85.png)

Photo by [Magnet.me](https://unsplash.com/@magnetme?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

钩子让我们观察状态和道具的值，并根据它们的值做一些事情。

有时我们可能只想在状态值更新后运行`useEffect`回调。

在本文中，我们将看看如何仅在状态值更新时运行`useEffect`钩子回调。

# 仅在状态更新时运行 useEffect React 挂钩回调

为了只在状态更新时运行`useEffect`钩子回调，我们可以创建一个 ref 来跟踪状态更新的时间。

例如，我们可以写:

```
import { useEffect, useRef, useState } from "react";export default function App() {
  const isInitialMount = useRef(true);
  const [count, setCount] = useState(0); useEffect(() => {
    if (isInitialMount.current) {
      isInitialMount.current = false;
    } else {
      console.log(count);
    }
  }); return (
    <form>
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
    </form>
  );
}
```

我们用最初设置为`true`的`useRef`钩子创建`isInitialMount` ref。

然后我们创建了`count`状态，我们只希望在`count`更新时记录它。

在`useEffect`回调中，我们检查的是`isInitialMount.current`是`true`。

如果是`true`，那么我们将`initialMount.current`设置为`false`。

引用是非反应性的，因此不会导致组件的重新渲染。

然而,`current`值在渲染中持续存在。

当`isIninitialMount.current`为`false`时，我们记录`count`的值。

在那下面，我们有一个按钮，当我们点击它时，它调用`setCount`来更新`count`值。

现在，当我们单击增量按钮时，我们看到`count`从 1 开始记录，这意味着它的更新超过了初始值。

我们也可以将逻辑提取到它自己的钩子中。

例如，我们可以写:

```
import { useEffect, useRef, useState } from "react";const useUpdateEffect = (effect, dependencies = []) => {
  const isInitialMount = useRef(true); useEffect(() => {
    if (isInitialMount.current) {
      isInitialMount.current = false;
    } else {
      effect();
    }
  }, dependencies);
};export default function App() {
  const [count, setCount] = useState(0); useUpdateEffect(() => {
    console.log(count);
  }, [count]); return (
    <form>
      <button onClick={() => setCount((c) => c + 1)}>increment</button>
    </form>
  );
}
```

我们有接受`effect`函数的`useUpdateEffect`钩子，当`dependencies`数组中的任何内容发生变化时，我们希望运行这个钩子。

我们将`isInitialMount` ref 移动到钩子上。

并且我们在`useUpdateEffect`钩子中调用`useEffect`而不是`App`组件。

这让我们可以轻松地在任何地方重用逻辑。

# 结论

我们可以添加一个 ref 来跟踪一个组件何时被更新，当它更新时，运行我们想要的回调代码。

这让我们只在组件更新时运行`useEffect`回调。

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)