# 如何用 JavaScript 添加 CSS 样式？

> 原文：<https://javascript.plainenglish.io/how-to-add-css-styles-with-javascript-c5c7ef8f77aa?source=collection_archive---------15----------------------->

![](img/25cc656f22659bf14f8373f0e72cb382.png)

Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 在网页中动态添加 CSS 样式。

在本文中，我们将研究用 JavaScript 动态添加 CSS 样式的方法。

# 使用 window.document.styleSheets 对象和 insertRule 方法

我们可以用`window.document.styleSheets`属性获得文档的第一个样式表。

然后我们可以在返回的样式表对象上调用`insertRule`方法。

例如，如果我们有下面的 HTML 代码:

```
<strong>hello world</strong>
```

然后我们可以通过编写以下代码使`strong`元素文本显示为红色:

```
const [sheet] = window.document.styleSheets;
sheet.insertRule('strong { color: red; }', sheet.cssRules.length);
```

我们使用析构语法从`window.document.styleSheets` iterable 对象中获取第一个样式表。

然后我们调用样式表对象上的`insertRule`,将 CSS 字符串作为第一个参数。

然后我们应该看到`strong`元素文本是红色的。

# 创建样式元素

用 JavaScript 添加 CSS 样式的另一种方法是使用`document.createElement`方法创建一个`style`元素。

例如，如果我们有下面的 HTML 代码:

```
<strong>hello world</strong>
```

然后我们可以通过编写以下代码来创建`style`元素:

```
const styleSheet = document.createElement("style")
styleSheet.type = "text/css"
styleSheet.innerText = 'strong { color: red; }'
document.head.appendChild(styleSheet)
```

我们用`'style'`调用`document.createElement`来创建一个`style`元素。

然后我们在产生的`styleSheet`对象上设置`type`属性。

然后我们将`innerText`属性设置为我们想要应用的 CSS 样式。

最后，我们用`styleSheet`调用`document.head.appendChild`，将我们创建的`style`元素添加到`head`元素中作为其子元素。

因此，我们应该得到和以前一样的结果。

# 结论

我们可以用 JavaScript 通过创建一个`style`元素来添加 CSS 样式，或者用 JavaScript 获得第一个样式表，并向其中添加我们想要的样式规则。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)