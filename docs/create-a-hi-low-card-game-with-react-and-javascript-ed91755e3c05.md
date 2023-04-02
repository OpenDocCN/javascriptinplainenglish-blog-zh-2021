# 用 React 和 JavaScript 创建一个高低牌游戏

> 原文：<https://javascript.plainenglish.io/create-a-hi-low-card-game-with-react-and-javascript-ed91755e3c05?source=collection_archive---------13----------------------->

![](img/5bb3b7976e0b6e6a169ed8eaf093beb8.png)

Photo by [Micheile Henderson](https://unsplash.com/@micheile?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个高低牌游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app hi-low-card-game
```

和 NPM 一起创建我们的 React 项目。

# 创建高低牌游戏

为了创建高低牌游戏，我们编写:

```
import React, { useEffect, useState } from "react";const suits = ["diamonds", "clubs", "hearts", "spades"];
const values = ["ace", 2, 3, 4, 5, 6, 7, 8, 9, 10];
const initCards = [];
for (const s of suits) {
  for (const v of values) {
    initCards.push(`${s}_${v}`);
  }
}export default function App() {
  const [score, setScore] = useState(0);
  const [cards, setCards] = useState(
    [...initCards].sort(() => Math.random() - 0.5)
  );
  const [drawnCards, setDrawnCards] = useState([]);
  const [guess, setGuess] = useState("lower"); const draw = (e) => {
    e.preventDefault();
    setCards((cards) => cards.slice(0, cards.length - 1));
    setDrawnCards((drawnCards) => [...drawnCards, cards[cards.length - 1]]);
  }; useEffect(() => {
    const indexLastCard = initCards.indexOf(drawnCards[drawnCards.length - 2]);
    const indexDrawnCard = initCards.indexOf(drawnCards[drawnCards.length - 1]); if (
      (indexLastCard < indexDrawnCard && guess === "higher") ||
      (indexLastCard > indexDrawnCard && guess === "lower")
    ) {
      setScore((score) => score + 1);
    }
  }, [drawnCards, guess, cards]); return (
    <div className="App">
      <form onSubmit={draw}>
        <select value={guess} onChange={(e) => setGuess(e.target.value)}>
          <option>lower</option>
          <option>higher</option>
        </select>
        <button type="submit">guess</button>
      </form>
      <p>score: {score}</p>
      <p>last drawn card</p>
      {drawnCards[drawnCards.length - 2] && (
        <img
          alt="last drawn card"
          src={`https://tekeye.uk/playing_cards/images/svg_playing_cards/fronts/${
            drawnCards[drawnCards.length - 2]
          }.svg`}
        />
      )} <p>currently drawrn card</p>
      {drawnCards[drawnCards.length - 1] && (
        <img
          alt="currently drawn card"
          src={`https://tekeye.uk/playing_cards/images/svg_playing_cards/fronts/${
            drawnCards[drawnCards.length - 1]
          }.svg`}
        />
      )}
    </div>
  );
}
```

我们有`suits`和`values`数组，它们用于创建包含所有卡片值的`initCards`数组。

然后我们定义`score`、`cards`、`drawnCartds`和`guess`状态。

`score`有玩家的分数。

`cards`有还没抽的牌。

`drawnCards`有抽到的牌。

`guess`有猜测值。

接下来，我们定义了`draw`函数。

在它内部，我们调用`e.preventDefault()`让我们进行客户端提交。

然后我们调用`setCards`来抽牌，通过调用`slice`从`cards`中去掉最后一个条目。

此外，我们通过传入一个回调函数来更新`drawnCards`状态，该回调函数返回一个数组，该数组包含现有的`drawnCards`条目和来自`cards`的最后一张卡片。

接下来，我们使用`useEffect`钩子获取存储在`indexLastCard`中的最后一张抽牌的索引。

并且我们还有当前抽卡的索引存储在`indexDrawnCard`中。

然后我们看`guess`值是否与上次抽的牌和当前抽的牌的大小比较匹配。

我们可以通过它们的索引进行比较，因为`initCards`按照从小到大的顺序排列卡片。

如果条件是`true`，那么我们调用`setScore`将分数递增 1。

接下来，我们用 select 下拉菜单定义表单，让我们选择 lower 或 high。

我们用`value`获取选定的值，并用`onChange`回调来设置该值。

`onSubmit`被设置为`submit`，所以当我们点击 guess 时我们运行它。

在那下面，我们显示`score`。

然后我们通过获取`drawnCards`的索引来显示最后抽的牌和当前抽的牌。

# 结论

因此，我们可以用 React 和 JavaScript 创建一个高低牌游戏。我希望这篇文章对你有用，感谢你的阅读。

*更多内容看*[*plain English . io*](http://plainenglish.io/)