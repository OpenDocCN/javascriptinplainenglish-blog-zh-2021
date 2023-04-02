# 用 React 和 JavaScript 创建一个回文检查器

> 原文：<https://javascript.plainenglish.io/create-a-palindrome-checker-with-react-and-javascript-74e3c918f525?source=collection_archive---------13----------------------->

![](img/8fa35f1fbdbd90c2bcd6257a89f25770.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个回文检查器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app palindrome-checker
```

和 NPM 一起创建我们的 React 项目。

# 创建回文检查器

为了创建回文检查器，我们编写:

```
import React, { useMemo, useState } from "react";export default function App() {
  const [word, setWord] = useState(""); const isPalindrome = useMemo(() => {
    return word === word.split("").reverse().join("");
  }, [word]); return (
    <div className="App">
      <form>
        <div>
          <label>word to check</label>
          <input value={word} onChange={(e) => setWord(e.target.value)} />
        </div>
      </form>
      <div>Is Palindrome:{isPalindrome ? "Yes" : "No"}</div>
    </div>
  );
}
```

我们有了用`value`和`onChange`属性绑定到输入的`word`状态。

我们用`onChange` prop 设置它的值，它有一个用`e.target.value`调用`setWord`的函数。

`e.target.value`有输入值。

接下来，我们用`useMemo`钩子创建`isPalindrome`变量。

它的第一个参数是一个回调函数，返回`word`和反转单词之间的比较。

我们用`word.split`反转`word`，将`word`拆分成一个字符数组。

然后我们调用`reverse`来反转字符数组。

并且我们调用`join`将字符数组再次连接回一个字符串。

在第二个参数中，我们传入一个带有`word`条目的数组，这样每当`word`改变时，第一个参数中回调的返回值都会更新。

在表单中，我们向用户显示输入，值是`isPalindrome`。

# 结论

我们可以用 React 和 JavaScript 创建一个回文检查器。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)