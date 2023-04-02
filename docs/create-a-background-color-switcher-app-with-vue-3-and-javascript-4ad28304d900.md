# 用 React 和 JavaScript 创建一个背景颜色切换器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-background-color-switcher-app-with-vue-3-and-javascript-4ad28304d900?source=collection_archive---------14----------------------->

![](img/ba92941e0306dc77b68db91f13154ba8.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个背景颜色切换器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app background-color-switcher
```

和 NPM 一起创建我们的 React 项目。

# 创建背景颜色切换器应用程序

为了创建背景颜色切换器应用程序，我们编写:

```
import React, { useState } from "react";
const colors = ["red", "green", "blue", "yellow"];export default function App() {
  const [backgroundColor, setBackgroundColor] = useState(""); return (
    <div
      className="App"
      style={{
        backgroundColor
      }}
    >
      <style>
        {`
        .circle {
          border-radius: 50%;
          width: 50px;
          height: 50px;
          border: 1px solid black;
          display: inline-block;
          cursor: pointer;
        } #screen {
          width: 100vw;
          height: 100vh;
        }
      `}
      </style>
      {colors.map((c) => {
        return (
          <div
            key={c}
            style={{
              backgroundColor: c
            }}
            class="circle"
            onClick={() => setBackgroundColor(c)}
          ></div>
        );
      })}
    </div>
  );
}
```

我们有一个`colors`数组，里面有我们可以切换到的颜色。

在`App`中，我们有`backgroundColor`状态，用于设置包装器 div 的背景颜色。

`style`标签有圆形的样式，这是我们在`map`回调中返回的 div。

我们可以通过设置`border-radius`为 50%来做一个圆。

此外，我们设置`border`使圆的边缘出现。

我们将`cursor`设置为`pointer`，这样当我们悬停在圆圈上方时就能看到一只手。

在`colors.map`回调中，我们返回一个 div，它的`style`和`backgroundColor`被设置为`colors`数组中的颜色`c`。

我们有一个`onClick`监听器，它调用`setBackgroundColor`来设置颜色。

# 结论

我们可以用 React 和 JavaScript 添加一个背景色切换器。希望这篇文章对你有用，感谢你的阅读！

[*更多内容尽在 plainenglish.io*](http://plainenglish.io/)