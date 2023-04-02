# 用 React 和 JavaScript 创建一个番茄定时器

> 原文：<https://javascript.plainenglish.io/create-a-pomodoro-timer-with-react-and-javascript-dead941b1fec?source=collection_archive---------7----------------------->

![](img/0befc1c469cfcb10517d91d73c887d2b.png)

Photo by [NeONBRAND](https://unsplash.com/@neonbrand?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个番茄定时器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app pomodoro-timer
```

和 NPM 一起创建我们的 React 项目。

# 创建番茄定时器应用程序

为了创建番茄定时器应用程序，我们编写:

```
import React, { useEffect, useState } from "react";export default function App() {
  const [secondsLeft, setSecondsLeft] = useState(25 * 60);
  const [timer, setTimer] = useState(); const start = () => {
    const timer = setInterval(() => {
      setSecondsLeft((secondsLeft) => secondsLeft - 1);
      if (secondsLeft === 0) {
        clearInterval(timer);
      }
    }, 1000);
    setTimer(timer);
  }; useEffect(() => {
    if (secondsLeft === 0) {
      clearInterval(timer);
    }
  }, [secondsLeft, timer]); useEffect(() => {
    return () => clearInterval(timer);
  }, [timer]); return (
    <div className="App">
      <h1>Pomodoro Timer</h1>
      <button onClick={start}>start</button>
      <div>{secondsLeft} seconds left</div>
    </div>
  );
}
```

我们将设置为`25 * 60`秒的`secondsLeft`状态定义为初始值。

同样，我们将设置为`undefined`的`timer`状态定义为初始值。

`start`功能通过`setInterval`功能创建一个定时器。

回调通过将状态减 1 来设置`secondsLeft`状态。

如果`secondsLeft`为 0，那么我们调用`clearInterval`来清除定时器。

我们每秒运行一次`setIntrval`回调。

同样，当`secondsLeft`为 0 时，我们有第一个`useEffect`通过调用`clearInterval`来停止计时器。

第二个`useEffect`回调函数返回一个调用`clearInterval`的函数，以便在我们卸载组件时清除计时器。

在那下面，我们有一个按钮，当我们点击它的时候启动计时器。

在那下面，我们向用户显示`secondsLeft`。

# 结论

我们可以用 React 和 JavaScript 很容易地创建一个番茄定时器。

*更多内容请看*[***plain English . io***](http://plainenglish.io)