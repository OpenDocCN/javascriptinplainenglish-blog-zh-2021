# 如何避免带有 JavaScript 代码的浏览器弹窗拦截器？

> 原文：<https://javascript.plainenglish.io/how-to-avoid-browser-popup-blockers-with-javascript-code-15c32b811dcc?source=collection_archive---------3----------------------->

![](img/988bbd3bb96ffdc876f73392a9343b0f.png)

Photo by [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时当我们试图用`window.open`方法打开一个窗口时，我们可能会看到浏览器权限弹出窗口，要求打开由`window.open`创建的弹出窗口。

在本文中，我们将研究如何在 JavaScript 代码中避免浏览器弹出窗口拦截器。

# 避免在异步函数中调用 window.open

为了避免打开弹出窗口的权限弹出窗口，我们应该避免在返回承诺的函数中调用`window.open`，或者在回调函数中调用`setTimeout`、`setInterval`或任何其他异步函数。

这是因为，只有在没有用户直接操作许可的情况下，才能从应用程序打开弹出窗口。

调用链的深度也很重要，因为一些老的浏览器需要权限，而不是由用户动作后立即运行的函数调用。

因此，我们应该在作为直接用户操作结果运行的同步函数中调用`window.open`,以避免弹出权限弹出窗口在任何浏览器中显示。

我们可以通过检查`window.open`是否返回`null`或`undefined`来检查一个弹出窗口是否被阻止。

例如，我们可以通过编写以下代码来检查弹出窗口是否被阻止:

```
const pop = (url, w, h) => {
  const popup = window.open(url, '_blank', 'toolbar=0,location=0,directories=0,status=1,menubar=0,titlebar=0,scrollbars=1,resizable=1,width=500,height=500');
  return popup !== null && typeof popup !== 'undefined'
}
console.log(pop('https://example.com'))
```

我们调用`window.open`,将`url`作为第一个参数，将带有一些设置的字符串作为第三个参数。

那么我们返回的是`popup`不是`null`并且`popup`不是`undefined`。

如果弹出窗口打开，那么`popup`不应该是`null`也不应该是`undefined`。

因此如果弹出窗口打开，`pop`应该返回`true`。

# 结论

我们可以通过在同步函数中调用`window.open`来避免浏览器弹出窗口拦截器。

*更多内容请看*[***plain English . io***](http://plainenglish.io)