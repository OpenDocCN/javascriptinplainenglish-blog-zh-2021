# 如何检索一个 HTML 元素相对于浏览器窗口的位置？

> 原文：<https://javascript.plainenglish.io/how-to-retrieve-the-position-of-an-html-element-relative-to-the-browser-window-1398d1e994e0?source=collection_archive---------5----------------------->

![](img/ee3aa3824cd4dffb4cdfd28e0e833a3d.png)

Photo by [Aditi Gautam](https://unsplash.com/@aditi_gautam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

检索 HTML 元素相对于浏览器窗口的位置是我们在 JavaScript web 应用程序中经常要做的事情。

在本文中，我们将研究如何获取 HTML 元素相对于浏览器窗口的位置。

# `getBoundingClientRect Method`

HTML 元素节点对象可以使用`getBoundingClientRect`方法来获取元素的位置。

例如，如果我们有下面的 HTML:

```
<div>
  hello world
</div>
```

那么我们可以通过书写来称呼`getBoundingClientRect`:

```
const div = document.querySelector('div')
const rect = div.getBoundingClientRect();
console.log(rect.top, rect.right, rect.bottom, rect.left);
```

我们用`querySelecttor`得到 div 元素。

然后我们打电话给`getBoundingClientRect`来得到这个职位。

`left`和`top`有元素左上角的 x 和 y 坐标。

`right`和`bottom`有元素右下角的 x 和 y 坐标。

# 元素相对于整个页面的位置

我们必须添加`scrollX`和`scrollY`来获得元素相对于整个页面的位置。

例如，我们可以写:

```
const div = document.querySelector('div')
const getOffset = (el) => {
  const rect = el.getBoundingClientRect();
  return {
    left: rect.left + window.scrollX,
    top: rect.top + window.scrollY
  };
}console.log(getOffset(div));
```

`scrollX`返回文档当前水平滚动的像素数。

并且`scrollY`返回文档当前垂直滚动的像素数。

# `offsetLeft and` 偏置

`offsetLeft`和`offsetTop`让我们获得元素左上角相对于最近的父元素的位置。

对于块级元素，`offsetTop`，`offsetLeft`相对于`offsetParent`描述元素的边框。

对于行内元素，`offsetTop`，`offsetLeft`描述第一个边框的位置。

例如，我们可以这样使用它:

```
const div = document.querySelector('div')
console.log(div.offsetLeft, div.offsetTop);
```

# 结论

我们可以在 JavaScript 中获得一个具有各种属性的元素的位置。