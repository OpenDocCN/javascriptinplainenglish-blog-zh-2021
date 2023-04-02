# 如何用 React 钩子把焦点放在下一次渲染上

> 原文：<https://javascript.plainenglish.io/how-to-focus-something-on-next-render-with-react-hooks-b8e0415f6c4a?source=collection_archive---------4----------------------->

![](img/b7eaa7eff7c10cde1e8ff33f6f696c7b.png)

Photo by [Johannes Plenio](https://unsplash.com/@jplenio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们可能希望在用 React 钩子创建的组件中的下一次渲染中关注一些东西。

在本文中，我们将研究如何在使用 React 钩子创建的组件中，在下一次呈现时关注某个元素。

# 用 React 钩子在下一次渲染时聚焦一些东西

为了在下一次渲染时关注某个元素，我们可以编写如下代码:

```
import { useEffect, useRef, useState } from "react";export default function App() {
  const [isEditing, setEditing] = useState(false);
  const toggleEditing = () => {
    setEditing(!isEditing);
  }; const inputRef = useRef(null); useEffect(() => {
    if (isEditing) {
      inputRef.current.focus();
    }
  }, [isEditing]); return (
    <div>
      {isEditing && <input ref={inputRef} />}
      <button onClick={toggleEditing}>edit</button>
    </div>
  );
}
```

我们用`useState`钩子创建了`isEditing`状态。

最初设置为`false`。

接下来，我们添加`toggleEditing`函数来调用`setEditing`函数到`isEditing`状态的否定值。

然后我们创建`inputRef` ref，让我们分配给下面的输入元素。

接下来，我们有一个在`isEditing`状态改变时运行的`useEffect`钩子。

我们检查`isEditing`值，如果是`true`，我们调用`inputRef.current.focus()`来关注输入。

第二个参数设置为`[isEditing]`，以便观察`isEditing`的值。

那么如果`isEditing`是`true`，我们就渲染输入。

在输入中，我们给它分配了一个`ref`。

我们有一个按钮，当我们点击编辑时，它运行`toggleEditing`功能。

# 结论

通过使用`useEffect`观察状态值，我们可以很容易地将注意力集中在下一次渲染的元素上。

然后，我们可以检查状态的值，并在元素对象上调用`focus`，这是我们分配给元素的 ref。

谢谢你，我希望这篇文章对你有用。

[*更多内容看 plainenglish.io*](https://www.mannmela.in/)