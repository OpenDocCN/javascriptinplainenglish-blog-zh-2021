# 用 React 和 JavaScript 创建联系人表单

> 原文：<https://javascript.plainenglish.io/create-a-contact-form-with-react-and-javascript-42f364938daa?source=collection_archive---------15----------------------->

![](img/4ea2e56a01c37afd6afb39b0bb92e69f.png)

Photo by [Miles Burke](https://unsplash.com/@milesb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将了解如何使用 React 和 JavaScript 创建联系人表单。

# 创建项目

我们可以用 Create React App 创建 React 项目。

为了安装它，我们运行…

```
npx create-react-app contact-form
```

…与 NPM 一起创建我们的 React 项目。

# 创建联系人表单应用程序

为了创建联系人表单应用程序，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState(""); const submit = (e) => {
    e.preventDefault();
    const formValid =
      name.length > 0 &&
      /(.+)@(.+){2,}.(.+){2,}/.test(email) &&
      message.length > 0;
    if (!formValid) {
      return;
    }
    if (!localStorage.getItem("messages")) {
      localStorage.setItem("messages", JSON.stringify([]));
    }
    const messages = JSON.parse(localStorage.getItem("messages"));
    messages.push({
      name,
      email,
      message
    });
    localStorage.setItem("messages", JSON.stringify(messages));
  }; const onReset = () => {
    setName("");
    setEmail("");
    setMessage("");
  }; return (
    <div className="App">
      <form onSubmit={submit} onReset={onReset}>
        <div>
          <label>name</label>
          <input value={name} onChange={(e) => setName(e.target.value)} />
        </div> <div>
          <label>email</label>
          <input
            value={email}
            onChange={(e) => setEmail(e.target.value)}
          />
        </div> <div>
          <label>message</label>
          <textarea
            value={message}
            onChange={(e) => setMessage(e.target.value)}
          ></textarea>
        </div> <button type="submit">submit</button>
        <button type="reset">reset</button>
      </form>
    </div>
  );
}
```

我们用`useState`钩子创建了`name`、`email`和`message`状态。

然后我们创建`submit`函数让用户提交联系表单。

在其中，我们调用`e.preventDefault()`让我们进行客户端表单提交。

然后我们检查输入的值是否有效。

然后我们检查带有关键字`messages`的本地存储条目是否存在。

如果它不存在，那么我们用`message`键添加一个新条目。

然后，我们向 JSON 数组添加一个新条目，并将关键字`message`放入本地存储。

我们用`JSON.parse`解析 JSON 数组字符串。

然后我们对解析后的数组调用`push`。

然后我们调用`setItem`来保存更新后的数组。

接下来，我们定义`onReset`函数将所有状态值设置为空字符串。

然后我们添加一个带有输入的表单。

`value` prop 具有从状态输入的值。

并且到达输入的`onChange`属性被设置为获取输入值并将它们设置为各种状态的值的函数。

当我们点击提交按钮时，就会触发`onSubmit`道具。

`onReset`在我们点击复位按钮时被触发。

# 结论

我们可以使用 React 和 JavaScript 轻松创建联系人表单。希望这篇文章对您有所帮助，感谢您的阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)