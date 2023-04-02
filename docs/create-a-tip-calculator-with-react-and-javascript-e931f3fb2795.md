# 用 React 和 JavaScript 创建一个小费计算器

> 原文：<https://javascript.plainenglish.io/create-a-tip-calculator-with-react-and-javascript-e931f3fb2795?source=collection_archive---------18----------------------->

![](img/18e1df62d68e82cba939d36921da0a05.png)

Photo by [Sam Dan Truong](https://unsplash.com/@sam_truong?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建小费计算器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app tip-calculator
```

和 NPM 一起创建我们的 React 项目。

# 创建小费计算器应用程序

为了创建小费计算器应用程序，我们编写:

```
import { useState } from "react";export default function App() {
  const [subtotal, setSubtotal] = useState(0);
  const [numDiners, setNumDiners] = useState(0);
  const [tipPercentage, setTipPercetnage] = useState(0);
  const [result, setResult] = useState({}); const submit = (e) => {
    e.preventDefault();
    if (+subtotal <= 0 || +numDiners <= 0 || +tipPercentage <= 0) {
      return;
    }
    const total = +subtotal * (1 + +tipPercentage);
    setResult({ total, totalPerDiner: +total / +numDiners });
  }; return (
    <div className="App">
      <form onSubmit={submit}>
        <fieldset>
          <label>subtotal</label>
          <input
            value={subtotal}
            onChange={(e) => setSubtotal(e.target.value)}
          />
        </fieldset> <fieldset>
          <label>number of people sharing the bill</label>
          <input
            value={numDiners}
            onChange={(e) => setNumDiners(e.target.value)}
          />
        </fieldset> <fieldset>
          <label>tip percentage</label>
          <select
            value={tipPercentage}
            onChange={(e) => setTipPercetnage(e.target.value)}
          >
            <option value="0">0%</option>
            <option value="0.05">5%</option>
            <option value="0.1">10%</option>
            <option value="0.15">15%</option>
            <option value="0.2">20%</option>
          </select>
        </fieldset> <button type="submit">Calculate</button>
      </form>
      <p>total: {result.total && result.total.toFixed(2)}</p>
      <p>
        total per diner:{" "}
        {result.totalPerDiner && result.totalPerDiner.toFixed(2)}
      </p>
    </div>
  );
}
```

我们有`subtotal`、`numDiners`、`tipPercentage`和`result`状态。

`subtotal`是小计。

`numDiners`是用餐人数。

`tipPercentage`具有 0 到 100 之间的小费百分比。

在`submit`函数中，我们调用`e.preventDefault()`来阻止服务器端表单提交。

然后我们用`if`块检查这些值是否有效。

然后我们计算`total`和结果对象，并调用`setResult`来设置它。

在`return`语句中，我们用带有`value`和`onChange`属性的输入字段分别获取和设置值。

我们从`e.target.value`得到值。

表单有`onSubmit`属性来设置提交事件监听器。

在那下面，我们显示了`result`数据。

# 结论

我们可以用 React 和 JavaScript 创建一个小费计算器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)