# Node.js + Express 中的异步错误处理

> 原文：<https://javascript.plainenglish.io/node-express-async-error-handling-e12aa693d84d?source=collection_archive---------2----------------------->

## 使用异步/等待，避免`UnhandledPromiseRejection`和崩溃

![](img/3d256bc63fe9a50714954757a72e0034.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 概观

您应该在 Node.js Express APIs 中使用`async`和`await`关键字。但是您知道 Express 对完全同步代码和异步代码的错误处理是不同的吗？

Express 确实有些魔力，可以将错误路由到错误处理中间件，但是任何异步调用都会遇到问题。你见过可怕的`UnhandledPromiseRejection`错误吗？请继续阅读，了解其中的区别，并找到避免这些问题的简单解决方案。

*注意:这里已经表达了关于错误处理的坚实的* [*文档*](https://expressjs.com/en/guide/error-handling.html) *—在本文中我们将重点介绍* `*async*` */* `*await*` *关键字，这与它们的* `*Promise*` *例子的思路完全相同。*

最终代码可以在我的回购协议中找到，在这里:

[](https://github.com/neightjones/express-async-errors) [## 邻居/快速异步错误

### 这个 repo 与我的关于使用 async / await 进行快速错误处理的博文一起发布。相关代码在…

github.com](https://github.com/neightjones/express-async-errors) 

这个代码库非常简单，只是为了这些例子而制作的——所有相关的代码都在`src/app.js`中。在现实生活中，一个项目将包含一个更复杂的结构来分离不同的关注点。

我在这里构建了我的[模板，其中设置了 Babel 和其他工具。我在这里写了设置](https://github.com/neightjones/node-babel-template)[这里写了](https://medium.com/javascript-in-plain-english/a-minimal-node-js-express-babel-setup-part-1-6be7b3f3bb55)和[这里写了](https://medium.com/javascript-in-plain-english/a-minimal-node-js-setup-part-2-eslint-prettier-vs-code-7963768dbb30)。

# 快速同步与异步错误处理

正如 [Express 提到的](https://expressjs.com/en/guide/error-handling.html)，同步和异步代码产生的错误是有区别的:

对于同步:

```
"Errors that occur in synchronous code inside route handlers and middleware require no extra work. If synchronous code throws an error, then Express will catch and process it."
```

但是，对于异步:

```
"For errors returned from asynchronous functions invoked by route handlers and middleware, you must pass them to the next() function, where Express will catch and process them."
```

所以……在异步情况下，Express 不会神奇地为我们做任何事情——我们需要确保捕捉到任何错误，并将它们传递给`next()`函数。

# 我们的错误处理器

在 Express APIs 中，错误处理中间件与其他中间件非常相似，但是它有 4 个参数。第一个参数代表一个错误，所以我们称之为`err`。

重要的是，错误处理器中间件应该放在路由处理器和其他中间件的 之后的 ***。您可以有多个错误处理程序来捕捉类似于`404`的事件，并处理其他特定的情况，但是出于讨论的目的，我们将坚持使用一个无所不包的错误处理程序。***

它看起来像这样，放在`app.js`文件的末尾:

```
app.use((err, req, res, next) => {
  // Simple error handling here... in real life we might
  // want to be more specific
  console.log(`I'm the error handler. '${err.message}'`);
  res.status(500);
  res.json({ error: err.message });
});
```

# 我们的模拟异步函数

对于我们下面的异步例子，我们想要一个`async`函数，我们可以在我们的路由中`await`。这个函数将模拟现实生活中的异步调用，如网络调用或数据库调用。我们称它为`asyncFn`:

```
const asyncFn = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject(new Error('Async Fn error!'));
    }, 1000);
  });
};
```

注意，这总是一个被拒绝的承诺(等待 1 秒钟后)。因为我们正在测试错误处理，所以我们将总是从这里用`new Error`拒绝。

# 同步端点测试

在我们的异步测试之前，让我们做一个简单的同步例子。我们的第一个端点看起来像这样:

```
/**
 * I throw an error in simple, synchronous code.
 * Express will automatically pass this error to our
 * error handler middleware (down at bottom).
 */
