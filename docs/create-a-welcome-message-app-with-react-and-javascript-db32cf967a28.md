# 用 React 和 JavaScript 创建一个欢迎消息应用程序

> 原文：<https://javascript.plainenglish.io/create-a-welcome-message-app-with-react-and-javascript-db32cf967a28?source=collection_archive---------10----------------------->

![](img/dc2ce5e19c9d66a83690a98e9f357f5f.png)

Photo by [Corinne Kutz](https://unsplash.com/@corinnekutz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个欢迎消息应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app welcome-message
```

和 NPM 一起创建我们的 React 项目。

# 创建欢迎消息应用程序

为了创建欢迎消息应用程序，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [firstName, setFirstName] = useState("");
  const [lastName, setLastName] = useState("");
  const [message, setMessages] = useState(""); const submit = (e) => {
    e.preventDefault();
    const formValid = firstName.length > 0 && lastName.length > 0;
    if (!formValid) {
      return;
    }
    setMessages(`hello, ${firstName} ${lastName}`);
  }; return (
    <div>
      <form onSubmit={submit}>
        <div>
          <label>first name</label>
          <input
            value={firstName}
            onChange={(e) => setFirstName(e.target.value)}
          />
        </div>
        <div>
          <label>last name</label>
          <input
            value={lastName}
            onChange={(e) => setLastName(e.target.value)}
          />
        </div>
        <button type="submit">submit</button>
      </form>
      {message}
    </div>
  );
}
```

我们有`firstName`、`lastName`、`message`状态，它们分别保存名字、姓氏和欢迎消息。

然后我们定义`submit`函数，让我们将`firstName`和`lastName`放入`message`。

在其中，我们调用`e.preventDefault()`让我们进行客户端表单提交。

然后我们检查`firstName`和`lastName`是否长于 0 长度。

如果是，那么我们调用`setMessages`将`message`值设置为欢迎消息。

在那下面，我们有一个将`onSubmit`属性设置为`submit`的表单，所以我们可以通过点击一个类型为`submit`的按钮来运行它。

在它里面，我们有两个输入，让我们输入名字和姓氏。

`value`有设定值的状态。

`onChange`设置为一个函数，分别将`firstName`和`lastName`状态设置为分别调用`setFirstName`和`setLastName`的函数。

`e.target.value`有我们输入的值。

在表格下面，我们展示或者欢迎`message`。

# 结论

我们可以用 React 和 JavaScript 创建一个欢迎消息应用程序。

*更多内容请看*[***plain English . io***](http://plainenglish.io)