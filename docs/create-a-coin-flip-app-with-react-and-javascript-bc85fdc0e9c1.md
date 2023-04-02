# 用 React 和 JavaScript 创建一个抛硬币应用程序

> 原文：<https://javascript.plainenglish.io/create-a-coin-flip-app-with-react-and-javascript-bc85fdc0e9c1?source=collection_archive---------12----------------------->

![](img/9a2b5260fe0bc7c0f5aa9cd223a4920b.png)

Photo by [Micheile Henderson](https://unsplash.com/@micheile?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个掷硬币应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app coin-flip
```

和 NPM 一起创建我们的 React 项目。

# 创建抛硬币应用程序

为了创建抛硬币应用程序，我们编写:

```
import React, { useMemo, useState } from "react";
const faces = ["heads", "tails"];export default function App() {
  const [selectedFace, setSelectedFace] = useState("");
  const [coinFlipResult, setCoinFlipResult] = useState(""); const flip = () => {
    let index;
    if (Math.random() < 0.5) {
      index = 0;
    } else {
      index = 1;
    }
    setCoinFlipResult(faces[index]);
  }; const computerSelectedFace = useMemo(() => {
    const face = faces.find((f) => f !== selectedFace);
    return face;
  }, [selectedFace]); const isWin = useMemo(() => {
    return coinFlipResult === selectedFace;
  }, [coinFlipResult, selectedFace]); const showResult = () => {
    if (isWin) {
      return <p>you win</p>;
    }
    return <p>you lost</p>;
  }; return (
    <div>
      <div>
        <h1>select a face</h1>
        <button onClick={() => setSelectedFace("heads")}>heads</button>
        <button onClick={() => setSelectedFace("tails")}>tails</button>
      </div>
      <p>you selected: {selectedFace}</p>
      <p>computer selected: {computerSelectedFace}</p>
      <button onClick={flip}>flip coin</button>
      {showResult()}
    </div>
  );
}
```

我们首先创建`faces`数组，其中有我们可以从中选择的`'heads'`和`'tails'`值。

然后我们定义`selectedFace`和`coinFlipResult`状态来分别设置选择的硬币正面和硬币翻转结果。

接下来，我们用`flip`函数来调用`setCoinFlipResult`来设置掷硬币的结果。

我们通过从`faces`数组中随机选取一个值来实现。

接下来，我们用`useMemo`钩子定义`computerSelectedFace`。

回调只是挑玩家没挑到的面。

我们观察`selectedFace`值来决定选择哪一个。

`isWin`变量检查`coinFlipResult`是否与`selectedFace`相同，以确定玩家是否获胜。

然后我们用`showResult`返回结果显示给玩家。

在那下面，我们有按钮，当我们点击它们时，让玩家选择正面或反面。

然后我们展示玩家和电脑选择了什么。

在那下面，我们有“抛硬币”按钮来选择硬币的正面。

下面我们调用`showResult`来显示结果。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个掷硬币游戏。

*更多内容请看*[***plain English . io***](http://plainenglish.io)