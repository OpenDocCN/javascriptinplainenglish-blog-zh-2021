# 如何用 JavaScript 检查一个元素是否存在于可见 DOM 中？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-an-element-exists-in-the-visible-dom-with-javascript-523692554402?source=collection_archive---------6----------------------->

![](img/7731973310bee366b935fb7c111995f7.png)

Photo by [Anne Nygård](https://unsplash.com/@polarmermaid?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须检查一个元素在 JavaScript 中是否可见。

在本文中，我们将看看如何用 JavaScript 检查一个元素是否存在于可见的 DOM 中。

# `document.body.contains`

我们可以使用`document.body.contains`方法检查一个元素是否是可视 DOM 的一部分。

例如，我们可以编写以下 HTML:

```
<div>
  hello world
</div>
```

然后我们可以通过编写以下代码来检查 div 是否在可见的 DOM 中:

```
const div = document.querySelector('div')
const isVisible = document.body.contains(div)
console.log(isVisible)
```

我们用`querySelector`获取元素，并将其传递给`contains`方法。

我们看到控制台日志记录了`true`，如果它在页面上可见的话。

`contains`可用于除 Internet Explorer 之外的任何设备。

# `document.`文档元素`.contains`

代替`document.body.contains`，我们可以使用`document.documentElement.contains`来做同样的检查。

例如，我们可以写:

```
const div = document.querySelector('div')
const isVisible = document.documentElement.contains(div)
console.log(isVisible)
```

对 div 进行检查。

我们应该得到和以前一样的结果。

# 检查 parentNode 属性

检查元素是否在可见 DOM 中的另一种方法是检查`parentNode`属性是否真实。

如果是，那么我们知道该元素在可见的 DOM 中。

例如，我们可以写:

```
const div = document.querySelector('div')
const isVisible = Boolean(div.parentNode)
console.log(isVisible)
```

我们只是将`div.parentNode`属性直接传递给`Boolean`函数，如果为真则返回`true`，否则返回`false`。

因此，如果我们有与第一个例子相同的 HTML，我们应该看到控制台日志是`true`。

# 检查 baseURI 属性

我们可以检查的另一个属性是在`baseURI`属性中，看一个元素是否在可视 DOM 中。

例如，我们可以写:

```
const div = document.querySelector('div')
const isVisible = Boolean(div.baseURI)
console.log(isVisible)
```

去做检查。

如果`div.baseURI`是真的，那么它就在 DOM 里。

否则就不是了。

# 结论

我们可以通过检查各种属性或使用`document.body.contains`或`document.documentElement.contains`方法来检查一个元素是否在可见的 DOM 中。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)