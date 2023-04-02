# 用 React 和 JavaScript 创建一个传递消息的应用程序

> 原文：<https://javascript.plainenglish.io/create-a-pass-the-message-app-with-react-and-javascript-5fe50acd8a30?source=collection_archive---------20----------------------->

![](img/931072514ca787700cb44f1130a13071.png)

Photo by [Adam Jang](https://unsplash.com/@adamjang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个传递消息应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app pass-the-message
```

和 NPM 一起创建我们的 React 项目。

# 创建传递消息应用程序

为了创建传递消息应用程序，我们编写:

```
import { useState } from "react";export default function App() {
  const [message, setMessage] = useState("");
  const [prevMessage, setPrevMessage] = useState(""); const pass = (e) => {
    e.preventDefault();
    if (!message) {
      return;
    }
    setPrevMessage(message);
    setMessage("");
  }; return (
    <div className="App">
      <form onSubmit={pass}>
        <label>message you like to pass</label>
        <input value={message} onChange={(e) => setMessage(e.target.value)} />
        <button type="submit">submit</button>
      </form>
      <h1>last message delivered</h1>
      <p>{prevMessage}</p>
    </div>
  );
}
```

我们有`message`和`prevMessage`两种状态。

`pass`函数让我们将`prevMessage`设置为`message`，并将`message`设置为空字符串。

我们调用`e.preventDefault()`,这样我们可以进行客户端表单提交。

然后，我们在继续之前检查`message`是否已设置。

在`form`元素中，我们将`pass`函数传递给`onSubmit`属性，以便在单击提交按钮时调用它。

此外，我们有一个输入字段，通过将`value`设置为`message`并将`onChange`属性绑定到一个调用`setMessage`来设置`message`值的函数，我们将该字段绑定到`message`状态。

在那下面，我们显示`prevMessage`。

# 结论

我们可以用 React 和 JavaScript 创建一个传递消息的应用程序。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)