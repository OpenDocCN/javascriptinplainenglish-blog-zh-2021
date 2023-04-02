# 用 React 和 JavaScript 创建一个点击形状游戏

> 原文：<https://javascript.plainenglish.io/create-a-click-shape-game-with-react-and-javascript-c4fa18698081?source=collection_archive---------10----------------------->

![](img/70d9dd28f439bd89a55a217a6af8c1b6.png)

Photo by [Anna Bakirova](https://unsplash.com/@nejumimi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个点击形状游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app click-shape-game
```

和 NPM 一起创建我们的 React 项目。

# 创建点击形状游戏

为了创建点击形状游戏，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [score, setScore] = useState(0);
  const [circleX, setCircleX] = useState();
  const [circleY, setCircleY] = useState();
  const [timer, setTimer] = useState(); const onClick = () => {
    setScore((s) => s + 1);
  }; const start = () => {
    const timer = setInterval(() => {
      setCircleX(Math.floor(Math.random() * window.innerWidth));
      setCircleY(Math.floor(Math.random() * (window.innerHeight - 50) + 50));
    }, 2000);
    setTimer(timer);
  }; const end = () => {
    clearInterval(timer);
    setScore(0);
    setCircleX(undefined);
    setCircleY(undefined);
  }; return (
    <div className="App">
      <style>
        {`
        .circle {
          border: 1px solid black;
          width: 50px;
          height: 50px;
          border-radius: 50%;
        }
        `}
      </style>
      <button onClick={start}>start game</button>
      <button onClick={end}>end game</button>
      <p>score: {score}</p>
      {circleX && circleY && (
        <div
          className="circle"
          style={{
            position: "absolute",
            top: `${circleY}px`,
            left: `${circleX}px`
          }}
          onClick={onClick}
        >
          &nbsp;
        </div>
      )}
    </div>
  );
}
```

我们有`score`、`circleX`、`circleY`和`timer`状态。

`score`有玩家的分数。

`circleX`和`circleY`有圆圈左上角的 x 和 y 坐标。

`timer`有一个计时器，运行该计时器可以让我们将`circleX`和`circleY`设置为随机数，让我们在随机位置显示圆。

接下来，我们定义`onClick`函数来增加分数。

`start`调用`setInterval`运行定时器，每 2 秒设置一次`circleX`和`circleY`。

我们调用`setTimer`来设置`timer`，以便稍后我们调用`clearInterval`来结束游戏。

`end`函数调用`clearInterval`清除定时器并将所有其他状态重置为初始值。

在那下面，我们有了`style`标签来使`circle`类有了`border-radius`属性来使一个 div 变成一个圆。

当我们点击按钮时，按钮让我们开始或结束游戏。

然后我们在下面显示`score`。

然后我们通过将`circleX`和`circleY`设置为`top`和`left`的值来显示圆。

我们将`onClick`函数传递给`onClick`道具，让我们在点击一个圆时增加分数。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个点击形状游戏。

*更多内容请看*[***plain English . io***](http://plainenglish.io)