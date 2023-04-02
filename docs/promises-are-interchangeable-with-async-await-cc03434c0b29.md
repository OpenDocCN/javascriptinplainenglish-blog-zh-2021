# 如何在 JavaScript 中用 Async/Await 交换承诺

> 原文：<https://javascript.plainenglish.io/promises-are-interchangeable-with-async-await-cc03434c0b29?source=collection_archive---------5----------------------->

![](img/0bbae9534ecb2e4d4e835c0a675fdead.png)

Photo by [Christopher Robin Ebbinghaus](https://unsplash.com/@cebbbinghaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

来自我的[博客](https://fek.io/blog/promises-are-interchangeable-with-async-await)。

JavaScript 如此强大的原因之一是它处理异步行为的方式。从一开始，JavaScript 就使用回调作为处理可能需要一段时间才能完成的响应的方式，而不会阻止程序继续处理其他逻辑。

向数据库、文件系统或网络中检索或写入内容都是可能阻塞程序的例子。以下示例是对文件系统的读取请求，其结果通过回调进行处理:

# 承诺

ECMAScript 2015 中引入了承诺，作为能够使用更结构化的模式处理异步行为的另一种方式。回调的基本问题是，如果您必须一次处理多个回调，您的代码可能看起来像一棵回调树。Promises 有`then`和`catch`函数，可以调用它们来处理异步请求。如果你的承诺解决了另一个承诺，你可以接着再做一个`then`。

Chrome 中的`fetch` API 是一个承诺库的例子，它可以在一个请求中返回多个承诺。下面是一个用 JSON 响应处理 Rest API 的 fetch 请求示例:

# 异步和等待

Promise API 比传统的错误优先回调更优雅，但语法仍然很简洁，因为`then`和`catch`函数都是高阶函数，需要向它们传递另一个函数来处理 Promise 的完成。

通过采用`async`和`await`关键字，我们可以编写看起来同步的代码，但是我们可以继续使用承诺:

正如我们在上面的例子中看到的，我们已经用关键字`await`替换了`then`高阶函数。`await`关键字必须在用`async`关键字注释的函数内部使用。如果您使用 Deno 或 Node.js 15 或更高版本，您可以在程序的顶层使用`await`关键字，而不必在`async`函数中运行它。

# 定义新的承诺

我们可以通过创建新的承诺来定义一个承诺。Promise 的构造函数只需要一个高阶函数，带有两个参数，分别用于解析和拒绝。以下是延迟 1000 毫秒后返回字符串的承诺示例:

我们也可以重写这个来使用`async`和`await`，并承诺处理`setTimeout`。

# 摘要

从前面的例子中我们可以看出，承诺和`async`和`await`是可以互换的。