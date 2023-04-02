# 用 React 和 JavaScript 创建一个加法游戏

> 原文：<https://javascript.plainenglish.io/create-an-addition-game-with-react-and-javascript-648b693b390b?source=collection_archive---------13----------------------->

![](img/f92ff84bc921ee750e0aebb39f21edff.png)

Photo by [Mesut Kaya](https://unsplash.com/@directormesut?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个加法游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app addition-game
```

和 NPM 一起创建我们的 React 项目。

# 创建加法游戏

为了创建加法游戏，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [num1, setNum1] = useState(0);
  const [num2, setNum2] = useState(0);
  const [sum, setSum] = useState(0);
  const [score, setScore] = useState(0); const generateQuestion = () => {
    setNum1(Math.ceil(Math.random() * 10));
    setNum2(Math.ceil(Math.random() * 10));
  }; const submit = (e) => {
    e.preventDefault();
    const formValid = +sum >= 0;
    if (!formValid) {
      return;
    }
    if (+num1 + +num2 === +sum) {
      setScore((score) => score + 1);
    }
    generateQuestion();
  }; return (
    <div className="App">
      <form onSubmit={submit}>
        <div>
          <label>
            {num1} + {num2}
          </label>
          <input value={sum} onChange={(e) => setSum(e.target.value)} />
        </div> <button type="submit">check</button>
      </form>
      <button type="button" onClick={generateQuestion}>
        start game
      </button>
      <p>score: {score}</p>
    </div>
  );
}
```

我们用`useState`钩子创建了`num1`、`num2`、`sum`和`score`状态。

`num1`和`num2`是加法题的部分。

`sum`有我们输入的总和。

`score`已得分。

在此之下，我们用`generateQuestion`函数来生成`num1`和`num2`值。

我们打电话

`setNum1`和`setNum2`进行设置。

`Math.random`创建一个介于 0 和 1 之间的随机数。

`Math.ceil`向上舍入到最接近的整数。

然后我们有了`submit`函数，它根据`num1`和`num2`的和来检查`sum`的值。

在我们进行检查之前，我们调用`e.preventDefault()`，这样我们就可以进行客户端提交。

然后我们检查`sum`是否是一个大于或等于 0 的数字。

如果是的话，我们就做检查。

如果答案与总和匹配，那么我们用`setScore`增加分数。

我们通过传递一个返回原始的`score`加 1 的回调来增加它。

然后我们再次调用`generateQuestion`生成下一个问题。

在那下面，我们有一个带有`onSubmit`属性的表单。

`onSubmit`点击检查按钮时运行。

在表单中，我们显示了`num1`和`num2`。

我们有一个接受`sum`值的输入，我们通过在`onChange`回调中调用`setSum`来设置`sum`。

`e.target.value`有输入值。

在那下面，我们有开始游戏按钮，当我们点击它时会调用`generateQuestion`。

最后，我们展示下面的`score`。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个加法游戏。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)