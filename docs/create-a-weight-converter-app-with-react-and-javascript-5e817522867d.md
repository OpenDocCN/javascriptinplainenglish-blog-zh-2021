# 用 React 和 JavaScript 创建一个重量转换器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-weight-converter-app-with-react-and-javascript-5e817522867d?source=collection_archive---------15----------------------->

![](img/495f617b2c1ac7b95ac32146f1f10ab7.png)

Photo by [Victor Freitas](https://unsplash.com/@victorfreitas?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个重量转换器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app weight-converter
```

和 NPM 一起创建我们的 React 项目。

# 创建重量转换器应用程序

为了创建重量转换器应用程序，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [weightInLb, setWeightInLb] = useState(0);
  const [weightInKg, setWeightInKg] = useState(0); const calculate = (e) => {
    e.preventDefault();
    const formValid = +weightInLb >= 0;
    if (!formValid) {
      return;
    }
    setWeightInKg(+weightInLb * 0.453592);
  }; return (
    <div className="App">
      <form onSubmit={calculate}>
        <div>
          <label>weight in pounds</label>
          <input
            value={weightInLb}
            onChange={(e) => setWeightInLb(e.target.value)}
          />
        </div>
        <button type="submit">calculate</button>
      </form>
      <p>{weightInKg} kg</p>
    </div>
  );
}
```

我们用`useState`钩子定义了`weightInLb`和`weightInKg`状态。

然后我们定义了`calculate`函数来计算`weightInKg`值。

我们调用`e.preventDefault()`来做客户端表单提交。

然后我们检查`weightInLb`是否大于或等于 0。

如果是，那么我们计算`weightInKg`值，也就是`weightInLb`值转换成千克。

在 return 语句中，我们有一个表单，它有一个在提交事件被触发时运行`calculate`函数的`onSubmit`属性。

单击计算按钮触发提交事件。

表单中的输入有`value`属性来设置输入的值。

`onChange`具有获取输入值并调用`setWeightInLb`设置`weightInLb`值的功能。

`e.target.value`有输入值。

在表格下方，我们显示了`weightInKg`值。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个权重转换器。

*更多内容请看*[***plain English . io***](http://plainenglish.io)