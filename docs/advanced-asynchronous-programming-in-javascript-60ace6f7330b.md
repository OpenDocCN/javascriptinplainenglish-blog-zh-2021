# JavaScript 中的高级异步编程

> 原文：<https://javascript.plainenglish.io/advanced-asynchronous-programming-in-javascript-60ace6f7330b?source=collection_archive---------4----------------------->

作为程序员，我们总有一天会面临这个问题:异步编程(也称为非阻塞编程)并不容易。幸运的是，JavaScript 是为数不多的能够很好地实现它的编程语言之一(至少从几年前开始)。这就是为什么我今天向您推荐一些比简单地发送 HTTP 请求并等待响应更高级的技术。

![](img/7c9045d4b5d82af0ef9b49e609fbb2f2.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

本文面向对 promises 和 async/await 语法有所了解并希望了解更多的 JavaScript 程序员。如果你理解起来有困难，我可以向你推荐 Mozilla 的课程。本文包含使用 [modern-async](https://github.com/nicolas-van/modern-async) 开源库的例子。你可能想知道我是这个库的创建者，所以它可能会影响我的观点。

# 进行多个异步操作

让我们从简单的开始，假设我们有一些无处不在的操作叫做`doSomething()`:

```
async function doSomething () {
  // we don't care what's in here
}
```

我们并不关心它有什么用。它可能会查询 REST API，等待用户执行操作，等等。我们唯一知道的是，它是一个异步函数，我们在调用它时必须使用`await`关键字。

打一次电话很容易。但是如果我们需要调用它 n 次呢？

我们可以简单地使用一个循环来实现:

```
for (let i = 0; i < 10; i += 1) {
  await doSomething()
}
```

精彩！我们刚刚编写了一个算法，以一种顺序的方式执行多个异步调用。每个异步操作将一个接一个地执行。

该算法将完美运行。但是如果我们不想等待每个异步操作完成呢？毕竟，如果我们唯一要做的事情就是等待，我们也可以并行执行多个调用。

这样做有一个众所周知的模式:

```
const promises = []
for (let i = 0; i < 10; i += 1) {
  promises.push(doSomething())
}
await Promises.all(promises)
```

这里的微妙之处在于，我们在调用`doSomething()`时不直接使用`await`。相反，我们收集函数返回的`Promise`对象(因为所有的异步函数都返回承诺),并且我们使用`Promise.all()`函数将我们的承诺列表收集到一个单独的列表中，当所有的子承诺被解析时，该列表将被解析。然后，我们可以在“超级承诺”上使用*wait*。

好的，那也可以。每个操作将与其他操作并行执行*。但是，如果我们没有一个代码示例在从 0 数到 9 时执行哑操作，那该怎么办呢？如果这是一个真实的用例，在迭代一个由用户填充的数组时执行耗费资源的 REST 查询，而这个数组可能包含成百上千个元素，那会怎么样呢？我们真的想并行处理数千个 REST 查询吗？实际上这不会发生，因为你的浏览器会拒绝执行太多的并行 HTTP 调用，反而会使你的代码崩溃。*

*因此，我们知道如何按顺序进行许多操作，也知道如何进行无限的并行操作。我们唯一怀念的是在有限的*并发性*下执行许多并行操作的能力。*

*不幸的是，这正是我们触及基本`Promise` API 极限的时候。当然，我们仍然会像使用`async/await`一样使用它，因为它们太棒了。但是我们需要一些帮助来制造更先进的东西。这就是为什么我将使用 [modern-async](https://github.com/nicolas-van/modern-async) 库:*

```
*import { forEachLimit } from 'modern-async'...const array = ... // our arrayawait forEachLimit(array, doSomething, 5)*
```

*`[forEachLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#forEachLimit)`类似于`[Array.forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)`的方法。唯一的区别是:*

*   *这是一个接受异步回调的异步函数。当执行完所有要求的异步操作后，它将返回。*
*   *它将并行调用它的异步回调多次，同时注意不要超过并发限制(这里是 5)。*

*这就是我们如何优化我们的代码来执行多个并行操作，同时避免探索极限或我们的资源尖叫“天空是极限！”。(…并认为不是)*

# *集合上更多的异步操作*

*我们已经看到 [modern-async](https://github.com/nicolas-van/modern-async) 库包含一个名为`[forEachLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#forEachLimit)`的类似于`[Array.forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)`的函数。但是还有很多其他有用的通用列表操作函数，比如`map()`或`find()`。*

*幸运的是，这个库包含了所有这些函数的异步替代品。以下是它们的列表:*

*   *`[everyLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#everyLimit)` 相当于`[Array.every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)`*
*   *`[filterLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#filterLimit)` 相当于`[Array.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)`*
*   *`[findLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#findLimit)`相当于`[Array.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)`*
*   *`[findIndexLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#findIndexLimit)`相当于`[Array.findIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)`*
*   *`[forEachLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#forEachLimit)`相当于`[Array.forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)`*
*   *`[mapLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#mapLimit)`相当于`[Array.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)`*
*   *`[reduce()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#reduce)`相当于`[Array.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)`*
*   *`[reduceRight()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#reduceRight)`相当于`[Array.reduceRight()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/ReduceRight)`*
*   *`[someLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#someLimit)`相当于`[Array.some()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)`*

*所有这些函数都有简化的等价物，以使常见用例更简短。在`[filterLimit()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#filterLimit)`的例子中，我们还有`[filterSeries()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#filterSeries)`(一个纯粹的顺序选择)和`[filter()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#filter)`(一个纯粹的并行选择，对并发性没有限制)。*

*这些函数应该能够满足集合操作和异步编程的大部分需求。*

# *等待呢？*

*有没有觉得现在的`[setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)`功能调用起来很无聊？让我们来看看对它的最小调用:*

```
*setTimeout(() => {
  ... // your code
}, 300)*
```

*最少的调用只有 3 行代码，你会发现调用一个新函数的缺点。当你习惯了`async/await`的时候，感觉有点老派和回调，不太符合那种语法。*

*`[modern-async](https://github.com/nicolas-van/modern-async)`还包含一个名为 [sleep()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#sleep) 的助手，用于说明:*

```
*import { sleep } from 'modern-async'await sleep(300)*
```

*虽然不多，但是拥有一个适合`async/await`范例的替代品总是有用的。*

# *轻松超时*

*回到我们的`doSomething()`函数。如果我们想为它的返回设定一个最长的时间，会发生什么呢？*

*我们可以使用我们刚刚看到的`setTimeout()`或`sleep()`函数来制作我们自己的解决方案，但是对于编码来说不会那么简单。*

*这就是为什么`[modern-async](https://github.com/nicolas-van/modern-async)`为名称为`[timeout()](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/global.html#timeout)`的对象提供了一个函数:*

```
*import { timeout } from 'modern-async'await timeout(doSomething, 5000)*
```

*该调用将执行与`doSomething()`完全相同的操作，除了异步操作将被限制为 5 秒(5000 毫秒)。如果超过该延迟，它将抛出一个`[TimeoutError](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/TimeoutError.html)`来代替。*

# *控制任何事情并发性的关键——无处不在的消息队列*

*在本文前面，我们已经看到了如何限制对集合执行的异步操作的并发性。让我们称之为“简单模式”，因为在现实世界中，你并不总是事先有一个好的操作列表。有些情况下，异步操作可以在任何时候触发(例如当用户执行一个动作时)。*

*在这些情况下，限制并发性的最佳通用解决方案被命名为[消息队列](https://en.wikipedia.org/wiki/Message_queue)。 [modern-async](https://github.com/nicolas-van/modern-async) 在`[Queue](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/Queue.html)`类中提供了该范例的实现。实际上，我们之前看到的所有允许限制并发性的工具都只是它上面的包装器。*

*下面是一个用法示例:*

```
*import { Queue } from 'modern-async'const myQueue = new Queue(3) // we will limit the concurrency to 3async function buttonClickHandler () { // let's imagine this
  // function is called when the user clicks a button const result = await myQueue.exec(doSomething)
  // do something with the result if you want
}*
```

*在这里，我们首先创建一个`[Queue](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/Queue.html)`对象，我们假设它对我们的应用程序是全局的。每当用户点击一个按钮，队列中就会安排一个对`doSomething()` 的异步调用。如果尚未达到并发性，它将立即启动。如果没有，那么一旦至少有一个槽被释放，它就会被执行(这意味着先前调度的异步操作已经完成)。这样，我们的用户就可以随心所欲地点击我们的按钮 Cookie 点击样式，它不会崩溃。*

*`[Queue](https://nicolas-van.github.io/modern-async/modern-async/1.0.2/Queue.html)`还提供了一种优先级机制，允许将一些任务放在队列中其他任务之前。*

# *最后一句话*

*正如我所说，异步编程并不容易。太多的程序员忽略了它的微妙之处，这常常会导致程序不稳定。虽然这篇文章可能被称为“高级”，但它是基于我作为前端和后端开发人员在处理非常传统的应用程序时的日常工作中遇到的真实需求。这些用例并不罕见，我认为更多的开发人员应该知道解决它们的解决方案。*

*你可能也想知道为什么我使用我自己创建的 [modern-async](https://github.com/nicolas-van/modern-async) 库来提供例子。实际上，还有更流行的库，比如 [Async.js](https://caolan.github.io/async) 。不幸的是，当我试图使用这些库时，我感到非常沮丧，因为它们中的大多数都很老派，不太适合新的`async/await`范式。由于我不太愿意回到回调地狱式的编码风格，我花时间做了一个很好的开源项目来解决我的问题。如果你有时间[的话，一个明星⭐on Github](https://github.com/nicolas-van/modern-async) 会很受欢迎😀。*