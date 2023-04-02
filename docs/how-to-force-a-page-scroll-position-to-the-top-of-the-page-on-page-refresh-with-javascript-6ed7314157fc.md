# 如何用 JavaScript 在页面刷新时强制一个页面滚动位置到页面顶部？

> 原文：<https://javascript.plainenglish.io/how-to-force-a-page-scroll-position-to-the-top-of-the-page-on-page-refresh-with-javascript-6ed7314157fc?source=collection_archive---------8----------------------->

![](img/b4cd72ec11313ad0fa542069128c17df.png)

Photo by [Marc Pell](https://unsplash.com/@blinky264?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

默认情况下，页面的滚动位置在我们刷新页面后保持不变。

有时，我们希望在刷新页面时强制页面滚动到顶部。

在这篇文章中，我们将看看如何在刷新页面时强制页面滚动到顶部。

# 侦听 beforeunload 事件并使用 scrollTo 方法

为了在页面刷新时运行代码，我们可以监听`beforeunload`事件。

然后在`beforeunload`事件处理程序中，我们调用`scrollTo`方法在页面刷新时滚动到页面顶部。

例如，如果我们有下面的 HTML:

```
<div></div>
```

然后我们可以写:

```
const div = document.querySelector('div')
for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}window.onbeforeunload = () => {
  window.scrollTo(0, 0);
}
```

用`document.createElement`方法和`appenndChild`方法在 div 中添加一些元素。

然后我们将`window.onbeforeunload`属性设置为一个用 0 和 0 调用`window.scrollTo`的函数，以滚动到顶部。

现在，当我们刷新页面时，我们滚动到页面的顶部。

# 结论

当我们刷新页面时，我们可以通过使用监听器监听`beforeunload`事件并调用`scrollTo` ibn 事件监听器来强制页面滚动到顶部。

*更多内容请看*[***plain English . io***](http://plainenglish.io)