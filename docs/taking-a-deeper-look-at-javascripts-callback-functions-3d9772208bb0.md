# 深入了解 JavaScript 的回调函数

> 原文：<https://javascript.plainenglish.io/taking-a-deeper-look-at-javascripts-callback-functions-3d9772208bb0?source=collection_archive---------4----------------------->

## 如果你熟悉 JavaScript，我打赌你听说过回调函数。但是你真的知道它们是什么，我们为什么使用它们，或者如何使用它们吗？

![](img/75ca01d0c7ab232ee46d1bdf5a2635d8.png)

Photo by [Marten Newhall](https://unsplash.com/@laughayette?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 目录

1.  [简介](#e814)
2.  [快速回顾](#8049)
3.  [定义教科书定义](#e6e7)
4.  [为什么我们需要回调？](#83a8)
5.  [但这到底意味着什么呢？](#edf4)
6.  [创建回调函数](#2406)
    6a。[奖金！回调地狱](#be6f)
7.  [结论&要点](#c5cf)
8.  [想要更多？查看其他资源！](#a8bb)

# 介绍🤿

JavaScript 中一定会遇到回调函数。虽然我知道什么是回访以及如何写回访，但我承认我的理解只是肤浅的😞在我自己的研究中，我发现这些解释要么太含糊，要么用了太多的技术术语，中间没有任何东西。为了加深我的理解，并与那些没有 JavaScript 经验的人分享我自己的观点，我将把它留在这里😄！

# **快速回顾** ⚡

开始之前，请记住以下几点:

*   *【一级函数】*:在 JavaScript 中函数是对象，我们可以将对象作为参数传递给函数。当你听到 JavaScript 有“一流的功能”时，这就是它所指的；该语言中的函数被视为与任何其他变量一样。
*   *异步 JavaScript* :简单来说，异步意味着允许多件事情同时发生，同时保持彼此独立。当您在后台等待某些代码(例如，您向 API 发出请求)同时继续运行其余代码时，通常会使用它。
*   *匿名函数*:函数没有名字的时候。如果函数存储在变量中，它不需要名字；相反，它是用变量名调用的。在匿名函数中,“this”关键字代表调用该函数的对象。
*   箭头函数:在 ES6 中引入，它们允许我们编写更短的函数语法。需要注意的重要一点是,“this”关键字总是代表定义 arrow 函数的对象。因此没有“这个”的约束。同样，如果 arrow 函数只有一个语句，你可以去掉花括号和 return 关键字。

```
// This is an anonymous function
let anonHello = function (name) {console.log(“Hi” + “ ” + name)}
anonHello(“Bob”) // returns “Hi Bob”// This is an arrow function
arrowHello = (name) => `Hello ${name}`
arrowHello(“Bob”) // returns “Hi Bob”
```

# **定义教科书定义📕**

为了理解什么是回调函数，我们先来看看回调的定义。

直接从 [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function) 开始，“回调函数是作为参数传递给另一个函数的函数，然后在外部函数中调用它来完成某种例程或动作。”换句话说，回调函数是作为另一个函数调用的参数传入的函数定义。回调永远不会运行，直到外部函数在适当的时候执行它。因此，回调受到接收它的函数的支配。

**边注**:一个无需深入细节的有趣事实是，JavaScript 中的一切都可以表现得像一个对象，即使它不是一个对象(即原语)。如果你对细节感兴趣，请点击这里查看安德鲁·克尼格-包蒂斯塔的解释[！](https://medium.com/better-programming/everything-in-javascript-is-an-object-except-for-when-it-isnt-305bc65a3410)

# **为什么我们需要回调？🤷‍♀️**

在阅读回调函数的好处之前，记住什么是[异步 JS](#b6df) 可能会有所帮助！

JavaScript 是一种事件驱动语言，代码自顶向下运行。正因为如此，为了考虑到当你不需要一些代码运行直到其他事情(例如，一个按钮被点击)之后，我们使用回调来保证一个函数不会在另一个任务完成之前运行。相反，该功能被“回调”,并将在其他任务完成后立即运行。这允许我们的代码继续执行，并防止我们的代码等待响应。

# **但是这到底意味着什么呢？🔎**

我明白了，这都是概念性的，所以即使我们理解了什么是回调以及我们为什么需要回调，那*到底是什么意思呢*？让我们看一个基本的例子来更好地理解“继续执行”和“回调直到另一个任务完成才会运行”的含义。

```
function first(){
 console.log(“I am first”)
}function second(){
 console.log(“I am second”)
}first()
second()
```

基于以上所述，“我是第一个”将首先登录，然后“我是第二个”将随后登录。然而，如果我们通过使用 setTimeout 异步调用回调函数使这变得更复杂:

```
function first(){
 setTimeout( function(){
  console.log(“I am first")
 }, 3000)
}function second(){
 console.log(“I am second”)
}first()
second()
```

“我是第二名”将是第一名，三秒钟后“我是第一名”将出现。这是因为尽管 first()在 second()之前被调用，JavaScript 仍会继续执行，而不会等待 3 秒钟。3 秒钟过去后，第一个()函数能够完成执行。因此，即使 JavaScript 是自顶向下执行的，你也不能总是期望它按顺序运行。这就是为什么回调如此重要；它们让我们能够控制代码的执行方式。

但是这并不意味着所有的回调函数都是异步的。它们也可以同步使用，这意味着代码会立即执行。这通常被称为“阻塞”,在这种情况下，直到回调完成执行，高阶函数才完成其执行。同步回调函数的例子有 forEach()、map()和 filter()等数组方法。

# **创建回调函数🏗️**

有三种方法可以创建回调函数:作为匿名函数、箭头函数，或者作为参数传递。让我们看看他们的行动吧！

```
// This an anonymous function
setTimeout(function() {
 console.log("This message is shown after 3 seconds")
}, 3000)// This is an arrow function
setTimeout(() => {
 console.log(“This message is shown after 3 seconds”)
}, 3000)// This is passing the callback as an argument
let message = function() { console.log(“This message is shown after 3 seconds”) }setTimeout(callback, 3000)setTimeout(message, 3000) // passing in the message as the callback
```

## **奖金**！回调地狱🔥

绝对有可能将回调嵌套在彼此内部。但是，它的伸缩性不好；这被称为“回调地狱”。相反，最好使用 promises 或 async/await 函数。

# **结论&外卖🐠**

你坚持到了最后🙌我加深了对回调函数以及其他相关主题的理解。这显示了一切是如何联系在一起的，通过花时间去了解一件事，你实际上从整体上了解了更多。

以下是我希望你记住的最重要的事情:

*   JavaScript 代码从上到下运行，但这并不意味着它会按顺序执行。
*   [回调是外部函数调用的函数定义。](#540f)
*   [回调通过允许代码继续执行而不等待它自己的代码运行，让我们控制我们的代码如何执行；相反，它等待外部函数“回调”和/或其他任务完成。](#c678)
*   [也就是说，回调函数可以同步和异步使用。](#c142)

感谢你跟随我踏上✌️的回归之旅。如果你喜欢这篇文章，请看看我的其他作品！一个很好的起点是我的相关文章“ [JavaScript Promises 101](https://medium.com/geekculture/javascript-promises-101-14f28158e5b9) ”、“[React Basics:JavaScript 和 JSX 有什么区别？](https://medium.com/weekly-webtips/react-basics-whats-the-difference-between-javascript-and-jsx-604dd224b1cf)或[React Basics:Components and the Importance State](https://medium.com/swlh/react-basics-components-and-the-importance-of-state-dd26250e88ce)。

# 想要更多吗？查看其他资源！💾

## 用 JavaScript 进行异步编程

📖[https://medium . com/codingsemartway-com-blog/async-programming-with-JavaScript-callbacks-promises-and-async-await-980 e3f 144185](https://medium.com/codingthesmartway-com-blog/async-programming-with-javascript-callbacks-promises-and-async-await-980e3f144185)

## JavaScript 回调

📖【https://dmitripavlutin.com/javascript-callback/[📖](https://dmitripavlutin.com/javascript-callback/)[https://www . freecodecamp . org/news/JavaScript-callback-functions-what-is-callbacks-in-js-and-how-to-use-them/](https://www.freecodecamp.org/news/javascript-callback-functions-what-are-callbacks-in-js-and-how-to-use-them/)
📖[https://code burst . io/JavaScript-what-the-heck-a-callback-ABA 4d a2 deced](https://codeburst.io/javascript-what-the-heck-is-a-callback-aba4da2deced)
📖[https://www.javascripttutorial.net/javascript-callback/](https://www.javascripttutorial.net/javascript-callback/)