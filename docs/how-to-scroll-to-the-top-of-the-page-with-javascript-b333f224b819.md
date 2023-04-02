# 如何用 JavaScript 滚动到页面顶部？

> 原文：<https://javascript.plainenglish.io/how-to-scroll-to-the-top-of-the-page-with-javascript-b333f224b819?source=collection_archive---------7----------------------->

![](img/5fce3cc27c6bbc1e9ac5324a29402fa2.png)

Photo by [Thought Catalog](https://unsplash.com/@thoughtcatalog?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要以编程方式滚动到网页的顶部。

在本文中，我们将看看如何用 JavaScript 滚动到页面顶部。

# 用 JavaScript 滚动到页面顶部

我们可以用 JavaScript 的`window.scrollTo`方法滚动到页面的顶部。

例如，如果我们有下面的 HTML 代码:

```
<div></div>
<button>
  scroll to top
</button>
```

然后，我们可以用 JavaScript 创建一个内容页面，并通过编写以下代码使按钮滚动到页面顶部:

```
const div = document.querySelector('div')
const button = document.querySelector('button')
for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  div.appendChild(p)
}button.addEventListener('click', () => {
  window.scrollTo(0, 0);
})
```

我们用`querySelector`得到 div。

然后我们有一个 for 循环，它用`document.createElement`创建了一个`p`元素。

我们把`textContent`设定为。

然后我们调用`appendChild`将`p`元素添加到 div 中。

为了让按钮在我们点击时滚动到页面的顶部，我们在按钮上调用`addEventListener`。

在回调中，我们用 x 和 y 坐标分别调用`window.scrollTo`来滚动。

# 平滑滚动动画

我们可以在滚动时添加平滑的滚动动画。

为此，我们改为向`scrollTo`传递一个对象。

例如，我们可以写:

```
const div = document.querySelector('div')
const button = document.querySelector('button')
for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  div.appendChild(p)
}button.addEventListener('click', () => {
  window.scrollTo({
    top: 0,
    left: 0,
    behavior: 'smooth'
  });
})
```

我们传入一个带有`top`和`left`属性的对象来分别设置滚动到的 x 和 y 坐标。

此外，我们将`behavior`属性设置为`'smooth'`以使滚动动画平滑。

这更好地使页面直接跳转到顶部，而没有第一个例子中的`behavior`选项。

# 结论

我们可以使用`window.scrollTo`方法用 JavaScript 让页面滚动到顶部。

我们可以设置滚动到的位置，以及在滚动过程中是否显示动画。

*更多内容请看*[***plain English . io***](http://plainenglish.io)