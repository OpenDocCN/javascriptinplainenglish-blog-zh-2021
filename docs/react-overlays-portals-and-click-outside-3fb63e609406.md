# 反应-覆盖-门户和点击外部

> 原文：<https://javascript.plainenglish.io/react-overlays-portals-and-click-outside-3fb63e609406?source=collection_archive---------14----------------------->

![](img/6ad9c900ea50e0c7a8b39ebd861ba00a.png)

Photo by [Victor Garcia](https://unsplash.com/@victor_g?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

叠加是我们必须经常添加到 React 应用程序中的东西。

为了使这项任务更容易，我们可以使用现有的组件库来添加它们。

在本文中，我们将了解如何使用 react-overlays 库在 React 应用程序中添加门户和点击外部功能。

# 入口

我们可以使用`Portal`组件让我们在 DOM 中我们想要的位置呈现内容。

例如，我们可以这样使用它:

```
import React, { useRef, useState } from "react";
import Portal from "react-overlays/Portal";export default function App() {
  const [show, setShow] = useState(false);
  const containerRef = useRef(null); let child = <span>But I actually render here!</span>; return (
    <div className="flex flex-col items-center">
      <button type="button" className="btn" onClick={() => setShow(true)}>
        Render Child
      </button>
      <div className="bg-brand-200 p-6 rounded-lg shadow my-4">
        <Portal container={containerRef}>{show && child}</Portal>
      </div>
      <div className="bg-brand-200 p-6 rounded-lg shadow " ref={containerRef} />
    </div>
  );
}
```

我们添加按钮来切换`show`状态，以显示门户的内容。

`Portal`组件有`containerRef`为门户设置容器。

这是让我们在`containerRef`的位置呈现门户内容。

# useRootClose 挂钩

当我们点击组件外部时,`useRootClose`钩子可以让组件消失。

为了使用它，我们写:

```
import React, { useRef, useState } from "react";
import { useRootClose } from "react-overlays";export default function App() {
  const ref = useRef();
  const [show, setShow] = useState(false);
  const handleRootClose = () => setShow(false); useRootClose(ref, handleRootClose, {
    disabled: !show
  }); return (
    <div className="flex flex-col items-center">
      <button type="button" className="btn" onClick={() => setShow(true)}>
        Show
      </button> {show && (
        <div ref={ref} className="rounded shadow bg-white p-6">
          <span>Click anywhere to dismiss</span>
        </div>
      )}
    </div>
  );
}
```

我们通过将`show`设置为`true`来添加显示 div 的按钮。

然后我们添加一个 div，当`show`为`true`时显示。

我们将 ref 传递给 div，为它分配 ref。

然后我们将引用传递给 th `useRootClose`钩子，让我们通过用`handleRootClose`函数将`show`设置为`false`来移除容器。

我们设置了`disabled`属性，使其在`show`为`false`时被禁用。

# 结论

我们可以添加`Portal`组件，让我们将元素添加到 DOM 中我们想要的任何地方。

当我们点击钩子之外的时候,`useRootClose`钩子允许我们移除组件。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)