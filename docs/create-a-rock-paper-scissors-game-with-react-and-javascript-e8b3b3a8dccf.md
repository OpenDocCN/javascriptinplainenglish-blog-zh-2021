# 用 React 和 JavaScript 创建一个石头剪刀布游戏

> 原文：<https://javascript.plainenglish.io/create-a-rock-paper-scissors-game-with-react-and-javascript-e8b3b3a8dccf?source=collection_archive---------15----------------------->

![](img/e8184c86fc2d01a411013f707dc443f7.png)

Photo by [Ben Karpinski](https://unsplash.com/@benkarpinski?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个石头剪刀布游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app rock-paper-scissors
```

和 NPM 一起创建我们的 React 项目。

# 创建石头剪刀布游戏

为了创建石头剪子布游戏，我们编写:

```
import React, { useMemo, useState } from "react";
const choices = ["rock", "paper", "scissors"];export default function App() {
  const [selected, setSelected] = useState("");
  const [computedSelected, setComputedSelected] = useState(""); const play = () => {
    if (!selected) {
      return;
    }
    const computerChoiceIndex = Math.floor(Math.random() * choices.length);
    setComputedSelected(choices[computerChoiceIndex]);
  }; const result = useMemo(() => {
    if (computedSelected === selected) {
      return `it's a tie`;
    } else {
      if (
        (computedSelected === "rock" && selected === "scissors") ||
        (computedSelected === "paper" && selected === "rock") ||
        (computedSelected === "scissors" && selected === "paper")
      ) {
        return "computer won";
      }
      return "player won";
    }
  }, [computedSelected, selected]); return (
    <div>
      <div>
        <button onClick={() => setSelected("rock")}>rock</button>
        <button onClick={() => setSelected("paper")}>paper</button>
        <button onClick={() => setSelected("scissors")}>scissors</button>
      </div>
      <button onClick={play}>play</button>
      <p>your choice: {selected}</p>
      <p>computer's choice: {computedSelected}</p>
      <div>{result}</div>
    </div>
  );
}
```

我们用可供选择的选项来定义`choices`数组。

然后我们定义`selected`状态来持有玩家的选择。

我们定义`computedSelected`状态来保存计算机的选择。

接下来，我们定义`play`函数让计算机选择选项。

我们用随机选择来调用`setComputedSelected`来设置计算机的选择。

然后我们用`useMemo`钩子定义`result`变量，得到`compyterSelected`和`selected`值，检查谁赢了。

如果值相同，那么它是一个平局。

不然石头打剪刀，布打石头，剪刀打布。

我们传递我们正在观察的所有值来计算第二个参数中的`result`。

之后。我们添加按钮让玩家设置`selected`值。

下面，我们显示播放按钮，当我们点击它时运行`play`。

然后我们显示玩家和电脑的选择。

最后，我们显示`result`。

# 结论

我们可以用 React 和 JavaScript 创建一个石头剪子布游戏。

*更多内容请看*[***plain English . io***](http://plainenglish.io)