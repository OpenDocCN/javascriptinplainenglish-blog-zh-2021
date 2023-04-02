# 用 React 和 JavaScript 创建工具提示

> 原文：<https://javascript.plainenglish.io/create-a-tooltip-with-react-and-javascript-16a7e7fe7979?source=collection_archive---------14----------------------->

![](img/d6abd0de998497fed56f150a9f6306dd.png)

Photo by [Sam Dan Truong](https://unsplash.com/@sam_truong?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建工具提示。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app tooltip
```

和 NPM 一起创建我们的 React 项目。

# 创建工具提示

为了创建工具提示，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [show, setShow] = useState(false);
  const [clientX, setClientX] = useState(0);
  const [clientY, setClientY] = useState(0); const onHover = (e) => {
    const { clientX, clientY } = e;
    setShow(true);
    setClientX(clientX);
    setClientY(clientY);
  }; return (
    <div className="App">
      <style>
        {`
          #container {
            width: 95vw;
            height: 95vh;
            align-items: center;
            display: flex;
            justify-content: center;
          }

          #tooltip {
            border: 1px solid black;
            padding: 5px;
            position: absolute;
            background-color: white;
          }
          `}
      </style>
      <button onMouseOver={onHover}>hover me</button>
      {show && (
        <div
          id="tooltip"
          style={{ top: `${clientY}px`, left: `${clientX}px` }}
          onMouseOut={() => setShow(false)}
        >
          tooltip
        </div>
      )}
    </div>
  );
}
```

我们有`show`、`clientX`和`clientY`状态，让我们分别设置是否显示工具提示及其位置。

接下来，我们定义`onHover`函数。

它从鼠标事件对象中获取`clientX`和`clientY`值。

然后调用`setShow`显示工具提示。

并且`setClientX`和`setClientY`设置工具提示的位置。

接下来，我们为工具提示添加样式。

我们设置它的位置`absolute`，这样它就可以显示在其他项目之上。

当我们将鼠标悬停在上面时,“悬停我”按钮会运行`onHover`。

如果`show`是`true`，我们就显示工具提示 div。

我们将`style`道具设置为带有`top`和`left`位置的对象，以设置工具提示位置。

`onMouseOut`设置为用`false`调用`setShow`的函数，隐藏工具提示。

# 结论

我们可以使用 React 和 JavaScript 轻松创建工具提示。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)