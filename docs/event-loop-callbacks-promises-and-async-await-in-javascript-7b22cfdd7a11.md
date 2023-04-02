# JavaScript 中的事件循环、回调、承诺和异步/等待

> 原文：<https://javascript.plainenglish.io/event-loop-callbacks-promises-and-async-await-in-javascript-7b22cfdd7a11?source=collection_archive---------6----------------------->

# 介绍

在互联网的早期，网站通常由一个 [HTML 页面](https://www.digitalocean.com/community/tutorial_series/how-to-build-a-website-with-html)中的静态数据组成。但是现在网络应用程序变得更加交互和动态，它变得越来越有必要进行密集的操作，比如发出外部网络请求来检索 [API](https://developer.mozilla.org/en-US/docs/Glossary/API) 数据。为了在 JavaScript 中处理这些操作，开发人员必须使用*异步编程*技术。

由于 JavaScript 是一种*单线程*编程语言，具有*同步*执行模型，处理一个又一个操作，所以一次只能处理一条语句。但是，像从 API 请求数据这样的操作可能需要不确定的时间，这取决于所请求数据的大小、网络连接的速度以及其他因素。如果 API 调用是以同步方式执行的，浏览器将无法处理任何用户输入，比如滚动或单击按钮，直到该操作完成。这就是所谓的*阻塞*。

为了防止阻塞行为，浏览器环境有许多 JavaScript 可以访问的 Web APIs，它们是*异步的*，这意味着它们可以与其他操作并行运行，而不是顺序运行。这很有用，因为它允许用户在处理异步操作时继续正常使用浏览器。

作为一名 JavaScript 开发人员，您需要知道如何使用异步 Web APIs 并处理这些操作的响应或错误。在本文中，您将了解事件循环、通过回调处理异步行为的原始方式、更新的 [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) 增加的承诺，以及使用`async/await`的现代实践

# 事件循环

本节将解释 JavaScript 如何处理带有事件循环的异步代码。它将首先演示工作中的事件循环，然后解释事件循环的两个元素:堆栈和队列。

不使用任何异步 Web APIs 的 JavaScript 代码将以同步方式执行——一次一个，按顺序执行。这个示例代码演示了这一点，它调用三个函数，每个函数向[控制台](https://www.digitalocean.com/community/tutorials/how-to-use-the-javascript-developer-console)打印一个数字:

```
// Define three example functions
function first() {
  console.log(1)
}function second() {
  console.log(2)
}function third() {
  console.log(3)
}
```

在这段代码中，您定义了三个用`console.log()`打印数字的函数。

接下来，编写对函数的调用:

```
// Execute the functions
first()
second()
third()
```

输出将基于函数被调用的顺序— `first()`、`second()`，然后是`third()`:

```
Output1
2
3
```

当使用异步 Web API 时，规则变得更加复杂。您可以用一个内置的 API`setTimeout`进行测试，它设置了一个定时器，并在指定的时间后执行一个动作。`setTimeout`需要异步，否则整个浏览器将在等待期间保持冻结，这将导致糟糕的用户体验。

向`second`函数添加`setTimeout`来模拟异步请求:

```
// Define three example functions, but one of them contains asynchronous code
function first() {
  console.log(1)
}function second() {
  setTimeout(() => {
    console.log(2)
  }, 0)
}function third() {
  console.log(3)
}
```

`setTimeout`接受两个参数:它将异步运行的函数，以及在调用该函数之前它将等待的时间。在这段代码中，您将`console.log`包装在一个匿名函数中，并将其传递给`setTimeout`，然后将该函数设置为在`0`毫秒后运行。

现在像以前一样调用这些函数:

```
// Execute the functions
first()
second()
third()
```

您可能希望在`setTimeout`设置为`0`的情况下，运行这三个函数仍然会导致数字按顺序打印。但是因为它是异步的，超时的函数将最后打印出来:

```
Output1
3
2
```

无论您将超时设置为零秒还是五分钟都没有区别——异步代码调用的`console.log`将在同步顶级函数之后执行。这是因为 JavaScript 主机环境(在本例中是浏览器)使用了一个叫做*事件循环*的概念来处理并发或并行事件。由于 JavaScript 一次只能执行一条语句，因此需要通知事件循环何时执行哪条特定的语句。事件循环用一个*堆栈*和一个*队列*的概念来处理这个问题。

# 堆

*堆栈*或调用堆栈，保存当前正在运行的函数的状态。如果你不熟悉堆栈的概念，你可以把它想象成一个具有“后进先出”(LIFO)属性的[数组](https://www.digitalocean.com/community/tutorials/understanding-arrays-in-javascript)，这意味着你只能在堆栈的末尾添加或删除项目。JavaScript 会运行堆栈中当前的*帧*(或者特定环境下的函数调用)，然后移除它，继续下一个。

对于仅包含同步代码的示例，浏览器按以下顺序处理执行:

*   将`first()`添加到堆栈中，运行将`1`记录到控制台的`first()`，从堆栈中移除`first()`。
*   将`second()`添加到堆栈中，运行将`2`记录到控制台的`second()`，从堆栈中移除`second()`。
*   将`third()`添加到堆栈中，运行将`3`记录到控制台的`third()`，从堆栈中移除`third()`。

第二个带有`setTimout`的例子如下所示:

*   将`first()`添加到堆栈中，运行将`1`记录到控制台的`first()`，从堆栈中移除`first()`。
*   将`second()`添加到堆栈中，运行`second()`。
*   将`setTimeout()`添加到堆栈中，运行`setTimeout()` Web API，它启动一个定时器并将匿名函数添加到*队列*中，从堆栈中移除`setTimeout()`。
*   从堆栈中移除`second()`。
*   将`third()`添加到堆栈中，运行将`3`记录到控制台的`third()`，从堆栈中移除`third()`。
*   事件循环检查队列中是否有任何未决消息，并从`setTimeout()`中找到匿名函数，将该函数添加到将`2`记录到控制台的堆栈中，然后将其从堆栈中移除。

使用异步 Web API`setTimeout`，引入了*队列*的概念，本教程将在接下来介绍。

# 长队

*队列*，也称为消息队列或任务队列，是函数的等待区。每当调用堆栈为空时，事件循环将从最早的消息开始，检查队列中是否有任何等待的消息。一旦找到一个，它将把它添加到堆栈中，堆栈将执行消息中的函数。

在`setTimeout`示例中，匿名函数在顶层执行的剩余部分之后立即运行，因为计时器被设置为`0`秒。重要的是要记住，计时器并不意味着代码将在精确的`0`秒或任何指定的时间内执行，而是在这段时间内将匿名函数添加到队列中。这个队列系统之所以存在，是因为如果计时器在计时器结束时将匿名函数直接添加到堆栈中，它将中断当前正在运行的任何函数，这可能会产生意想不到的和不可预测的影响。

现在您知道了事件循环如何使用堆栈和队列来处理代码的执行顺序。下一个任务是找出如何控制代码的执行顺序。为此，您将首先了解确保异步代码被事件循环正确处理的原始方法:回调函数。

# 回调函数

在`setTimeout`示例中，超时的函数在主顶级执行上下文中的所有内容之后运行。但是如果你想确保其中一个函数，比如`third`函数，在超时后运行，那么你必须使用异步编码方法。这里的超时可以表示包含数据的异步 API 调用。您希望处理来自 API 调用的数据，但是您必须确保首先返回数据。

处理这个问题的原始解决方案是使用*回调函数*。回调函数没有特殊的语法；它们只是一个作为参数传递给另一个函数的函数。将另一个函数作为自变量的函数称为*高阶函数*。根据这个定义，任何函数如果作为参数传递，都可以成为回调函数。回调本质上不是异步的，但是可以用于异步目的。

下面是高阶函数和回调的语法代码示例:

```
// A function
function fn() {
  console.log('Just a function')
}// A function that takes another function as an argument
function higherOrderFunction(callback) {
  // When you call a function that is passed as an argument, it is referred to as a callback
  callback()
}// Passing a function
higherOrderFunction(fn)
```

在这段代码中，您定义了一个函数`fn`，定义了一个以函数`callback`为参数的函数`higherOrderFunction`，并将`fn`作为回调传递给`higherOrderFunction`。

运行这段代码将得到以下结果:

```
OutputJust a function
```

让我们回到带有`setTimeout`的`first`、`second`和`third`功能。这是你目前所拥有的:

```
function first() {
  console.log(1)
}function second() {
  setTimeout(() => {
    console.log(2)
  }, 0)
}function third() {
  console.log(3)
}
```

任务是让`third`函数总是延迟执行，直到`second`函数中的异步动作完成。这就是回调的用武之地。您将把`third`函数作为参数传递给`second`，而不是在顶层执行`first`、`second`和`third`。`second`函数将在异步动作完成后执行回调。

下面是应用了回调的三个函数:

```
// Define three functions
function first() {
  console.log(1)
}function second(callback) {
  setTimeout(() => {
    console.log(2) // Execute the callback function
    callback()
  }, 0)
}function third() {
  console.log(3)
}
```

现在，执行`first`和`second`，然后将`third`作为参数传递给`second`:

```
first()
second(third)
```

运行此代码块后，您将收到以下输出:

```
Output1
2
3
```

首先`1`将会打印，在计时器完成后(在本例中是零秒，但您可以将其更改为任意值)，它将会打印`2`然后`3`。通过将函数作为回调传递，您成功地延迟了函数的执行，直到异步 Web API ( `setTimeout`)完成。

这里的关键要点是回调函数不是异步的— `setTimeout`是负责处理异步任务的异步 Web API。回调只允许您在异步任务完成时得到通知，并处理任务的成功或失败。

现在您已经学习了如何使用回调来处理异步任务，下一节将解释嵌套太多回调和创建“末日金字塔”的问题

# 嵌套回调和末日金字塔

回调函数是确保延迟执行一个函数直到另一个函数完成并返回数据的有效方法。然而，由于回调的嵌套性质，如果您有许多相互依赖的连续异步请求，代码可能会变得混乱。这在早期对 JavaScript 开发人员来说是一个很大的挫折，因此包含嵌套回调的代码通常被称为“末日金字塔”或“回调地狱”

下面是嵌套回调的演示:

```
function pyramidOfDoom() {
  setTimeout(() => {
    console.log(1)
    setTimeout(() => {
      console.log(2)
      setTimeout(() => {
        console.log(3)
      }, 500)
    }, 2000)
  }, 1000)
}
```

在这段代码中，每个新的`setTimeout`都嵌套在一个更高阶的函数中，创建了一个越来越深的回调的金字塔形状。运行这段代码将得到以下结果:

```
Output1
2
3
```

实际上，对于现实世界中的异步代码，这可能会变得更加复杂。您很可能需要在异步代码中进行错误处理，然后将每个响应中的一些数据传递给下一个请求。用回调做这件事会使你的代码难以阅读和维护。

这里有一个更现实的“末日金字塔”的运行示例，您可以随意摆弄:

```
// Example asynchronous function
function asynchronousRequest(args, callback) {
  // Throw an error if no arguments are passed
  if (!args) {
    return callback(new Error('Whoa! Something went wrong.'))
  } else {
    return setTimeout(
      // Just adding in a random number so it seems like the contrived asynchronous function
      // returned different data
      () => callback(null, {body: args + ' ' + Math.floor(Math.random() * 10)}),
      500,
    )
  }
}// Nested asynchronous requests
function callbackHell() {
  asynchronousRequest('First', function first(error, response) {
    if (error) {
      console.log(error)
      return
    }
    console.log(response.body)
    asynchronousRequest('Second', function second(error, response) {
      if (error) {
        console.log(error)
        return
      }
      console.log(response.body)
      asynchronousRequest(null, function third(error, response) {
        if (error) {
          console.log(error)
          return
        }
        console.log(response.body)
      })
    })
  })
}// Execute
callbackHell()
```

在这段代码中，你必须让每个函数都考虑到一个可能的`response`和一个可能的`error`，让函数`callbackHell`在视觉上变得混乱。

运行这段代码将得到以下结果:

```
OutputFirst 9
Second 3
Error: Whoa! Something went wrong.
    at asynchronousRequest (<anonymous>:4:21)
    at second (<anonymous>:29:7)
    at <anonymous>:9:13
```

这种处理异步代码的方式很难遵循。于是，在 ES6 中引入了*承诺*的概念。这是下一节的重点。

# 承诺

一个*承诺*代表一个异步函数的完成。它是一个将来可能会返回值的对象。它实现了与回调函数相同的基本目标，但是增加了许多额外的特性和更易读的语法。作为一名 JavaScript 开发人员，您可能会花更多的时间来消费承诺，而不是创建承诺，因为通常是异步 Web APIs 返回一个承诺供开发人员消费。本教程将向您展示如何做到这两点。

# 创造承诺

你可以用`new Promise`语法初始化一个承诺，而且你必须用一个函数来初始化它。传递给 promise 的函数有`resolve`和`reject`参数。`resolve`和`reject`函数分别处理操作的成功和失败。

写下面一行来宣告一个承诺:

```
// Initialize a promise
const promise = new Promise((resolve, reject) => {})
```

如果您使用 web 浏览器的控制台检查这种状态下的初始化承诺，您会发现它有一个`pending`状态和`undefined`值:

```
Output__proto__: Promise
[[PromiseStatus]]: "pending"
[[PromiseValue]]: undefined
```

到目前为止，还没有为承诺设置任何东西，所以它将永远处于`pending`状态。检验一个承诺的第一件事就是通过用一个价值来解决它来履行承诺:

```
const promise = new Promise((resolve, reject) => {
  resolve('We did it!')
})
```

现在，在检查承诺时，您会发现它的状态为`fulfilled`，并且`value`被设置为您传递给`resolve`的值:

```
Output__proto__: Promise
[[PromiseStatus]]: "fulfilled"
[[PromiseValue]]: "We did it!"
```

如本节开头所述，承诺是可以返回值的对象。成功完成后，`value`从`undefined`变为被数据填充。

承诺可以有三种可能的状态:待定、履行和拒绝。

*   **待定** —解决或拒绝前的初始状态
*   **履行完毕** —操作成功，承诺已解决
*   **被拒绝** —操作失败，承诺被拒绝

在履行或拒绝之后，承诺就达成了。

既然你对承诺是如何产生的有了一个概念，让我们看看一个开发者如何消费这些承诺。

# 履行诺言

上一节中的承诺已经用一个值实现了，但是您还希望能够访问该值。承诺有一个名为`then`的方法，它将在承诺到达代码中的`resolve`后运行。`then`将返回承诺的值作为参数。

这是您返回并记录示例承诺的`value`的方式:

```
promise.then((response) => {
  console.log(response)
})
```

你创造的承诺有一个`We did it!`的`[[PromiseValue]]`。这个值将作为`response`传递给匿名函数:

```
OutputWe did it!
```

到目前为止，您创建的示例没有涉及异步 Web API——它只解释了如何创建、解析和使用原生 JavaScript promise。使用`setTimeout`，您可以测试出一个异步请求。

以下代码将异步请求返回的数据模拟为承诺:

```
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve('Resolving an asynchronous request!'), 2000)
})// Log the result
promise.then((response) => {
  console.log(response)
})
```

使用`then`语法确保只有在`2000`毫秒后`setTimeout`操作完成时才会记录`response`。所有这些都是在没有嵌套回调的情况下完成的。

现在，两秒钟后，它将解析承诺值，并记录在`then`中:

```
OutputResolving an asynchronous request!
```

承诺也可以被链接起来，将数据传递给多个异步操作。如果在`then`中返回一个值，可以添加另一个`then`来满足前一个`then`的返回值:

```
// Chain a promise
promise
  .then((firstResponse) => {
    // Return a new value for the next then
    return firstResponse + ' And chaining!'
  })
  .then((secondResponse) => {
    console.log(secondResponse)
  })
```

第二个`then`中完成的响应将记录返回值:

```
OutputResolving an asynchronous request! And chaining!
```

由于`then`可以被链接，它允许承诺的消费看起来比回调更同步，因为它们不需要嵌套。这将允许更多的可读代码，可以更容易地维护和验证。

# 错误处理

到目前为止，您只处理了一个成功的`resolve`承诺，它将承诺置于`fulfilled`状态。但是通常对于异步请求，您还必须处理一个错误——如果 API 关闭，或者发送了一个格式错误或未经授权的请求。一个承诺应该可以处理这两种情况。在本节中，您将创建一个函数来测试创建和消费承诺的成功和错误情况。

这个`getUsers`函数将传递一个标志给一个承诺，并返回承诺:

```
function getUsers(onSuccess) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      // Handle resolve and reject in the asynchronous API
    }, 1000)
  })
}
```

设置代码，以便如果`onSuccess`是`true`，超时将通过一些数据实现。如果`false`，该功能将出错拒绝:

```
function getUsers(onSuccess) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      // Handle resolve and reject in the asynchronous API
      if (onSuccess) {
        resolve([
          {id: 1, name: 'Jerry'},
          {id: 2, name: 'Elaine'},
          {id: 3, name: 'George'},
        ])
      } else {
        reject('Failed to fetch data!')
      }
    }, 1000)
  })
}
```

对于成功的结果，您返回代表样本用户数据的 JavaScript 对象。

为了处理这个错误，您将使用`catch`实例方法。这将给你一个失败回调，并把`error`作为一个参数。

在`onSuccess`设置为`false`的情况下运行`getUser`命令，对成功案例使用`then`方法，对错误案例使用`catch`方法:

```
// Run the getUsers function with the false flag to trigger an error
getUsers(false)
  .then((response) => {
    console.log(response)
  })
  .catch((error) => {
    console.error(error)
  })
```

由于错误被触发，将跳过`then`并由`catch`处理错误:

```
OutputFailed to fetch data!
```

如果您切换标志和`resolve`，则`catch`将被忽略，数据将返回:

```
// Run the getUsers function with the true flag to resolve successfully
getUsers(true)
  .then((response) => {
    console.log(response)
  })
  .catch((error) => {
    console.error(error)
  })
```

这将产生用户数据:

```
Output(3) [{…}, {…}, {…}]
0: {id: 1, name: "Jerry"}
1: {id: 2, name: "Elaine"}
3: {id: 3, name: "George"}
```

作为参考，这里有一个关于`Promise`对象的处理程序方法的表格:

方法描述`then()`处理一个`resolve`。返回一个承诺，并异步调用`onFulfilled`函数`catch()`处理一个`reject`。返回一个承诺，并在承诺完成时异步调用`onRejected`函数`finally()`。返回一个承诺，异步调用`onFinally`函数

承诺可能会使新开发人员和以前从未在异步环境中工作过的有经验的程序员感到困惑。然而，如上所述，消费承诺比创造承诺更常见。通常，浏览器的 Web API 或第三方库会提供承诺，您只需要使用它。

在最后的承诺部分，本教程将引用一个返回承诺的 Web API 的常见用例:[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)。

# 使用带有承诺的获取 API

最有用和最常用的 Web APIs 之一是 Fetch API，它允许您通过网络发出异步资源请求。`fetch`是一个两部分的过程，因此需要链接`then`。这个例子演示了使用 GitHub API 获取用户数据，同时处理任何潜在的错误:

```
// Fetch a user from the GitHub API
fetch('https://api.github.com/users/octocat')
  .then((response) => {
    return response.json()
  })
  .then((data) => {
    console.log(data)
  })
  .catch((error) => {
    console.error(error)
  })
```

`fetch`请求被发送到`https://api.github.com/users/octocat` URL，它异步等待响应。第一个`then`将响应传递给一个匿名函数，该函数将响应格式化为 [JSON 数据](https://www.digitalocean.com/community/tutorials/how-to-work-with-json-in-javascript)，然后将 JSON 传递给第二个`then`，后者将数据记录到控制台。`catch`语句将任何错误记录到控制台。

运行此代码将产生以下结果:

```
Outputlogin: "octocat",
id: 583231,
avatar_url: "https://avatars3.githubusercontent.com/u/583231?v=4"
blog: "https://github.blog"
company: "@github"
followers: 3203
...
```

这是从`https://api.github.com/users/octocat`请求的数据，以 JSON 格式呈现。

教程的这一部分显示了 promises 包含了许多处理异步代码的改进。但是，尽管使用`then`处理异步动作比金字塔式的回调更容易实现，一些开发人员仍然更喜欢编写异步代码的同步格式。为了满足这一需求， [ECMAScript 2016 (ES7)](https://www.ecma-international.org/ecma-262/7.0/index.html) 引入了`async`函数和`await`关键字，使处理承诺变得更加容易。

# 带`async/await`的异步功能

一个`*async*` *函数*允许你以一种看似同步的方式处理异步代码。`async`函数仍然使用承诺，但是有更传统的 JavaScript 语法。在本节中，您将尝试这种语法的示例。

您可以通过在函数前添加`async`关键字来创建一个`async`函数:

```
// Create an async function
async function getUser() {
  return {}
}
```

虽然这个函数还没有处理任何异步的东西，但是它的行为与传统函数不同。如果您执行该函数，您会发现它返回一个带有`[[PromiseStatus]]`和`[[PromiseValue]]`的承诺，而不是返回值。

通过记录对`getUser`函数的调用来尝试一下:

```
console.log(getUser())
```

这将给出以下内容:

```
Output__proto__: Promise
[[PromiseStatus]]: "fulfilled"
[[PromiseValue]]: Object
```

这意味着你可以用`then`处理`async`函数，就像处理承诺一样。用下面的代码试试看:

```
getUser().then((response) => console.log(response))
```

对`getUser`的调用将返回值传递给一个匿名函数，该函数将该值记录到控制台。

运行该程序时，您将收到以下内容:

```
Output{}
```

一个`async`函数可以使用`await`操作符处理在它内部调用的承诺。`await`可以在`async`函数中使用，在执行指定的代码之前会一直等待，直到承诺完成。

有了这些知识，您可以使用`async` / `await`重写上一节的获取请求，如下所示:

```
// Handle fetch with async/await
async function getUser() {
  const response = await fetch('https://api.github.com/users/octocat')
  const data = await response.json() console.log(data)
}// Execute async function
getUser()
```

这里的`await`操作符确保在请求用数据填充之前`data`不会被记录。

现在，最终的`data`可以在`getUser`函数中处理，而不需要使用`then`。这是`data`测井的输出:

```
Outputlogin: "octocat",
id: 583231,
avatar_url: "https://avatars3.githubusercontent.com/u/583231?v=4"
blog: "https://github.blog"
company: "@github"
followers: 3203
...
```

最后，因为您在异步函数中处理已实现的承诺，所以您也可以在函数中处理错误。您将使用`[try](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)`/[/](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)`[catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)`模式来处理异常，而不是使用`then`的`catch`方法。

添加以下突出显示的代码:

```
// Handling success and errors with async/await
async function getUser() {
  try {
    // Handle success in try
    const response = await fetch('https://api.github.com/users/octocat')
    const data = await response.json() console.log(data)
  } catch (error) {
    // Handle error in catch
    console.error(error)
  }
}
```

如果程序接收到一个错误，它将跳到`catch`块，并将该错误记录到控制台。

现代的异步 JavaScript 代码通常用`async` / `await`语法处理，但是了解承诺如何工作是很重要的，尤其是当承诺能够提供用`async` / `await`无法处理的额外特性时，比如用`[Promise.all()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)`组合承诺。

**注意:** `async` / `await`可以通过使用[生成器结合 promises](https://www.digitalocean.com/community/tutorials/understanding-generators-in-javascript#asyncawait-with-generators) 来重现，为您的代码增加更多的灵活性。要了解更多，请查看我们的 JavaScript 教程中的[理解生成器。](https://www.digitalocean.com/community/tutorials/understanding-generators-in-javascript)

# 结论

因为 Web APIs 通常异步提供数据，所以学习如何处理异步操作的结果是 JavaScript 开发人员的一个重要部分。在本文中，您了解了主机环境如何使用事件循环来处理带有*堆栈*和*队列*的代码的执行顺序。您还尝试了三种处理异步事件成功或失败的方法，包括回调、承诺和`async` / `await`语法。最后，您使用了 Fetch Web API 来处理异步操作

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。***