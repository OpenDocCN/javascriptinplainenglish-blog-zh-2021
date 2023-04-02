# 用 React 和 JavaScript 创建一个简单的计算器

> 原文：<https://javascript.plainenglish.io/create-a-simple-calculator-with-react-and-javascript-cd1396dd0719?source=collection_archive---------21----------------------->

![](img/a01e0020c01b9580fa2b7f443f7341ef.png)

Photo by [StellrWeb](https://unsplash.com/@stellrweb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个简单的计算器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app simple-calculator
```

和 NPM 一起创建我们的 React 项目。

此外，我们必须安装`mathjs`库，这样我们就可以很容易地计算字符串中的数学表达式。

要安装它，我们运行:

```
npm i mathjs
```

# 创建计算器应用程序

为了创建计算器应用程序，我们编写:

```
import { useState } from "react";
import { evaluate } from "mathjs";export default function App() {
  const [expression, setExpression] = useState(""); const submit = (e) => {
    e.preventDefault();
    setExpression((ex) => evaluate(ex));
  }; return (
    <div className="App">
      <style>
        {`button {
          width: 20px
        }`}
      </style>
      <div>{expression}</div>
      <form onSubmit={submit}>
        <div>
          <button type="button" onClick={() => setExpression((ex) => `${ex}+`)}>
            +
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}-`)}>
            -
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}*`)}>
            *
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}/`)}>
            /
          </button>
        </div>
        <div>
          <button type="button" onClick={() => setExpression((ex) => `${ex}.`)}>
            .
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}9`)}>
            9
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}8`)}>
            8
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}7`)}>
            7
          </button>
        </div>
        <div>
          <button type="button" onClick={() => setExpression((ex) => `${ex}6`)}>
            6
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}5`)}>
            5
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}4`)}>
            4
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}3`)}>
            3
          </button>
        </div>
        <div>
          <button type="button" onClick={() => setExpression((ex) => `${ex}2`)}>
            2
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}1`)}>
            1
          </button>
          <button type="button" onClick={() => setExpression((ex) => `${ex}0`)}>
            0
          </button>
          <button type="submit">=</button>
        </div>
        <div>
          <button
            type="button"
            style={{ width: 50 }}
            onClick={() => setExpression("")}
          >
            Clear
          </button>
        </div>
      </form>
    </div>
  );
}
```

我们有用`useState`钩子创建的`expression`态。

它被设置为一个空字符串作为初始值。

然后我们用键盘和表达式显示返回 JSX 代码。

我们还有一个`style`标签来设置`button`元素为 20px 宽度。

大部分按钮除了=按钮都调用`setExpression`给`expression`追加一个字符。

回调函数有一个`ex`参数，它是`expression`的当前值。

我们返回`expression`的新值。

`form`元素将`onSubmit`属性设置为`submit`函数。

在`submit`中，我们调用`e.preventDefault()`来阻止服务器端表单提交。

然后我们用一个回调函数调用`setExpression`来返回`mathjs`的`evaluate`方法的返回值，该方法返回表达式字符串的计算值。

当我们单击 Clear 按钮时，它会将`expression`设置回空字符串。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个简单的计算器。

*更多内容看* [***说白了***](https://plainenglish.io/)