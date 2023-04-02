# 理解 JavaScript 基础知识反应更快

> 原文：<https://javascript.plainenglish.io/js-fundamentals-to-understand-reactjs-faster-6dfef87b67de?source=collection_archive---------7----------------------->

## 构建现代 React 应用程序的关键 JavaScript 概念。

![](img/e9199b6ef36e22a93e249a8d5fa394f3.png)

Photo by [Chris Liverani](https://unsplash.com/@chrisliverani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您已经很好地掌握了 JavaScript，并且希望继续使用 React 之类的复杂库，那么在开始之前，您需要了解和掌握一些关键概念。

掌握这些基础知识将缩短您的学习曲线，并让您更好地理解组件内部发生的事情，并有望最终编写出更好的代码。

本文假设您熟悉 JavaScript，并且可能已经知道其中的一些概念。每个案例都包含一个用于下述反应的应用程序。请考虑通过它们的官方文档链接阅读更多关于它们的信息。

# JavaScript 模块

当您开始在 React 中工作时，您将很快理解对[代码拆分](https://reactjs.org/docs/code-splitting.html)的需求。应用程序可以发展得非常快，而且随着它们的发展，它们变得越来越难以阅读和理解。

幸运的是，您可以利用 Js [模块](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)将代码分割成更小更易管理的块。现在记住:

> 模块只是一个文件。一个脚本就是一个模块。就这么简单。— [javascript.info](https://javascript.info/modules-intro)

拆分代码将允许你利用 React 组件内部的本地[作用域](https://developer.mozilla.org/en-US/docs/Glossary/Scope)和[提升](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)。

因此，React 组件不是 Js 模块，但是它可以存在于 Js 模块中。重要的是你要知道两者的区别，这样你就可以在组件之外思考，并使用模块的作用域来声明变量，导入其他模块，执行业务逻辑等等。

# 目标

除了原始的[数据类型](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)，JavaScript 中几乎所有的东西都是[对象类](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)的实例，这可能是你需要学习的最重要的数据结构，本质上是因为 JavaScript 是一种[面向对象的编程语言](https://developer.mozilla.org/en-US/docs/Glossary/OOP)。

> 对象是指包含数据和处理数据的指令的数据结构—[developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Glossary/Object)

了解如何使用对象将允许您简化在应用程序中处理数据的方式。它们是完美的信息传输工具，对于在脚本中对逻辑进行分组非常有用。

在 React 中，对象可以用于在组件之间传递属性，处理组件状态，将内联样式应用于 HTML，以 [JSON](https://developer.mozilla.org/en-US/docs/Glossary/JSON) 格式呈现数据或将数据传输到任何外部 API，等等。

# 解构作业

在 [ECMAScript 2015 (ES6](https://www.w3schools.com/js/js_es6.asp) )中引入的最受欢迎的功能之一。它的主要目的是提供一种更干净的管理对象的方式，使用它将缩短和细化您的代码。

> **析构赋值**语法是一个 JavaScript 表达式，可以将数组中的值或对象中的属性解包到不同的变量中。—[developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

下面是一个析构对象的例子:

```
*({ a, b } = { a: 10, b: 20 });
console.log(a); // 10
console.log(b); // 20*
```

在 modern React 中，除了上面描述的传统用法之外，当使用[钩子](https://reactjs.org/docs/hooks-intro.html)时，你将使用解构赋值。

钩子允许你在[功能组件](https://reactjs.org/docs/components-and-props.html#function-and-class-components)中处理状态，语法如下:

```
*const [count, setCount] = useState(0);*
```

理解这个概念将有助于您在处理具有复杂逻辑和异步状态的组件时更快地进步。你可以从 [React 的官方文档](https://reactjs.org/docs/hooks-overview.html)中读到更多关于它的应用用法。

# 箭头功能

在 [ECMAScript 2015 (ES6](https://www.w3schools.com/js/js_es6.asp) )中引入的另一个流行特性。本质上，它们是函数表达式的简写，或者更好地定义:

> *箭头函数表达式*是用“胖箭头”语法(= >)编写的匿名函数表达式。—[digitalocean.com](https://www.digitalocean.com/community/tutorials/understanding-arrow-functions-in-javascript)

```
*const foo = (param1, paramN) => expression*
```

它们以与常规函数相同的方式工作，但是它们有一些限制，这可能有助于编写更好的代码。例如，箭头函数不能被提升，这意味着你需要在调用它们之前声明它们，使得代码更容易阅读。而且不能用关键字“*这个****”***，这样会防止范围 bug 等等。

在 React 中，箭头函数通常用作功能组件内部的方法，或者用作组件本身的定义。虽然使用[函数声明](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)来定义你的组件更被接受。

# 事件

一个[事件](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)被简单地定义为发生在系统中的一个动作，它被触发以通知某些事情已经改变。用更专业的术语来说，事件是一个对象，然后可以方便地使用和操作它。

每一个设计用户界面(UI)的 JavaScript 应用程序都会在某个时刻触发事件。现在，如果您查看 [React](https://reactjs.org) 主页，他们将该库描述为:

> 一个用于构建用户界面的 JavaScript 库—[reactjs.org](https://reactjs.org)

因此，事件是在 React 中工作的整个概念的核心部分，但是它们有许多层，因此在继续使用库时熟悉它们的结构是非常重要的。

# 承诺

Promises 是一种更现代的异步回调函数的方法。不是将回调传递给函数，而是将它们附加到返回的对象上。

> **Promise** 对象表示异步操作的最终完成(或失败)及其结果值。—[developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

承诺可以被连锁、计时和验证。结合箭头函数，它们为代码逻辑提供了一个漂亮的数组:

```
*promise1
.then(value => { return value })
.then(value => { return value + 1 })
.catch(err => { console.log(err) })
.finally(value => { console.log(value) });*
```

在 React 中，承诺主要用于数据获取，它们为应用程序提供了一种执行外部请求而不影响其状态的方式，这为用户带来了超级流畅的体验。在 React 中开始工作后不久，您将不得不执行第一次异步数据获取，因此尝试尽早了解这个概念。

# 结论

这些是我认为开发人员在开始使用现代 React 应用程序之前必须了解的 JavaScript 基础知识。我从语言的角度而不是从库的角度来描述它们，因为我相信这些是帮助你开始使用 React 的基础。

我希望你喜欢读这篇文章，并且它能帮助其他人找到你努力的方向。

*更多内容看*[***plain English . io***](http://plainenglish.io/)