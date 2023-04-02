# 用 React 和 JavaScript 创建一个记忆游戏

> 原文：<https://javascript.plainenglish.io/create-a-memory-game-with-react-and-javascript-793d27ad7bf6?source=collection_archive---------20----------------------->

![](img/33a71df727f921aba5d1a3b77bfdae07.png)

Photo by [Soragrit Wongsa](https://unsplash.com/@invictar1997?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个内存游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app memory-game
```

和 NPM 一起创建我们的 React 项目。

# 创造记忆游戏

为了创建记忆游戏，我们写道:

```
import React, { useEffect, useState } from "react";
import { v4 as uuidv4 } from "uuid";
const answerArr = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5]
  .map((n) => {
    return {
      id: uuidv4(),
      open: false,
      value: n
    };
  })
  .sort(() => Math.random() - 0.5);export default function App() {
  const [answer, setAnswer] = useState([...answerArr]);
  const [itemIds, setItemIds] = useState([]); const onClick = (id) => {
    if (!itemIds.includes(id)) {
      setItemIds((itemIds) => [...itemIds, id]);
    }
    const index = answer.findIndex((a) => a.id === id);
    setAnswer((answer) => {
      const ans = [...answer];
      ans[index].open = true;
      return ans;
    });
  }; useEffect(() => {
    if (itemIds.length === 2) {
      const item1Index = answer.findIndex((a) => a.id === itemIds[0]);
      const item2Index = answer.findIndex((a) => a.id === itemIds[1]);
      if (answer[item1Index].value !== answer[item2Index].value) {
        setAnswer((answer) => {
          const ans = [...answer];
          ans[item1Index].open = false;
          ans[item2Index].open = false;
          return ans;
        });
      }
    }
  }, [itemIds, answer]); useEffect(() => {
    if (itemIds.length === 2) {
      setItemIds([]);
    }
  }, [itemIds]); return (
    <div>
      <style>
        {`
          .container {
            display: flex;
          }.tile {
            border: 1px solid black;
            width: 20vw;
            height: 50px;
          }
          `}
      </style>
      <div className="container">
        {answer.map((a) => {
          return (
            <div key={a.id} className="tile" onClick={() => onClick(a.id)}>
              {a.open ? <div>{a.value}</div> : <div>&nbsp;</div>}
            </div>
          );
        })}
      </div>
    </div>
  );
}
```

我们有一个`answerArr`数组，它是一个随机的数字数组。

它用于渲染玩家可以通过点击打开的盒子。

如果两个号码匹配，那么他们保持开放。

否则，两者都关闭。

然后我们用答案定义`answer`状态。

`itemIds`有打开的答题卡的 id。

最多可以打开 2 个。

接下来，我们定义检查`itemIds`是否包含`id`的`onClick`。

如果没有，我们用`setItemIds`将它添加到`itemIds`数组中。

然后我们调用`setAnswer`将`answer`中应该打开的`open`属性中的项目设置为`true`。

接下来，我们有一个`useEffect`回调来检查`itemIds.length`是否为 2。

如果是，那么我们调用`findIndex`来获取我们点击的`answer`项的索引。

如果它们的`value`不匹配，那么我们通过将两个项目的`open`属性设置为`false`来关闭它们。

我们观察`itemIds`和`answer`的值来相应地进行更新。

我们还有另一个`useEffect`钩子来再次检查`itemIds.length`是否为 2，但是这一次，如果是`true`，当我们将`itemIds`设置为空数组时。

接下来，我们在`style`标签中添加卡片的样式。

然后我们将`answers`项渲染成 div。

我们显示的值是`a.open`是`true`。

否则，我们显示一个空框。

# 结论

我们可以用 React 和 JavaScript 创建一个记忆游戏。

*更多内容请看*[***plain English . io***](http://plainenglish.io)