# 如何用 JavaScript 替换 div 元素内部的文本？

> 原文：<https://javascript.plainenglish.io/how-to-replace-text-inside-a-div-element-with-javascript-fe1c01872301?source=collection_archive---------3----------------------->

![](img/a6c1149f30d8c29a5dc6e045199ab3b2.png)

Photo by [Jeremy Liem](https://unsplash.com/@jeremyliem5?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 替换 div 元素中的文本。

在本文中，我们将研究用 JavaScript 替换 div 元素中的文本的方法。

# 设置元素的 innerHTML 属性

用 JavaScript 替换 div 元素中的文本的一种方法是将元素的`innerHTML`属性设置为不同的值。

如果我们有下面的 HTML:

```
<div>
  hello world
</div>
```

然后我们可以写:

```
const div = document.querySelector('div')
div.innerHTML = "My new text!";
```

用`querySelector`选择 div。

然后我们可以将`innerHTML`设置为一个新的字符串。

# 设置元素的 textContent 属性

用 JavaScript 替换 div 元素中的文本的另一种方法是将元素的`textContent`属性设置为不同的值。

如果我们有下面的 HTML:

```
<div>
  hello world
</div>
```

然后我们可以写:

```
const div = document.querySelector('div')
div.textContent = "My new text!";
```

用`querySelector`选择 div。

然后我们可以将`textContent`设置为一个新的字符串。

然后我们得到和以前一样的结果。

# 将元素的 innerHTML 属性设置为空字符串，并向该元素插入一个新的子文本节点

替换 div 中文本的另一种方法是将`innerHTML`属性设置为空字符串。

然后我们可以添加一个新的文本节点，并将其插入到 div 中。

如果我们有下面的 HTML:

```
<div>
  hello world
</div>
```

然后我们可以写:

```
const div = document.querySelector('div')
div.innerHTML = '';
div.appendChild(document.createTextNode("My new text!"));
```

将`innerHTML`设置为空字符串。

然后我们调用`document.createTextNode`用参数中的文本创建一个新的文本节点。

然后我们调用`appendChild`将文本节点插入到 div 中。

# 结论

在 JavaScript 中，用新文本替换 div 元素中的文本有多种方法。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)