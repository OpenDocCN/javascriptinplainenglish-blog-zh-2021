# 如何用 React 钩子处理输入？

> 原文：<https://javascript.plainenglish.io/how-to-handle-an-input-with-react-hooks-9a071f57ce1c?source=collection_archive---------14----------------------->

![](img/955c1e2d0a9ddf0985d18a93b84ed3c2.png)

Photo by [Anton Maksimov juvnsky](https://unsplash.com/@juvnsky?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

处理输入值是我们在 React 组件中经常要做的事情。

在本文中，我们将看看如何用 React 钩子处理输入。

# 使用 useState 挂钩

为了使输入值在 React 组件中可用，我们必须将输入值设置为状态值。

为此，我们可以使用`useState`钩子。

例如，我们可以写:

```
import React from "react";export default function App() {
  const [inputValue, setInputValue] = React.useState(""); const onChangeHandler = (event) => {
    setInputValue(event.target.value);
  }; return (
    <div>
      <input
        type="text"
        name="name"
        onChange={onChangeHandler}
        value={inputValue}
      />
      <p>{inputValue}</p>
    </div>
  );
}
```

我们调用`useState`钩子返回一个带有`inputValue`状态的数组，调用`setInputValue`函数设置`inputValue`状态。

然后我们用调用`setInputValue`来设置`inputValue`状态的`event`参数来定义`onChangeHandler`函数。

`event.target.value`有输入值。

然后我们添加一个输入元素，并将`onChangeHandler`事件处理程序和`inputValue`状态分别传入`onChange`和`value`道具。

然后我们展示一下`inputValue`。

我们将`value`属性设置为`inputValue`，这样我们就可以看到我们在输入中输入了什么。

如果我们经常使用输入，我们可能还想把输入逻辑放在一个钩子中:

```
import React, { useState } from "react";const useInput = ({ type }) => {
  const [value, setValue] = useState("");
  const input = (
    <input
      value={value}
      onChange={(e) => setValue(e.target.value)}
      type={type}
    />
  );
  return [value, input];
};export default function App() {
  const [username, userInput] = useInput({ type: "text" }); return (
    <div>
      {userInput}
      <p>{username}</p>
    </div>
  );
}
```

我们创建了一个`useInput`钩子，它接受一个带有属性的对象，这样我们就可以设置输入类型。

然后我们调用`App`中的`useInput`来使用。

我们将`userInput`组件放在 div 和`username`中，后者有输入值。

钩子的逻辑和我们之前的一样。

因此，当我们键入输入内容时，我们会看到呈现的输入值。

# 结论

我们可以通过调用带有输入值的状态设置函数来处理输入值，这样我们就可以在组件中使用输入值。