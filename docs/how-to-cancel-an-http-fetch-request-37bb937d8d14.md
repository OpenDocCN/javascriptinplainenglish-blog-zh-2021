# 如何取消 HTTP 获取请求

> 原文：<https://javascript.plainenglish.io/how-to-cancel-an-http-fetch-request-37bb937d8d14?source=collection_archive---------13----------------------->

![](img/2475de33df630abfc2400930d5b73732.png)

JavaScript 承诺是该语言中异步编码的巨大催化剂。他们极大地改善了 web 开发的性能和体验。native promises 的一个缺点是，一旦发起了 HTTP fetch 请求，我们就不能取消它。但是现在有一种方法可以做到这一点。

DOM 标准中添加了一个名为 AbortController 的新控制器，允许我们将它用作取消 HTTP 获取请求的信号。它利用 AbortSignal 属性来实现这一点。

它是在 2017 年添加的，在大多数浏览器中都受支持(显然 IE 除外)。但是现在 IE 支持很快就要结束了，这可能是一件大事。

# 为什么我们需要取消一个 HTTP 获取请求？

在我们进入 how-to 部分之前，让我们先看看为什么我们需要取消一个 HTTP fetch 请求。

当我们有一个由多个组件组成的应用程序，这些组件可以动态地添加到 DOM 树中或者从 DOM 树中移除时，许多组件必然会发出 HTTP 请求。并且有可能在获取请求完成之前这些组件中的一个被卸载。在网速较慢的情况下，或者用户在页面间跳跃时，这种情况很常见。

因为 fetch 请求是异步的，所以它将继续在后台执行，如果处理不当，当它完成时可能会导致一些错误。

Chrome 的默认获取超时是 300 秒，Firefox 是 90 秒。在网络条件不可靠的情况下，这远远超过了用户希望等待的时间。因此，如果需要的话，我们肯定希望实现我们自己的方法来取消 HTTP 获取请求。

# 中止控制器和中止信号

AbortController 和 AbortSignal API 是由 [DOM 标准](https://dom.spec.whatwg.org/#aborting-ongoing-activities)提供的，并且保持了通用性，以便它们可以被其他 web 标准使用。要声明控制器:

```
const controller = new AbortController();
```

对于信号:

```
const signal = controller.signal;
```

控制器只有一种中止方法。当它被调用时，信号会得到通知。

```
controller.abort();
signal.addEventListener('abort', () => {
  console.log(signal.aborted); // true
});
```

# 如何中止 HTTP 获取请求？

fetch API 本身不允许以编程方式取消请求。但是它可以接受 AbortSignal 作为参数。然后，如果我们愿意，我们可以在特定的持续时间后中止获取请求。

```
const controller = new AbortController();
const signal = controller.signal;

fetch(url, { signal })
  .catch(err => {
    if (err.name === 'AbortError') {
      console.log('Fetch was aborted');
    }
  });

// Abort the request after 4s
// aborts the fetch with 'AbortError'
setTimeout(() => {
  controller.abort();
}, 4000);
```

如果需要，我们甚至可以创建自己的超时获取调用包装器:

```
async function cancellableFetch(url, data, timeout = 4000) {
  const controller = new AbortController();
  const timer = setTimeout(() => controller.abort(), timeout);

  const response = await fetch(url, {
    ...data,
    signal: controller.signal  
  });
  clearTimeout(timer);

  return response;
}
```

需要注意一些事情:

*   如果您将同一个信号传递给多个 fetch 调用，它会在 abort 上取消所有带有该信号的请求。因此，如果有多个请求需要在一个失败时中止，我们可以使用它。
*   由于控制器不可重用，如果我们不想在取消 HTTP 获取请求时中止所有获取，我们需要为所有获取创建一个新的控制器实例。
*   请求仅在客户端被中止。尽管客户端不会收到响应，但服务器可能仍然会处理它。
*   我们也可以使用 Promise.race 来实现这个功能，但是这个解决方案会让请求挂起，而不是中止请求。它会在后台继续消耗带宽。

这就是如何在超时后取消 HTTP 获取请求，或者以编程方式中止它。我很兴奋能够这样做，希望你也是。如果你打算使用这个，请在评论区告诉我。

*原载于 2021 年 1 月 19 日*[*【https://www.wisdomgeek.com】*](https://www.wisdomgeek.com/development/web-development/javascript/how-to-cancel-http-fetch-request/)*。*