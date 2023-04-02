# 如何用 JavaScript 获取整个文档的高度？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-height-of-the-entire-document-with-javascript-199a7e0a8299?source=collection_archive---------4----------------------->

![](img/ea1ceb18aab44134e138a0e3b246eeab.png)

Photo by [Cytonn Photography](https://unsplash.com/@cytonn_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们可能想用 JavaScript 获得整个文档的高度。

在本文中，我们将看看如何用 JavaScript 获得整个文档的高度。

# 获取文档的高度

要获得文档的高度，我们可以获得`scrollHeight`、`offsetHeight`或`clientHeight`属性的最大值。

例如，我们可以写:

```
const body = document.body;
const html = document.documentElement;const height = Math.max(body.scrollHeight, body.offsetHeight,
  html.clientHeight, html.scrollHeight, html.offsetHeight);
console.log(height)
```

根据使用的浏览器，文档可以存储在`document.body`或`document.documentElement`属性中。

`scrollHeight`是只读属性是对元素内容高度的度量，包括页面上不可见的区域。

`offsetHeight`是一个只读属性，以整数形式返回元素的高度，包括垂直填充和边框。

`clientHeight`是一个只读属性，是元素的内部高度，以像素为单位。

它包括填充，但不包括边框、边距和水平滚动条(如果有)。

因此，这两个值之间的最大值就是包含所有内容的文档高度。

# getBoundingClientRect 方法

我们还可以在文档元素上使用`getBoundClientRect`方法来获得它的高度。

为了使用它，我们写:

```
const body = document.body;
const html = document.documentElement;const height = Math.max(body.getBoundingClientRect().height, html.getBoundingClientRect().height);
console.log(height)
```

我们用`getBoundingClientRect`方法得到文档内容的高度。

它返回一个带有`height`属性的对象来获取文档内容的高度。

高度以像素为单位。

# 结论

通过 JavaScript，我们可以使用各种属性来获取文档的高度。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)