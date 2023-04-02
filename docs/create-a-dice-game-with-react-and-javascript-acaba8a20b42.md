# 用 React 和 JavaScript 创建一个骰子游戏

> 原文：<https://javascript.plainenglish.io/create-a-dice-game-with-react-and-javascript-acaba8a20b42?source=collection_archive---------19----------------------->

![](img/6870f5692668f55fe007603e09a322bb.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个骰子游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app dice-game
```

和 NPM 一起创建我们的 React 项目。

# 创建骰子游戏

为了创建骰子游戏，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [rolledValue, setRolledValue] = useState(1); const roll = () => {
    setRolledValue(Math.ceil(Math.random() * 5 + 1));
  }; return (
    <div>
      <button onClick={roll}>roll</button>
      <p>rolled dice value: {rolledValue}</p>
    </div>
  );
}
```

我们有`rolledValue`状态，它包含掷骰子的值。

然后我们创建`roll`函数，将`rolledValue`状态设置为一个随机数。

由于`Math.random`只返回一个 0 到 1 之间的数字，我们必须将返回值乘以 5，再加 1，以生成一个 1 到 6 之间的随机数。

在那下面，我们有一个按钮，当我们点击它时，它会调用`roll`。

下面是我们展示的`rolledValue`。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个骰子游戏。

*更多内容请看*[***plain English . io***](http://plainenglish.io)