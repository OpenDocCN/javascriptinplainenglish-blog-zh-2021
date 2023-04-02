# 如何用 JavaScript 自动滚动到页面底部？

> 原文：<https://javascript.plainenglish.io/how-to-scroll-automatically-to-the-bottom-of-the-page-with-javascript-14241ab1b751?source=collection_archive---------6----------------------->

![](img/8c8689a9ab104ebb40ab1c47a4a964c1.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 自动滚动到页面底部。

在本文中，我们将看看如何用 JavaScript 自动滚动到页面底部。

# window.scrollTo 方法

我们可以使用`window.scrollTo`方法滚动到页面底部。

例如，我们可以编写以下 HTML:

```
<div></div>
```

然后我们通过书写来调用`window.scrollTo`:

```
const div = document.querySelector('div')
for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  div.appendChild(p)
}
window.scrollTo(0, document.body.scrollHeight);
```

我们用`querySelector`得到 div。

然后我们用`createElement`创建一些 p 元素，并用`appendChild`将它们添加到 div 中。

接下来，我们用 x 和 y 坐标分别调用`window.scrollTo`来滚动。

`document.body.scrollHeight`是 body 元素的高度，所以我们滚动到底部。

如果我们的滚动容器不是 body 元素，那么我们也可以从我们想要的任何元素中获取`scrollHeight`。

例如，我们可以写:

```
const div = document.querySelector('div')

for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  div.appendChild(p)
}window.scrollTo(0, div.scrollHeight);
```

我们使用 div 的`scrollHeight`而不是`document.body`。

我们得到了和以前一样的滚动效果。

# scrollIntoView 方法

我们可以使用`scrollIntoView`方法将屏幕滚动到它所调用的元素。

例如，我们可以写:

```
const div = document.querySelector('div')
for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  p.id = `el-${i}`
  div.appendChild(p)
}document.querySelector('#el-99')
  .scrollIntoView(false);
```

我们调用`scrollIntoView`滚动到 ID 为`el-99`的元素。

该参数指示我们是否要滚动到元素的顶部。

因为是`false`，我们没有滚动到元素的顶部。

此外，我们可以通过编写以下代码来更改滚动行为:

```
const div = document.querySelector('div')
for (let i = 0; i < 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  p.id = `el-${i}`
  div.appendChild(p)
}document.querySelector('#el-99')
  .scrollIntoView({
    behavior: 'smooth'
  });
```

我们传入一个将`behavior`设置为`'smooth'`的对象。

因此我们得到了平滑的滚动。

# 结论

我们可以使用 JavaScript 自动滚动到页面底部。

我们可以直接滚动到滚动容器的底部，也可以滚动到页面底部的一个元素。

*更多内容请看*[***plain English . io***](http://plainenglish.io)