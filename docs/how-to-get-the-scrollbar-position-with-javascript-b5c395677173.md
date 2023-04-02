# 如何用 JavaScript 获取滚动条位置

> 原文：<https://javascript.plainenglish.io/how-to-get-the-scrollbar-position-with-javascript-b5c395677173?source=collection_archive---------9----------------------->

![](img/455f9d8926e6f8600e2205097aff8b2d.png)

Photo by [Aditi Gautam](https://unsplash.com/@aditi_gautam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，当我们在一个元素或页面上滚动时，我们可能想要得到滚动条的位置。

在本文中，我们将看看如何用 JavaScript 获得滚动条的位置。

# 使用元素的 scrollTop 属性

我们可以使用元素的`scrollTop`属性来获取因为滚动而隐藏的像素数量。

所以我们可以用它来获得滚动条的位置。

例如，我们可以编写以下 HTML:

```
<div></div>
```

然后，我们可以通过编写以下内容来监听滚动事件:

```
const div = document.querySelector('div')
for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}window.addEventListener('scroll', (e) => {
  console.log(document.documentElement.scrollTop);
})
```

我们用`document.querySelector`方法得到 div。

然后，我们通过调用`document.createElement`来创建元素，将 100 个 p 元素添加到 div 中。

并且我们通过设置`textContent`属性来设置每个的内容。

然后我们用`div.appendChild`方法将它添加到 div 中。

接下来，我们调用`window.addEventListener`，将`'scroll'`字符串作为第一个参数来监听滚动事件。

然后我们可以获取`documentElement`的`scrollTop`属性来获取`html`元素向下滚动了多远。

我们还可以得到其他元素的`scrollTop`属性。

例如，如果我们有:

```
<div style='height: 300px; overflow-y: auto'></div>
```

我们设置了`height`和`overflow-y`属性来使 div 可滚动。

然后我们可以通过编写以下内容来监听 div 的`scroll`事件:

```
const div = document.querySelector('div')
for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}div.addEventListener('scroll', (e) => {
  console.log(div.scrollTop);
})
```

我们像以前一样将内容添加到 div 中。

但是我们调用`div.addEventListener`而不是`window.addEventListener`来监听 div 的`scroll`事件。

然后我们获取`div.scrollTop`属性来获取 div 向下滚动了多远。

# 使用 window 对象的 scrollY 属性

还有一个属性`window.scrollY`可以让我们以像素为单位获取滚动条向下的距离。

例如，我们可以这样使用它:

```
const div = document.querySelector('div')
for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}window.addEventListener('scroll', (e) => {
  console.log(window.scrollY);
})
```

我们仍然监听`'scroll'`事件，但是我们得到的是`window.scrollY`属性而不是`document.documentElement.scrollTop`。

# 结论

有几种方法我们可以用 JavaScript 得到滚动条的位置。

*更多内容请看*[***plain English . io***](http://plainenglish.io)