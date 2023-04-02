# 使用 React 和 JavaScript 创建小费计算器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-tip-calculator-app-with-react-and-javascript-4093153a8aa?source=collection_archive---------18----------------------->

![](img/1661f0b5ece3c5edb9b402e70100300b.png)

DFPhoto by [Alex Iby](https://unsplash.com/@alexiby?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个小费计算器应用程序。

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
import React, { useState } from "react";export default function App() {
  const [percentageTip, setPercentageTip] = useState(0);
  const [billAmount, setBillAmount] = useState(0);
  const [tipAmount, setTipAmount] = useState(0);
  const [total, setTotal] = useState(0); const calculate = (e) => {
    e.preventDefault();
    const formValid = +billAmount > 0 && +percentageTip > 0;
    if (!formValid) {
      return;
    }
    const tipAmount = +billAmount * (+percentageTip / 100);
    const total = +billAmount * (1 + percentageTip / 100);
    setTipAmount(tipAmount);
    setTotal(total);
  }; return (
    <div className="App">
      <form onSubmit={calculate}>
        <div>
          <label>bill amount</label>
          <input
            value={billAmount}
            onChange={(e) => setBillAmount(e.target.value)}
          />
        </div>
        <div>
          <label>percentage tip</label>
          <input
            value={percentageTip}
            onChange={(e) => setPercentageTip(e.target.value)}
          />
        </div>
        <button type="submit">calculate</button>
      </form>
      <p>tip amount: {tipAmount.toFixed(2)}</p>
      <p>total: {total.toFixed(2)}</p>
    </div>
  );
}
```

在`App`组件中，我们有`percentageTip`、`billAmount`、`tipAmount`和`total`状态。

我们用`useState`挂钩创建它们。

然后我们定义`calculate`函数。

我们调用`e.preventDefault()`来完成客户端表单提交。

然后我们检查`billAmoubnt`和`percentageTip`看它们是否是有效值。

如果是，那么我们计算`tipAmount`和`total`。

我们调用`setTipAmount`和`setTotal`来设置这些值。

在此之下，我们将表单元素的`onSubmit`属性设置为`calculate`，这样当我们单击 calculate 按钮时它就会运行。

在表单中，我们有输入，让我们输入帐单金额和百分比小费。

`value`有来自各州的值。

我们用传递给`onChange` prop 的函数来设置状态。

`e.target.value`获取输入值。

在那下面，我们显示`tipAmount`和`total`。

`toFixed`让我们把数字四舍五入到给定的小数位数。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个小费计算器。

*更多内容请看*[***plain English . io***](http://plainenglish.io)