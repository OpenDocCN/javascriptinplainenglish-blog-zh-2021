# 使用 React 和 JavaScript 创建绘图应用程序

> 原文：<https://javascript.plainenglish.io/create-a-drawing-app-with-react-and-javascript-9325cff905f5?source=collection_archive---------18----------------------->

![](img/7962c9fff395f3026557357aee180c0b.png)

Photo by [Victoria Bilsborough](https://unsplash.com/@vicbils?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个绘图应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app drawing-app
```

和 NPM 一起创建我们的 React 项目。

# 创建绘图应用程序

为了创建绘图应用程序，我们编写:

```
import React, { useEffect, useRef, useState } from "react";export default function App() {
  const canvas = useRef();
  const [pos, setPos] = useState({}); const setPosition = (e) => {
    setPos({
      x: e.clientX,
      y: e.clientY
    });
  }; const resize = () => {
    const ctx = canvas.current.getContext("2d");
    ctx.canvas.width = window.innerWidth;
    ctx.canvas.height = window.innerHeight;
  }; const draw = (e) => {
    if (e.buttons !== 1) {
      return;
    }
    const ctx = canvas.current.getContext("2d");
    ctx.beginPath();
    ctx.lineWidth = 5;
    ctx.lineCap = "round";
    ctx.strokeStyle = "green";
    ctx.moveTo(pos.x, pos.y);
    setPosition(e);
    ctx.lineTo(pos.x, pos.y);
    ctx.stroke();
  }; useEffect(() => {
    window.addEventListener("resize", resize);
    return () => window.removeEventListener("resize", resize);
  }, []); return (
    <div>
      <style>
        {`
          #canvas {
            border: 1px solid black;
          }
        `}
      </style>
      <canvas
        ref={canvas}
        onMouseMove={draw}
        onMouseDown={setPosition}
        onMouseEnter={setPosition}
        id="canvas"
      ></canvas>
    </div>
  );
}
```

我们创建了`canvas` ref，它将被分配给 canvas 元素。

然后我们定义`pos`状态来设置画布指针的位置。

然后我们定义了`setPosition`函数，它从`clientX`和`clientY`事件属性值中设置`pos`状态值。

接下来，我们定义获取画布的`resize`函数，然后在调整窗口大小时设置画布的宽度和高度。

之后，我们定义`draw`函数来画线。

我们用事件对象获取`e`参数。

首先，我们通过检查`e.buttons`是否为 1 来检查我们是否点击了左边的按钮。

只有当`e.buttons`为 1 时，我们才继续。

接下来，我们得到画布元素对象。

然后我们调用`beginPath`开始画图。

我们设置线条宽度、线帽样式和笔画样式。

然后我们调用`moveTo`将指针移动到给定位置。

然后我们调用`setPosition`将`pos`的值设置为相同的值。

并且我们用直线的终点坐标再次调用`lineTo`来设置直线的终点坐标。

然后我们调用`ctx.stroke`来画线。

然后我们添加带有回调函数的`useEffect`钩子，当我们调整窗口大小时，回调函数会调整画布的大小。

在此之下，我们添加了样式元素来为画布添加边框。

最后，我们添加画布并分配当我们单击并移动鼠标时运行的事件处理程序。

# 结论

我们可以使用 React 和 JavaScript 轻松创建一个绘图应用程序。

*更多内容请看*[***plain English . io***](http://plainenglish.io)