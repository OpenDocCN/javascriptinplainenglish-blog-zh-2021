# 用 React 和 JavaScript 创建一个密码生成器

> 原文：<https://javascript.plainenglish.io/create-a-password-generator-with-react-and-javascript-789dd96ba8b8?source=collection_archive---------13----------------------->

![](img/5f4d09e33a8470219b9a2bbd48fa429e.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个密码生成器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app password-generator
```

和 NPM 一起创建我们的 React 项目。

# 创建密码生成器应用程序

为了创建密码生成器应用程序，我们编写:

```
import React, { useState } from "react";
const string = "abcdefghijklmnopqrstuvwxyz";
const numeric = "0123456789";
const punctuation = "!@#$%^&*()_+~`|}{[]:;?><,./-=";export default function App() {
  const [length, setLength] = useState(10);
  const [password, setPassword] = useState(""); const generatePassword = (e) => {
    e.preventDefault();
    const formValid = +length > 0;
    if (!formValid) {
      return;
    }
    let character = "";
    let password = "";
    while (password.length < length) {
      const entity1 = Math.ceil(string.length * Math.random() * Math.random());
      const entity2 = Math.ceil(numeric.length * Math.random() * Math.random());
      const entity3 = Math.ceil(
        punctuation.length * Math.random() * Math.random()
      );
      let hold = string.charAt(entity1);
      hold = password.length % 2 === 0 ? hold.toUpperCase() : hold;
      character += hold;
      character += numeric.charAt(entity2);
      character += punctuation.charAt(entity3);
      password = character;
    }
    password = password
      .split("")
      .sort(() => {
        return 0.5 - Math.random();
      })
      .join("");
    setPassword(password.substr(0, length));
  }; return (
    <div className="App">
      <form onSubmit={generatePassword}>
        <div>
          <label>length</label>
          <input value={length} onChange={(e) => setLength(e.target.value)} />
        </div>
        <button type="submit">generate password</button>
      </form>
      <div>{password}</div>
    </div>
  );
}
```

我们定义`length`状态来保持长度。

`password`已经生成密码。

接下来，我们定义`generatePassword`函数来生成密码。

在函数中，我们调用`e.preventDefault`做客户端表单提交。

然后我们检查`length`，看它是否大于 0。

如果是，那么我们创建密码。

为了创建它，我们创建 3 个数字并分别存储在`entity1`、`entity2`和`entity3`中。

然后我们用它们从`string`、`numeric`和`punctuation`中得到一个值。

然后我们将它们添加到`character`变量中。

然后我们将`character`的值赋给`password`。

然后我们用`split`、`sort`和`join`来洗牌`password`字符。

`sort`回调返回一个介于-0.5 和 0.5 之间的随机数来洗牌。

最后，我们调用`setPassword`来设置`password`值。

在下面，我们添加一个表单，将`onSubmit`属性设置为`generatePassword`，当我们单击类型为`submit`的按钮时生成密码。

输入 hs 分别支持`value`和`onChange`获得和设置`length`状态。

`e.target.value`有输入值。

# 结论

我们可以用 React 和 JavaScript 创建一个密码生成器。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)