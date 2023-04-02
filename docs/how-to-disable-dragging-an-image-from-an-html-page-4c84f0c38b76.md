# 如何禁用从 HTML 页面拖动图像？

> 原文：<https://javascript.plainenglish.io/how-to-disable-dragging-an-image-from-an-html-page-4c84f0c38b76?source=collection_archive---------5----------------------->

![](img/d38c893e3958394a9fbff27a0c48ae25.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望禁止从 HTML 页面拖动图像。

在本文中，我们将看看如何禁止从页面中拖动图像。

# 将 ondragstart 属性设置为返回 false 的函数

禁止从 HTML 页面拖动图像的一种方法是将图像元素的`ondragstart`属性设置为返回`false`的函数。

例如，如果我们有下面的 HTML:

```
<img src='https://i.picsum.photos/id/49/200/300.jpg?hmac=mC_cJaZJfrb4JZcnITvz0OOwLCyOTLC0QXH4vTo9syY'>
```

我们可以写:

```
const img = document.querySelector('img')
img.ondragstart = () => {
  return false;
};
```

将`ondragstart`设置为返回`false`的函数。

# 将指针事件 CSS 属性设置为“无”

另一种禁止拖动图像的方法是将`pointer-event` CSS 属性设置为`none`。

例如，如果我们有以下 HTML:

```
<img src='https://i.picsum.photos/id/49/200/300.jpg?hmac=mC_cJaZJfrb4JZcnITvz0OOwLCyOTLC0QXH4vTo9syY'>
```

然后，我们可以通过写入以下命令来禁用拖动:

```
img {
  pointer-events: none
}
```

# 将 draggable HTML 属性设置为 false

我们还可以将我们想要禁用拖动的`img`元素的`draggable` HTML 属性设置为`false`。

为此，我们写道:

```
<img draggable="false" src='https://i.picsum.photos/id/49/200/300.jpg?hmac=mC_cJaZJfrb4JZcnITvz0OOwLCyOTLC0QXH4vTo9syY'>
```

禁用拖动。

要用 JavaScript 做同样的事情，我们可以使用`setAttribute`方法:

```
const img = document.querySelector('img')
img.setAttribute("draggable", false);
```

我们分别用属性名和值调用`setAttribute`。

# 结论

有几种方法可以禁止用 HTML、CSS 或 JavaScript 拖动图像。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)