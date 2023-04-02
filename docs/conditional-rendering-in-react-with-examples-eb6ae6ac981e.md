# 反应示例中的条件呈现

> 原文：<https://javascript.plainenglish.io/conditional-rendering-in-react-with-examples-eb6ae6ac981e?source=collection_archive---------12----------------------->

## 通过实例了解 React 中的条件渲染。

![](img/bdb3e19d2750c1713965c30e6f04171d.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

条件渲染是 React 中的主要概念之一。它允许您根据应用程序的状态来呈现组件。在 React 中，有许多方法可以进行条件渲染。

这就是为什么在本文中，我们将了解一些在 React 中实现条件渲染的方法。让我们开始吧。

# 使用 If Else 的条件呈现

在 React 中，我们不能在 JSX 内部直接使用 if-else 语句。然而，我们可以使用 if-else 语句来呈现 JSX 和我们的组件。当我们想在 if-else 块中执行多行代码时，这很有用。

这里有一个例子:

```
import React , { useState } from 'react';
import ReactDOM from 'react-dom';// Our functional component.
const App = ()=>{
  const [isLogged, setLogin] = useState(true);
  **if(isLogged){
    return <h1>Hello</h1>
  }else{
    return <h1>Sign Up</h1>
  }**
}// Rendering the component using the render method.
ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

*输出:*

```
Hello
```

我们还可以在 if-else 语句中使用多行代码来呈现其他组件。

这里有一个例子:

```
const App = ()=>{
  const [isLogged, setLogin] = useState(true);
  **if(isLogged){
    <Component1 />
    setLogin****(userData);** //more code.
  **}else{
    <Component2 />
  }**
}
```

如您所见，我们可以在 React 中使用 if-else 语句进行条件渲染。但是我们不能在 JSX 境内使用它们，有一些其他的方法可以做到这一点，我将在下面向你展示。

# 三元运算符

我们可以使用三元运算符`? :`有条件地呈现 JSX 内部的组件。当您希望根据应用程序状态执行一行代码时，这很有用。

这里有一个例子:

```
const App = ()=>{
  const [isLogged, setLogin] = useState(false);
  return (
    <>
    **{isLogged ? <h1>Hello</h1> : <h1>Sign Up</h1>}**
    </>
  )
}
```

*输出:*

![](img/45f65d51fe116898c59b392f1201ab10.png)

Output.

我们还可以根据应用程序的状态值来呈现组件。

这里有一个例子:

```
const App = ()=>{
  const [isLogged, setLogin] = useState(false);
  return (
    <>
    **{isLogged ? <Component1 /> : <Component2 />}**
    </>
  )
}
```

如您所见，三元运算符仅用于一行代码，它也可以在 JSX 内部使用。你只需要用花括号`{}`告诉 React 你正在 JSX 内部使用 JavaScript 代码。

如果你不熟悉三元运算符，你可以看看我下面的详细文章:

[](/better-javascript-the-ternary-operator-d181338c4c20) [## 更好的 JavaScript——三元运算符

### 理解 JavaScript 中的三元运算符以及如何使用它

javascript.plainenglish.io](/better-javascript-the-ternary-operator-d181338c4c20) 

# 短路&运算符

短路`&&`操作符也可以用于条件渲染。它主要用在你只有一个没有`else`的条件`if`语句的时候，也可以在 JSX 内部执行。

看看下面的例子:

```
const Greeting = ()=>{
  return (
    <h1>Hello World!</h1>
  )
}const App = ()=>{
  const [isLogged, setLogin] = useState(true);
  return (
    <>
    **{isLogged && <Greeting />}**
    </>
  )
}*// Rendering the component with the render method.* ReactDOM.render(
<App />,
document.getElementById('root'));
```

*输出:*

![](img/23e87b3b9d40b4f5dbd09ed5b136ac4b.png)

Output.

如您所见，如果状态`isLogged`为真，操作符`&&`呈现组件`<Greeting />`。但是要记住，短路`&&`只能代替一个没有`else`的`if`语句。

# 结论

在 React 中有很多方法可以进行条件渲染。你可以根据你的情况使用任何方法。但是如果我有多行代码需要根据某些条件来执行，我总是会使用 if-else 语句。

感谢您阅读这篇文章。希望你觉得有用。

**延伸阅读**

[](/8-must-have-vscode-extensions-for-front-end-web-developers-69842a456f9c) [## 前端 Web 开发人员必备的 8 个 VSCode 扩展

### 8 个 VSCode 扩展，让您的生活更轻松。

javascript.plainenglish.io](/8-must-have-vscode-extensions-for-front-end-web-developers-69842a456f9c)