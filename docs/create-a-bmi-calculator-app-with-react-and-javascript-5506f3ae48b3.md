# 用 React 和 JavaScript 创建一个身体质量指数计算器应用

> 原文：<https://javascript.plainenglish.io/create-a-bmi-calculator-app-with-react-and-javascript-5506f3ae48b3?source=collection_archive---------14----------------------->

![](img/3fe9b922fa7e6c8e26759d2a2163525b.png)

Photo by [Philippe Bout](https://unsplash.com/@flipboo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个身体质量指数计算器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app bmi-calculator
```

和 NPM 一起创建我们的 React 项目。

# 创建身体质量指数计算器应用程序

为了创建身体质量指数计算器应用程序，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [height, setHeight] = useState(0);
  const [mass, setMass] = useState(0);
  const [bmi, setBmi] = useState(0); const calculate = (e) => {
    e.preventDefault();
    const formValid = +height > 0 && +mass > 0;
    if (!formValid) {
      return;
    }
    const bmi = +mass / (+height) ** 2;
    setBmi(bmi);
  }; return (
    <div className="App">
      <form onSubmit={calculate}>
        <div>
          <label>height in meters</label>
          <input value={height} onChange={(e) => setHeight(e.target.value)} />
        </div> <div>
          <label>mass in kg</label>
          <input value={mass} onChange={(e) => setMass(e.target.value)} />
        </div> <button type="submit">calculate</button>
      </form>
      <p>bmi: {bmi}</p>
    </div>
  );
}
```

首先，我们用`useState`钩子定义了`height`、`mass`和`bmi`状态。

然后，我们用`calculate`函数从`height`和`mass`中计算出`bmi`。

在其中，我们调用`e.preventDefault()`进行客户端表单提交。

然后我们检查`height`和`mass`是否是有效值。

如果是，那么我们计算`bmi`并调用`setBmi`来设置身体质量指数值。

然后我们返回一个表单，将`onSubmit`属性设置为`calculate`。

当我们点击计算按钮时，它就运行了。

此外，我们有 2 个输入，它们接受输入值并分别设置为值`height`和`mass`。

`e.target.value`有输入值。

在表单下方，我们显示了`bmi`。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个身体质量指数计算器。

*更多内容看* [***说白了***](http://plainenglish.io)