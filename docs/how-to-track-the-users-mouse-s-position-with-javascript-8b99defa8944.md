# 如何用 JavaScript 追踪用户的鼠标位置？

> 原文：<https://javascript.plainenglish.io/how-to-track-the-users-mouse-s-position-with-javascript-8b99defa8944?source=collection_archive---------11----------------------->

![](img/0885345046f6bb1409e766d4b336084c.png)

Photo by [Ryan Stone](https://unsplash.com/@rstone_design?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 跟踪用户的鼠标位置。

在本文中，我们将看看如何用 JavaScript 跟踪用户的鼠标位置。

# 用 clientX 和 clientY 属性获取鼠标的位置

我们可以监听移动鼠标时触发的`mousemove`事件。

然后从`mousemove`事件对象中，我们可以使用`clientX`和`clientY`属性来获取鼠标光标在页面上的 x 和 y 坐标。

例如，我们可以写:

```
document.onmousemove = (event) => {
  const {
    clientX,
    clientY
  } = event
  console.log(clientX, clientY)
}
```

以像素为单位记录鼠标的 x 和 y 坐标。

我们设置一个事件处理函数作为`document.onmousemove`属性的值。

我们将事件监听器连接到`document`，因为我们想要监听页面上的鼠标移动。

该方法接受`event`参数，它是`mousemove`事件对象。

在事件处理函数中，我们获取`clientX`和`clientY`属性来获取鼠标光标在页面上的位置的 x 和 y 坐标。

我们还可以用`addEventListener`方法附加事件监听器。

例如，我们可以写:

```
document.addEventListener('mousemove', (event) => {
  const {
    clientX,
    clientY
  } = event
  console.log(clientX, clientY)
})
```

我们用`'mousemove’`调用`addEventListener`来监听`mousemove`事件。

然后我们用同样的方法得到鼠标光标的 x 和 y 坐标。

现在我们应该看到鼠标光标的 x 和 y 坐标被记录下来。

# 结论

我们可以使用`mousemove`事件对象的`clientX`和`clientY`属性来获取鼠标光标在页面上的 x 和 y 坐标(以像素为单位)。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)