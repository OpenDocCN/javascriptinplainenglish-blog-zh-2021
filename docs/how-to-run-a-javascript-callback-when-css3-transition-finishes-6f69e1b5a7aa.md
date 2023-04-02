# CSS3 过渡完成后如何运行 JavaScript 回调？

> 原文：<https://javascript.plainenglish.io/how-to-run-a-javascript-callback-when-css3-transition-finishes-6f69e1b5a7aa?source=collection_archive---------13----------------------->

![](img/05809190802eba627e2a9a73b55fa77a.png)

Photo by [Chelsea Scott](https://unsplash.com/@chelseanscott?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在 CSS 转换完成时运行 JavaScript 代码。

在本文中，我们将研究如何在 CSS3 转换完成时运行 JavaScript 回调。

# 听 transitionend 事件

为了在 CSS3 转换完成时运行 JavaScript 代码，我们可以监听`transitionend`事件。

例如，如果我们有下面的 HTML:

```
<div id="my-div">Click me to start animation.</div>
```

和下面的 CSS:

```
#my-div {
  transition: top 2s;
  position: relative;
  top: 0;
}div {
  background: #ede;
  cursor: pointer;
  padding: 20px;
}
```

然后，我们可以添加一个 click 事件侦听器来应用转换，并在转换完成时通过编写以下代码来更新 div 的内容:

```
const myDiv = document
  .getElementById("my-div")myDiv
  .addEventListener("transitionend",
    () => {
      myDiv.innerHTML = "transition event ended";
    })myDiv
  .addEventListener('click', () => {
    myDiv.style.top = '55px'
  })
```

首先，我们有 ID 为`my-div`的 div 和`document.getElementById`。

然后我们用`'transitionend'`字符串调用返回的 div 上的`addEventListener`来添加一个`transitionend`事件监听器。

在事件处理函数中，我们将其`innerHTML`更新为`'transition event ended'`。

然后我们向同一个 div 添加一个`click`事件监听器，将`top` CSS 属性设置为`'55px'`。

在 CSS 中，我们添加了一个`transition`属性，以便在更改`top`属性时添加一些过渡效果。

并且效果会持续 2 秒。

现在，当我们单击 div 时，它会侧朝下。文本内容将变为“转换事件结束”，因为`transitionend`事件监听器已运行。

# 结论

当 CSS3 转换结束时，我们可以监听`transitonend`事件来运行 JavaScript 代码。

*更多内容看* [***说白了. io***](http://plainenglish.io)