app.get('/sync-test', (req, res) => {
  throw new Error('Error from synchronous code!');
});
```

使用以下工具对此进行测试:

```
curl localhost:3000/sync-test
```

由于这是导致错误的同步代码`throw`，我们可以确认 Express 会自动将错误传递给我们的错误处理程序。确实如此，所以`curl`从状态为`500`的错误处理程序获得预期的 JSON 响应:

```
{"error":"Error from synchronous code!"}
```

对于 Express 来说，同步错误很容易发生。

# 测试 1。

让我们试试异步端点:

```
/**
 * I'm an async route handler (see my 'async' keyword).
 * When I try awaiting asyncFn defined above, what'll happen
 * with that error? Express WON'T automatically pass the error
 * to our error handler defined below! :0
 * This leads to the fateful UnhandledPromiseRejection.
 */
app.get('/async-test-1', async (req, res) => {
  await asyncFn();
  res.json({ well: `We're not going to reach this line.` });
});
```

1.  `async`关键字用于处理函数中。
2.  处理函数`await`是我们的测试`asyncFn()`——我们已经知道它会一直失败/拒绝。

试一试:

```
curl localhost:3000/async-test-1
```

这不好…你会在服务器日志中看到`Timeout`或`UnhandledPromiseRejection`问题，以及来自客户端服务器的空回复。您的服务器可能会崩溃。

由于这个端点会导致一个异步错误，Express **不会自动将这个错误传递给我们的错误处理程序！**

我们必须小心避免这些。代码看起来非常类似于 sync 的情况，但是结果却非常不同。

# 测试 2。

如果您熟悉`async` / `await`语法，您可能已经使用过`try` / `catch`来处理错误。让我们将其添加到下一个端点:

```
/**
 * This is like the async test above, but now we're using the
 * try...catch syntax to catch the async error. Then, we
 * can call 'next' to forward the error to our error handler.
 * We need to do this for async errors!
 */
app.get('/async-test-2', async (req, res, next) => {
  try {
    await asyncFn();
    res.json({ well: `We're not going to reach this line, either.` });
  } catch (e) {
    // This time, we'll catch the error and pass it along
    // to our error handler, below.
    next(e);
  }
});
```

尝试一下:

```
curl localhost:3000/async-test-2
```

太好了！现在，您将看到错误在我们的错误处理程序中间件中得到正确处理，并且 JSON 被传播到客户端。

由对`asyncFn()`的注定调用导致的错误被捕获。我们只需要用`next(e)`显式地将错误(名为`e`)传递给我们的错误处理程序。

# 测试 3。

我们在之前的测试中修复了我们的异步问题，但是我不喜欢为每一个路由处理器编写`try` / `catch`语法。看看这个名为 [express-async-handler](https://www.npmjs.com/package/express-async-handler) 的包。这是一个很好的简单的包，为我们处理错误。看看我们的最终路线:

```
/**
 * The last code works pretty well, but do you really want
 * to wrap every route handler in a try...catch?
 * The express-async-handler package takes care of that for us!
 * So this code works equally as well as the above.
 * Look how we wrap our handler -
 */
app.get(
  '/async-test-3',
  asyncHandler(async (req, res) => {
    await asyncFn();
    res.json({ well: `We're *still* not going to reach this line.` });
  }),
);
```

这与上面的测试#2 基本上是相同的代码，但是我们抽象出了`try` / `catch`和`next`调用。您甚至可以在这里看到包中的[主代码](https://github.com/Abazhenov/express-async-handler/blob/master/index.js) —它使用 Promise 语法来`catch`一个错误，并根据需要将其传递给`next`。

# 结论

错误处理是 Express API 中的一个关键部分。除了避免崩溃和`UnhandledPromiseRejection`错误之外，您还需要让您的错误处理变得清晰和有洞察力，以了解用户遇到了什么问题。

如果你喜欢你在这里看到的，你可以考虑看看我的高级产品 [Sapling](https://sapling.dev/) ，它为你生成了一个全栈应用。您将获得的代码处理本文中概述的错误处理代码，以及处理 CRUD 功能、Auth0 和 Stripe 集成等。

*这篇文章最初是* [*发表在我的博客上，是关于 sapphire*](https://sapling.dev/blog/express-async-error-handling)*的，一个启动 JS 项目的工具。*