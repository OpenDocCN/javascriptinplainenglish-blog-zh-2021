# 用 React 和 JavaScript 创建一个猜数字游戏

> 原文：<https://javascript.plainenglish.io/create-a-guess-a-number-game-with-react-and-javascript-c1efd9e6cf24?source=collection_archive---------11----------------------->

![](img/07062b1e40a6412aed15c8eef12dc69e.png)

Photo by [Luigi Estuye, LUCREATIVE®](https://unsplash.com/@lucreative?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个猜数字游戏。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app guess-number-game
```

和 NPM 一起创建我们的 React 项目。

# 创建一个猜数字游戏

为了创建猜数字游戏，我们写道:

```
import React, { useState } from "react";export default function App() {
  const [started, setStarted] = useState(false);
  const [status, setStatus] = useState(false);
  const [answer, setAnswer] = useState(0);
  const [rightAnswer, setRightAnsweer] = useState(0);
  console.log(rightAnswer); const submit = (e) => {
    e.preventDefault();
    const formValid = +answer >= 0;
    if (!formValid) {
      return;
    }
    if (+answer === +rightAnswer) {
      setStatus("you got it");
      setStarted(false);
    } else if (+answer < +rightAnswer) {
      setStatus("too low");
    } else {
      setStatus("too high");
    }
  }; const start = () => {
    setRightAnsweer(Math.ceil(Math.random() * 10));
    setStarted(true);
  }; if (started) {
    return (
      <div>
        <form onSubmit={submit}>
          <div>
            <label>answer</label>
            <input value={answer} onChange={(e) => setAnswer(e.target.value)} />
          </div>
          <button type="submit">check</button>
        </form>
        <p>{status}</p>
      </div>
    );
  } else {
    return (
      <div>
        <button type="button" onClick={start}>
          start
        </button>
        <p>{status}</p>
      </div>
    );
  }
}
```

我们有`started`状态来设置渲染表单，让我们在游戏开始时输入一个数字。

`status`显示猜测是否正确。

`answer`显示了答案。

`rightAnswer`有正确答案。

接下来，我们有`submit`函数来检查我们输入的答案。

在其中，我们调用`e.preventDefault()`进行客户端表单提交。

然后我们检查`answer`是否大于或等于 0。

如果是，那么我们对照`rightAnswer`对其进行检查，并相应地设置`status`和`started`状态。

`start`功能用`setRightAnswer`设置`rightAnswer`。

`setStarted`设置`started`状态。

如果`started`是`true`，我们显示表单。

我们将`onSubmit`属性设置为`submit`，以便提交我们的`answer`。

`submit`是我们点击检查按钮时运行的，按钮类型为`submit`。

输入的值被设置为`answer`，我们用`onChange`回调来设置`answer`。

我们用`e.target.value`得到输入值。

在表格下面，我们展示了`status`。

如果`started`是`false`，我们显示开始按钮和`status`。

# 结论

我们可以用 React 和 JavaScript 创建一个猜数字游戏。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)