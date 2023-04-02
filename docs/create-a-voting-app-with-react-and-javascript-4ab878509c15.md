# 用 React 和 JavaScript 创建一个投票应用

> 原文：<https://javascript.plainenglish.io/create-a-voting-app-with-react-and-javascript-4ab878509c15?source=collection_archive---------15----------------------->

![](img/49b25b6753b626c224795d3445dda69b.png)

Photo by [Glen Carrie](https://unsplash.com/@glencarrie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将了解如何使用 React 和 JavaScript 创建投票应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app voting-app
```

和 NPM 一起创建我们的 React 项目。

# 创建投票应用程序

为了创建投票应用程序，我们编写:

```
import React, { useState, useEffect } from "react";export default function App() {
  const [choice, setChoice] = useState("");
  const [results, setResults] = useState({}); const vote = () => {
    if (!localStorage.getItem("vote-result")) {
      localStorage.setItem("vote-result", JSON.stringify({}));
    }
    setResults({ ...results, [choice]: (results[choice] ?? 0) + 1 });
  }; useEffect(() => {
    localStorage.setItem("vote-result", JSON.stringify(results));
  }, [results]); return (
    <div>
      <form>
        <div>
          <label>What's your favorite fruit?</label>
          <input
            type="radio"
            value="apple"
            checked={"apple" === choice}
            onChange={(e) => setChoice(e.target.value)}
          />
          apple
          <input
            type="radio"
            value="orange"
            checked={"orange" === choice}
            onChange={(e) => setChoice(e.target.value)}
          />
          orange
          <input
            type="radio"
            value="grape"
            checked={"grape" === choice}
            onChange={(e) => setChoice(e.target.value)}
          />
          grape
        </div>
        <button type="button" onClick={vote}>
          vote
        </button>
      </form>
      <div>
        <h1>result</h1>
        {Object.entries(results).map(([key, val]) => {
          return (
            <p key={key}>
              {key}: {val}
            </p>
          );
        })}
      </div>
    </div>
  );
}
```

我们创建了存储用户选择的选项的`choice`状态。

然后我们定义存储投票结果的`results`状态。

接下来，我们定义用键`vote-result`获取本地存储项的`vote`函数。

如果没有设置，那么我们添加它。

接下来，我们用`setResults`设置`results`状态。

我们制作了一个`results`的副本，然后将`choices`添加到其中。

`??`是 nullish 合并操作符，仅当`results[choice]`未设置或者为`undefined`时返回 0。

然后我们加 1 来登记投票。

接下来，我们用一个回调函数调用`useEffect`，该回调函数调用`localStorage.setItem`将最新的`result`值存储在本地存储中。

在此之下，我们定义一个包含问题和选项的表单。

我们有单选按钮输入。

我们将它们设置为不同的值，并设置`checked`值，以便在我们做出选择时检查它们。

并且在`onChange`回调中，我们用`e.target.value`调用`setChoice`来将`choice`设置为所选的值。

当我们点击投票按钮时，我们调用`vote`。

在表单下方，我们向用户显示了`results`。

`Object.entries`返回一个数组中对象的键和值的数组。

数组条目是键和值的数组。

# 结论

我们可以使用 React 和 JavaScript 轻松创建投票应用程序。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)