# 用 React 和 JavaScript 创建一个气球弹出游戏

> 原文：<https://javascript.plainenglish.io/create-a-balloon-popping-game-with-react-and-javascript-b4b877862613?source=collection_archive---------11----------------------->

![](img/b95000d1dbd80b5d56af84d2249d91b1.png)

Photo by [Aaron Burden](https://unsplash.com/@aaronburden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个气球弹出游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app balloon-popping-game
```

和 NPM 一起创建我们的 React 项目。

# 创建气球弹出游戏

为了创建弹出气球游戏，我们编写:

```
import React, { useState } from "react";const colors = ["red", "green", "blue"];const generateColor = () => {
  const index = Math.floor(Math.random() * colors.length);
  return colors[index];
};const balloonArr = Array(25)
  .fill()
  .map((_, i) => ({ id: i, popped: false, color: generateColor() }));export default function App() {
  const [balloons, setBalloons] = useState(balloonArr); const onPop = (index) => {
    setBalloons((balloons) => {
      const b = [...balloons];
      b[index].popped = true;
      return b;
    });
  }; return (
    <div className="App">
      <style>
        {`
        .balloon-container {
          display: inline-block;
        }

        .balloon {
          width: 50px;
          height: 50px;
          border-radius: 50%;
          border: 1px solid black;
        }
      `}
      </style>
      <div>
        {balloons.map((b, i) => {
          if (!b.popped) {
            return (
              <div className="balloon-container" key={b.id}>
                <div
                  className="balloon"
                  style={{ backgroundColor: b.color }}
                  onMouseOver={() => onPop(i)}
                ></div>
              </div>
            );
          } else {
            return <div className="balloon-container">popped</div>;
          }
        })}
      </div>
    </div>
  );
}
```

我们有带有气球颜色的`colors`数组。

`generateColor`从`colors`数组中随机选取一种颜色。

然后我们有了`balloonArr`数组，它有 25 个对象和渲染气球的数据。

包括是不是`popped`，还有`color`。

在`App`中，我们有初始设置为`balloonArr`的`balloons`状态。

`onPop`函数让我们将`balloons`条目的`index`属性设置为`true`。

我们有一个回调来获取`balloons`，然后我们制作一个副本，修改它，然后返回修改后的副本。

接下来，我们有使气球在线显示的样式。

`ballon`类通过将`border-radius`设置为`50%`使 div 显示为圆形。

最后，我们通过调用`map`来渲染`balloons`。

在`map`回调中，我们检查`b.popped`是否为`false`。

如果是`false`，那么我们用 div 渲染气球。

我们将`styles`和`onMouseOver`属性设置为调用`onPop`函数的函数，通过将`popped`设置为`true`来弹出气球。

否则，我们呈现“弹出”的文本。

# 结论

因此，我们可以用 React 和 JavaScript 创建一个气球弹出游戏。希望这篇文章对你有用。感谢阅读。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)