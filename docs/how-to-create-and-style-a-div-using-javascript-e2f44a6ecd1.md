# 如何使用 JavaScript 创建和样式化 div？

> 原文：<https://javascript.plainenglish.io/how-to-create-and-style-a-div-using-javascript-e2f44a6ecd1?source=collection_archive---------4----------------------->

![](img/619661c19af6bec5d1150cfe16f8a030.png)

Photo by [David Lezcano](https://unsplash.com/@_thedl?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在许多情况下，我们希望在 web 应用程序中动态地创建 div 元素并设置其样式。

在本文中，我们将了解如何使用 JavaScript 创建和样式化 div。

# 使用 document.createElement 方法

我们可以使用`document.createElement`方法创建一个 HTML 元素。

要使用它，我们只需将想要创建的元素的标记名作为字符串传递。

例如，我们可以写:

```
const div = document.createElement("div");
div.style.width = "100px";
div.style.height = "100px";
div.style.background = "red";
div.style.color = "white";
div.innerHTML = "Hello";document.body.appendChild(div);
```

要创建一个 div，对其进行样式化，并将其作为`body`元素的子元素追加。

`createElement`返回元素对象。

然后我们可以设置`style`属性的属性来应用各种样式。

所有的 CSS 属性都在`style`属性的 camel case 中。

`innerHTML`设置 HTML 元素的内容。

# 设置 document.body 的 innerHTML 属性

我们还可以用 HTML 代码将`document.body`的`innerHTML`属性设置为一个字符串，以便向`body`元素添加内容。

例如，我们可以写:

```
const div = '<div>hello</div>';
document.body.innerHTML = div;
```

将 div 的`innerHTML`属性设置为我们想要的。

# 结论

我们可以使用`document.createElement`方法创建一个 div。

然后我们可以通过给属性`style`赋值来设置样式。

*更多内容请看*[***plain English . io***](http://plainenglish.io)