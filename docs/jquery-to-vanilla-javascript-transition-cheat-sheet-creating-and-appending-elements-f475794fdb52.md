# jQuery 到普通 JavaScript 转换备忘单-创建和附加元素

> 原文：<https://javascript.plainenglish.io/jquery-to-vanilla-javascript-transition-cheat-sheet-creating-and-appending-elements-f475794fdb52?source=collection_archive---------14----------------------->

![](img/ecf4409eeb7a2fa7c30917128127c46b.png)

Photo by [Pablo Merchán Montes](https://unsplash.com/@pablomerchanm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

浏览器中的普通 JavaScript 现在已经内置了 jQuery 的许多功能。

因此，我们不需要使用 jQuery 来做很多事情。

在本文中，我们将研究 jQuery 特性的普通 JavaScript 等价物。

# 创建元素

我们可以使用 jQuery 的`$`函数来创建元素。

例如，我们可以写:

```
$("<div/>");
$("<span/>");
```

分别创建 div 和 span。

为了用普通的 JavaScript 做同样的事情，我们使用`document.createElement`方法:

```
document.createElement("div");
document.createElement("span");
```

为了给创建的元素添加一些内容，我们可以设置`textContent`属性来添加文本。

也可以通过`appendChild`方法附着子节点。

要添加文本内容，我们写道:

```
const element = document.createElement("div");
element.textContent = "text"
```

为了添加子节点，我们可以写:

```
const element = document.createElement("div");
const text = document.createTextNode("text");
element.appendChild(text);
```

# 更新 DOM

在 jQuery 中，我们可以使用`text`方法来更新元素的文本内容。

例如，我们可以写:

```
$("div").text("New text");
```

要返回所选元素的文本内容，我们可以写:

```
$("div").text();
```

无争议地调用`text`。

要使用普通的 JavaScript 设置元素的文本内容，我们可以编写:

```
document.querySelector("div").textContent = "New text";
```

为了得到所选元素的文本内容，我们写道:

```
document.querySelector("div").textContent
```

在 jQuery 中添加一个新的子元素，我们使用`append`方法:

```
$(".search-result").append($("<div/>"));
```

我们用类`search-result`给元素添加了一个新的 div。

为了用普通的 JavaScript 做同样的事情，我们称之为`appendChild`:

```
const element = document.createElement("div");
document.querySelector(".search-result").appendChild(element);
```

我们用`createElement`创建 div，并将返回的元素传递到`appendChild`。

# 结论

我们可以创建文本节点和元素，并用普通的 JavaScript 轻松地将其附加到 DOM 中。