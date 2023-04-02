# 用 Vue 3 和 JavaScript 创建一个随机笑话应用

> 原文：<https://javascript.plainenglish.io/create-a-random-joke-app-with-vue-3-and-javascript-a522006ce7ad?source=collection_archive---------14----------------------->

![](img/9755ef4b2cbada134dcf954e90a3c552.png)

Photo by [Bret Kavanaugh](https://unsplash.com/@bretkavanaugh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个随机笑话应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app random-joke
```

和 NPM 一起创建我们的 React 项目。

# 创建随机笑话应用程序

为了创建随机笑话应用程序，我们编写:

```
import { useEffect, useState } from "react";export default function App() {
  const [joke, setJoke] = useState(""); const getJoke = async () => {
    const res = await fetch("https://api.chucknorris.io/jokes/random");
    const { value } = await res.json();
    setJoke(value);
  }; useEffect(() => {
    getJoke();
  }, []); return (
    <div className="App">
      <p>{joke}</p>
      <button onClick={getJoke}>get new joke</button>
    </div>
  );
}
```

我们有`joke`状态，它是由`useState`创建的字符串状态。

然后我们添加`getJoke`函数，用`fetch`向 Chuck Norris 笑话 API 发出 HTTP 请求。

我们发出一个 GET 请求，并调用`res.json()`用数据对象返回一个承诺。

然后我们调用`setJoke`来设置`joke` 值。

当我们加载组件时，我们用`useEffect`回调函数调用`getJoke`来加载笑话。

回调只在我们挂载它时运行，因为我们将一个空数组传入第二个组件。

然后我们渲染`joke`字符串。

然后我们添加了一个按钮，当我们点击它时，它会调用`getJoke`。

# 结论

我们可以使用 React 和 JavaScript 轻松创建一个随机笑话应用程序。

*更多内容请看*[***plain English . io***](http://plainenglish.io)