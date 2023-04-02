# 如何在现代浏览器中检测页面缩放级别

> 原文：<https://javascript.plainenglish.io/how-to-detect-page-zoom-levels-in-modern-browsers-bdb6404496b?source=collection_archive---------8----------------------->

![](img/92f8d6c51ad9d5e9568f543b0a305489.png)

Photo by [Charles Deluvio](https://unsplash.com/@charlesdeluvio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要检测现代浏览器中的页面缩放级别。

在这篇文章中，我们将看看如何在现代浏览器中检测缩放级别。

# 使用 window.devicePixelRatio 属性

检测浏览器缩放级别的一种方法是使用`window.devicePixelRatio`属性。

例如，我们可以写:

```
window.addEventListener('resize', () => {
  const browserZoomLevel = Math.round(window.devicePixelRatio * 100);
  console.log(browserZoomLevel)
})
```

当我们放大或缩小时，会触发`resize`事件。

所以我们可以用`addEventListener`来听。

在事件处理程序回调中，我们得到了`window.devicePixelRatio`，它具有当前像素大小和常规像素大小之间的比率。

# 用外宽除以内宽

由于`outerWidth` 是以屏幕像素为单位测量的，而`innerWidth` 是以 CSS 像素为单位测量的，我们可以使用它们之间的比率来确定缩放级别。

例如，我们可以写:

```
window.addEventListener('resize', () => {
  const browserZoomLevel = (window.outerWidth - 8) / window.innerWidth;
  console.log(browserZoomLevel)
})
```

然后`browserZoomLevel`与我们放大或缩小的程度成正比。

# 结论

我们可以用`window.devicePixelRatio`属性或者`outerWidth`和`innerWidth`之间的比率来检测页面缩放级别。

*更多内容请看*[***plain English . io***](http://plainenglish.io)