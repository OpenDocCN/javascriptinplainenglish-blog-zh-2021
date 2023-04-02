# 如何使用钩子检测 React 组件外部的点击？

> 原文：<https://javascript.plainenglish.io/how-to-detect-clicks-outside-a-react-component-using-hooks-dc8050331b77?source=collection_archive---------5----------------------->

![](img/79f671c47479d733411b0bd640a95e27.png)

Photo by [Idella Maeland](https://unsplash.com/@idellamaeland?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望检测 React 组件外部的单击，例如我们希望创建一个弹出菜单，当我们在外部单击时它会关闭。

在本文中，我们将研究如何用钩子检测 React 组件外部的点击。

# 监听页面上的点击

我们可以监听页面上的点击来检测我们点击了页面的哪个位置。

如果我们在组件外部单击，那么我们就从 DOM 中移除 React 组件。

检查我们点击的位置并相应地运行代码称为事件委托。

例如，我们可以写:

```
import React, { useEffect, useRef, useState } from "react";const useComponentVisible = (initialIsVisible) => {
  const [isComponentVisible, setIsComponentVisible] = useState(
    initialIsVisible
  );
  const ref = useRef(null); const handleClickOutside = (event) => {
    if (ref.current && !ref.current.contains(event.target)) {
      setIsComponentVisible(false);
    }
  }; useEffect(() => {
    document.addEventListener("click", handleClickOutside, true);
    return () => {
      document.removeEventListener("click", handleClickOutside, true);
    };
  });return { ref, isComponentVisible, setIsComponentVisible };
}; const DropDown = () => {
  const { ref, isComponentVisible } = useComponentVisible(true); return <div ref={ref}>{isComponentVisible && <p>drop down</p>}</div>;
};export default function App() {
  return (
    <div>
      <DropDown />
    </div>
  );
}
```

我们创建了`useComponentVisible`钩子来观察页面上的点击。

我们首先定义`isComponentVisible`状态来跟踪组件何时应该可见。

我们将它设置为`initialVisible`的适当值。

然后我们定义一个`ref`，当我们点击外部时，它被分配给我们想要关闭的组件。

我们在`handleClickOutside`函数中做元素检查。

这时我们调用`contains`来检查我们点击的元素是否在组件之外。

如果`!ref.current.contains(event.target)`是`true`，那么我们知道我们点击了组件外部。

接下来，我们调用`document.addEventListener`来监听整个页面上的点击，这样我们就可以进行上面的检查。

当我们卸载组件时，我们返回一个调用`removeEventListener`来删除事件监听器的回调。

接下来，我们将`DropDown`组件定义为获取我们返回的 ref 和`isComponentVisible`状态。

然后，我们将 ref 分配给 div，因此我们使用 click 事件侦听器来进行比较。

最后，我们将`DropDown`组件添加到`App`中，这样我们就可以看到它了。

现在，当我们在文本外单击时，文本应该会消失。

# 结论

我们可以检测 React 组件外部的点击，方法是当我们在组件外部点击时，给我们想要关闭的组件分配一个 ref。

然后我们可以将一个事件处理程序附加到`document`上，并检查我们是否在被分配了 ref 的元素之外单击了鼠标。