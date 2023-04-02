# 如何用 JavaScript 获取屏幕、当前网页或浏览器窗口的大小？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-size-of-the-screen-current-web-page-or-browser-window-with-javascript-b6a28ad33f2?source=collection_archive---------12----------------------->

![](img/f02e688168cd2317bebe4477babba90e.png)

Photo by [Bruna Araujo](https://unsplash.com/@brucaraujo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我们想创建响应迅速的 web 应用程序，获得屏幕尺寸是很重要的。

因此，这是 JavaScript web 应用程序中经常进行的操作。

在本文中，我们将看看如何用 JavaScript 获得屏幕、网页或浏览器窗口的大小。

# 使用 window.screen 对象获取屏幕尺寸

`window.screen`对象让我们分别用`height`和`width`属性获得浏览器屏幕的高度和宽度。

例如，我们可以写:

```
console.log(window.screen.height,
  window.screen.width)
```

以获取应用程序当前所在屏幕的高度和宽度。

# 窗口 innerWidth 和 innerHeight 属性

`window.innerWidth`和`window.innerHeight`属性让我们获得当前显示应用程序的框架的宽度和高度。

它不包括框架外的任何东西的尺寸，如工具栏等。

例如，我们可以写:

```
console.log(window.innerWidth, window.innerWidth)
```

记录框架的宽度和高度。

# 窗口 outerWidth 和 outerHeight 属性

`window.outerWidth`和`window.outerHeight`属性让我们获得当前显示应用程序的框架的当前宽度和高度。

它包括整个框架的尺寸，包括工具栏和滚动条。

例如，我们可以写:

```
console.log(window.innerWidth, window.innerWidth)
```

用工具栏和滚动条记录框架的宽度和高度。

# 使用 window.screen 对象获取屏幕的可用空间

我们可以使用`window.screen`对象通过`availWidth`和`availHeight`属性获得屏幕的可用空间。

例如，我们可以写:

```
console.log(window.screen.availWidth, window.screen.availHeight)
```

获取浏览器可用的屏幕宽度和高度。

因此，操作系统的菜单栏和任务栏的尺寸将从屏幕分辨率中减去。

# 从文档对象获取屏幕尺寸

同样，我们可以从`document`对象中获得屏幕的尺寸。

例如，我们可以写:

```
console.log(document.body.clientWidth, document.body.clientHeight)
```

获取`body`元素的宽度和高度。

`clientWidth`由 CSS 宽度+CSS 填充-垂直滚动条的高度计算得出。

`clientHeight`由 CSS height+CSS padding-水平滚动条的高度计算得出。

# 结论

用 JavaScript 有几种方法可以获得屏幕或浏览器窗口的尺寸。

*更多内容看*[***plain English . io***](http://plainenglish.io)