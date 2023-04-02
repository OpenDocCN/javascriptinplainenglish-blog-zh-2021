# 如何用 JavaScript 在正文或文档中添加 Div 元素？

> 原文：<https://javascript.plainenglish.io/how-to-add-a-div-element-to-the-body-or-document-with-javascript-58164217992d?source=collection_archive---------5----------------------->

![](img/9784aa2e25e4f77ab69ab4db52550032.png)

Photo by [Jeffrey Keenan](https://unsplash.com/@youngjefferson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们经常想用 JavaScript 在网页的正文或文档中添加一个 div 元素。

在本文中，我们将研究如何用 JavaScript 向正文或文档添加 div 元素。

# 设置 document.body.innerHTML 属性

向`body`元素添加 div 元素的一种方法是设置`document.body.innerHTML`属性。

例如，我们可以写:

```
document.body.innerHTML += '<div>hello world</div>';
```

我们将`innerHTML`赋给一个带有 div 元素代码的字符串。

因此，我们将看到在主体中呈现的 div。

# 调用 document.createElement 方法

向`body`元素添加 div 的另一种方法是使用`document.createElement`方法。

`document.createElement`用于创建 div。

然后我们调用`document.body.appendChild`将它附加到`body`元素作为其子元素。

例如，我们可以写:

```
const elem = document.createElement('div');
elem.style.cssText = 'position: absolute; width: 100ppx; height: 100px; z-index:100; background: lightgreen';
elem.innerHTML = 'hello world'
document.body.appendChild(elem);
```

我们调用`document.createElement`来创建 div。

然后我们设置`elem.style.cssText`属性，用 CSS 给 div 添加一些样式。

接下来，我们给`innerHTML`属性赋值，在 div 中添加一些内容。

最后，我们用`elem`调用`document.body.appendChild`将 div 作为它的子元素添加到主体中。

# 结论

我们可以通过给`document.body.innerHTML`属性分配一个 HTML 字符串来将 div 添加到 web 页面的`body`元素中。

或者我们可以用`document.createElement`创建一个 div 元素，并用创建的 div 调用`document.body.appendChild`。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)