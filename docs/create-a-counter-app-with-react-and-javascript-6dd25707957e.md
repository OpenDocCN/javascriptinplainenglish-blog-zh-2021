# 用 React 和 JavaScript 创建计数器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-counter-app-with-react-and-javascript-6dd25707957e?source=collection_archive---------14----------------------->

![](img/07df73729465113aa3b0f61d1ba9c9d9.png)

Photo by [Bruce Tang](https://unsplash.com/@brucetml?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个计数器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app counter
```

和 NPM 一起创建我们的 React 项目。

# 创建计数器应用程序

为了创建计数器应用程序，我们编写:

```
import { useState } from "react";export default function App() {
  const [count, setCount] = useState(0); const increment = () => {
    setCount((c) => c + 1);
  }; const decrement = () => {
    setCount((c) => c - 1);
  }; return (
    <div className="App">
      <button onClick={increment}>increment</button>
      <button onClick={decrement}>decrement</button>
      <p>{count}</p>
    </div>
  );
}
```

我们有由`useState`钩子创建的`count`状态。

我们将初始值设置为 0。

然后我们用`increment`和`decrement`函数分别将`count`增加和减少 1。

我们传入一个函数，该函数将当前的`count`状态值作为参数，并在`setCount`回调中返回新值。

然后我们有按钮，当我们点击它们时分别调用`increment`和`decrement`。

我们显示`count`作为我们点击的结果。

# 结论

我们可以用 React 和 JavaScript 创建一个计数器应用程序。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)