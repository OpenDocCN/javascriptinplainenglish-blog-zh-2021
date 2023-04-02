# 异步 JavaScript 的传奇:Thunks

> 原文：<https://javascript.plainenglish.io/the-saga-of-async-javascript-thunks-3606f7de0123?source=collection_archive---------10----------------------->

![](img/0995a27251d9b01f48994fe4aeed385c.png)

# 介绍

上次我们谈到了[回调](https://medium.com/@romansarder/the-saga-of-async-javascript-callbacks-6f56b3490f4d)——一种看似容易理解的模式。我们今天要讨论的概念是进化的下一步，自然会扩展回调的能力。它还为我们带来了一个有趣的异步编程解决方案，最重要的是，它改变了我们的思维模式，迫使我们从不同的角度看待事物。这一次我想为你提供一个关于什么是**思维方式**的全面解释，以及它们如何帮助你更好地组织我们的代码。

# 那是什么鬼东西？

说真的，我希望知道为什么有人会用这个名字。但是玩笑归玩笑，thunks 在某些时候让我想知道我是如何在不知道 JavaScript 有多强大的情况下走了这么远。从同步的角度来看，thunk 本质上是一个**函数**,它可以返回一些值，并且不需要额外的输入。就这么简单。许多使用 React 的人可能知道一个非常棒的简单的库，叫做 [redux-thunk](https://github.com/reduxjs/redux-thunk) ，顾名思义，它是基于 thunks 的。但稍后会详细介绍。现在，让我们看一个同步 thunk 的简单例子:

```
function superCalculation() {
    return 9999 + 9999
}const outFirstThunk = function () {
    return superCalculation()
}const sum = thunk() // 19998
```

这里我们有一个名为`ourFirstThunk`的 thunk，它的值是一个**函数**，当它被调用时，它总是返回相同的值——out`superCalculation`的结果。

# 我们关心的部分

重要的是，这个 thunk 已经成为某个特定状态的包装器。在这种情况下，这是一个潜在的昂贵操作的结果。想象自己在老式胶片上拍摄一个美丽的瞬间。电影本身就是你的思维，被捕捉的瞬间是被包裹的状态。我们现在可以在我们的应用程序中传递这个“电影”,当我们想要提取状态时，我们只需通过调用 thunk 来“开发电影”并获取值。我们传递的不是状态本身，而是值的一个**表示**。模式允许我们方便地隐藏底层计算的细节，并提供一个公共接口。我们还设法**延迟**计算，直到我们真正需要它，现在有可能将这个操作注入到我们代码的不同部分。这也就是所谓的**懒铛**。

# 进行异步

当您考虑异步应用程序时，事情开始变得非常有趣。那么，如何描述异步 thunk 呢？在很大程度上，是一样的。这个函数不需要任何参数来完成它的任务**，除了回调的**。有趣的是，尽管回调模式有很多缺陷，但它还是在这里找到了用武之地。标准的同步实现没有考虑时间因素，我们已经看到回调能够很好地处理“未来值处理”。为什么不在这里也使用它呢？让我们将前面的例子扩展到异步 thunk:

```
function superCalculationAsync (callback) {
    setTimeout(() => {
        callback(9999 + 9999)
    }, 1000)
}const thunk = function (callback) {
    superCalculationAsync(callback)
}thunk((result) => {
    console.log(result) // 19998
})
```

我们现在有了一个`superCalculationAsync`函数，它通过使用`setTimeout`实用程序来模拟异步行为。然后我们创建一个`thunk`，它是一个接受回调的函数。这个回调被传递给`superCalculationAsync`函数来处理操作的结果。总体概念保持不变，除了回调开始帮助我们处理事情。尽管如此，我们最终还是得到了一个方便的容器，只要我们传递回调，就可以在应用程序的任何地方使用它。

# 懒惰 vs 渴望

我们设法将我们的同步 thunk 转换成异步 thunk。你会注意到我们的`superCalculationAsync`本身并没有马上执行。这是一个**懒 thunk** 。在提供回调之前，不会进行任何计算。让我们试着把这个例子再玩一会儿，想办法把它重写为**eager thunk**——它会尝试提前运行计算，并尝试立即给你返回结果。

```
const thunk = (function () {
    let thunkResult;
    let handleResult;
    superCalculationAsync(function (result) {
        if (handleResult) {
            handleResult(thunkResult) // result is not ready
        } else {
            thunkResult = result // result is ready
        }
    }) return function runThunk (callback) {
        if (thunkResult) {
            callback(thunkResult) // result is ready
        } else {
            handleResult = callback // result is not ready
        }
    }
})()
```

在开发一个热切的思维时，你偶然发现了两种可能的情况，你需要处理。第一种情况是在内部操作完成后调用【thunk，我们可以安全地返回结果。这是比较容易的部分，和我们到目前为止所做的没有什么不同。第二种情况需要考虑——调用了 thunk，但操作仍在进行。我们必须以某种方式连接我们程序的这两个分支。所提供的解决方案绝不是性能最好和最优雅的，但它完成了工作。这里，我们以两个互为镜像的`if`语句结束。如果底层计算已经完成，我们就用底层计算的结果调用用户的回调。如果没有，我们就直接注入提供的回调。客户端代码甚至不知道 thunk 可能需要时间来完成。

# 权力来自抽象

重点是——我们可以用回调重写同步示例，然后统一处理异步和同步 thunk。通过这样做，我们可以通过这种规范化有效地将自己从处理代码中的时间因素中解放出来。我们不必知道或关心价值是如何传递给我们的。我们第一次调用 thunk 并传递回调时，它可能会做大量的工作来获得预期的响应。这可能是一个 AJAX 请求，一个 CPU 密集型任务，或者任何其他可能需要一段时间的疯狂的事情。但是当我们第二次调用它的时候，它可能会决定记住返回值，然后马上给我们。使用我们的 thunks 的客户端代码不需要担心内部实现，只要它能够以相同的方式处理同步和异步代码。这是一大进步。我们已经制作了一个独立于时间的数据包装器。我们知道时间可能是我们的应用程序中最复杂的事情。

# 真实世界的例子

我已经提到过**redux-thunk**——redux 维护者自己推荐用来处理 redux 应用中副作用的库。它为我们提供了一个中间件，该中间件期望一个 thunk 或一个简单的动作对象，并相应地处理它们。它非常简单，创建中间件的主要函数只有 9 行代码。

```
function createThunkMiddleware(extraArgument) {
  return ({ dispatch, getState }) => (next) => (action) => {
    if (typeof action === 'function') {
      return action(dispatch, getState, extraArgument);
    } return next(action);
  };
}
```

代码非常简单，很可能根本不需要任何解释。这在概念上与我们上面讨论的 thunk 是一样的。唯一的区别是传递给我们的 thunk 的几个额外的参数— `dispatch`和`getState`，其中`dispatch`起到了回调的作用。

# 简单

thunks 的伟大之处在于这只是纯 JavaScript 代码。不涉及任何库或框架。通过采用一种不同的思维方式，我们成功地消除了一种令人困惑和难以处理的东西——时间。让它沉一会儿。精神负担消失了，取而代之的是一个代表我们价值的公共界面。另外，我们能够毫无问题地在代码中重用这些表示。但是有一个新发现。

# 可怕的控制反转问题

我将立即发表这一声明——thunks 不是为解决控制反转问题而创建的。在异步编程的世界里，这并不是什么灵丹妙药。在上面的例子中， **redux-thunk** 库没有办法确保它们的`dispatch`函数会被适当地调用。我们的例子也是如此。thunks 有效地做的是，他们正在为**承诺**打下基础。如果你对承诺很熟悉，我敢肯定你们大多数人都很熟悉，你会注意到 thunks 本质上是没有花哨 API 的承诺。是的，我们得到了统一处理、可重用性和封装计算细节的良好包装的好处，但控制反转问题仍有待解决。此外，因为 thunks 仍然在幕后使用回调，所以您很容易得到与**回调地狱**非常相似的东西。如果我们试图表达几个相互之间有时间依赖关系的操作，这就变得很清楚了。假设我们有一个`makeThunk`实用程序，它接受一个函数和一个传递给它的参数列表。为了简单起见，我不会提供任何实现细节，你可以在互联网上找到很多。

```
const readFirst = makeThunk(readFile, 'first file');
const readSecond = makeThunk(readFile, 'second file');
const readThird = makeThunk(readFile, 'third file');readFirst((firstFileContents) => {
    console.log('first file contents', firstFileContents);
    readSecond((secondFileContents) => {
        console.log('second file contents', secondFileContents)
        readThird((thirdFileContents) => {
            console.log('third file contents', thirdFileContents)
        })
    })
})
```

我们首先预先创建三个 thunks 供以后使用。理解`readFile`直到我们通过回调才被执行是很重要的。在接下来的几行中，我们嵌套了 thunks 执行以获得正确的操作顺序。规则**时态依赖===嵌套**在这里也适用。

# 结尾部分

Thunks 对改进我们的 JavaScript 代码大有帮助。与回调相比，这种模式带来了几个重要的好处，并且仍然设法做到了轻量级和简单。最棒的是，这一切都可以通过函数的操作来实现。

正如我们在 redux-thunk 库示例中看到的，thunk 仅用 9 行代码就可以在 Redux a childsplay 中处理副作用。经过一些实践，您可以想象这种模式的功能远远超出了 React & Redux 应用程序的范围。Thunks 在意识形态上领先于 **Promise** 模式，这两者非常相似。虽然 thunks 没有成功解决控制反转的问题，但是我们将看到这个模式的概念核心是如何通过添加新的 API 最终成功的。感谢您的阅读，请关注更新，下次我们将讨论[承诺](https://medium.com/@romansarder/the-saga-of-async-javascript-promises-8ddef2477c24)。

*更多内容看* [***说白了. io***](http://plainenglish.io/)