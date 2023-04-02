# 用 React 和 JavaScript 创建一个高度转换器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-height-converter-app-with-react-and-javascript-8e2c578a78f5?source=collection_archive---------13----------------------->

![](img/d07af1c7d35d056a300b7b1d5c093028.png)

Photo by [Vlad Busuioc](https://unsplash.com/@juvx?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个高度转换器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app height-converter
```

和 NPM 一起创建我们的 React 项目。

# 创建高度转换器应用程序

为了创建高度转换器应用程序，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [feet, setFeet] = useState(0);
  const [inches, setInches] = useState(0);
  const [centimeters, setCentimeters] = useState(0); const submit = (e) => {
    e.preventDefault();
    const formValid = +feet >= 0 && +inches >= 0;
    if (!formValid) {
      return;
    }
    setCentimeters((+feet + +inches / 12) * 12 * 2.54);
  }; return (
    <div>
      <form onSubmit={submit}>
        <div>
          <label>feet</label>
          <input value={feet} onChange={(e) => setFeet(e.target.value)} />
        </div>
        <div>
          <label>inches</label>
          <input value={inches} onChange={(e) => setInches(e.target.value)} />
        </div>
        <button type="submit">calculate</button>
      </form>
      <p>{centimeters} cm</p>
    </div>
  );
}
```

我们用`useState`钩子创建了`feet`、`inches`和`centimeters`状态。

然后我们定义`submit`函数从`feet`和`inches`计算出`centimeters`。

在其中，我们调用`e.preventDefault`进行客户端表单提交。

然后我们检查`feet`和`inches`是否是有效数字。

如果是，那么我们计算英尺和英寸的厘米当量，并调用`setCentimeters`来设置`centimeter`值。

在那下面，我们有表格。

当我们单击 calculate 按钮时，我们将`submit`函数传递给`onSubmit`钩子来触发提交。

这些输入用于设置`feet`和`inches`。

`onChange`设置为一个函数来设置每个值。

`e.target.value`有输入值。

在那下面，我们显示`centimeters`值。

# 结论

我们可以使用 React 和 JavaScript 轻松创建一个高度转换器应用程序。

*更多内容请看*[***plain English . io***](http://plainenglish.io)