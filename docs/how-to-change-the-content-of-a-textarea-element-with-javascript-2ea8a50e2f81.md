# 如何用 JavaScript 改变一个 textarea 元素的内容？

> 原文：<https://javascript.plainenglish.io/how-to-change-the-content-of-a-textarea-element-with-javascript-2ea8a50e2f81?source=collection_archive---------5----------------------->

![](img/19d90fc326af0cb86e3ed4ce9c9c5fc9.png)

Photo by [Rohit D'Silva](https://unsplash.com/@rohitdsilva?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 改变文本区域元素的内容。

在本文中，我们将研究如何用 JavaScript 改变 HTML 文本区域元素的内容。

# 更改文本区域元素的 value 属性

我们可以通过设置文本区域元素的`value`属性的值来改变文本区域的内容。

例如，如果我们有下面的 HTML:

```
<textarea></textarea>
```

然后我们可以通过编写来设置文本区域的内容:

```
document.querySelector('textarea').value = 'hello world';
```

我们用`document.querySelector`方法选择文本区域。

然后我们给文本区域的`value`属性赋值。

因此，现在我们应该看到一个以“hello world”为内容的文本区域。

# 更改文本区域元素的 innerHTML 属性

文本区域元素的另一个属性是`innerHTML`属性，我们可以通过修改它来向文本区域元素添加内容。

例如，如果我们有下面的 HTML:

```
<textarea></textarea>
```

然后我们可以通过编写来设置文本区域的内容:

```
document.querySelector('textarea').innerHTML = 'hello world';
```

我们用`document.querySelector`方法选择文本区域。

然后我们给文本区域的`innerHTML`属性赋值。

因此，现在我们应该看到一个以“hello world”为内容的文本区域。

# 从 document.forms 属性中选择表单中的文本区域

如果我们的文本区域在一个表单元素中，那么我们可以通过表单中文本区域的`name`属性来获取文本区域。

例如，如果我们有以下形式:

```
<form name="form">
  <textarea name="textarea" rows="10" cols="60"></textarea>
</form>
```

然后，我们可以通过编写以下代码来分配表单中文本区域的`value`属性:

```
document.forms.form.textarea.value = 'hello world';
```

`form`和`textarea`分别是表单和`textarea` 元素的`name`属性的值。

因此，我们应该在文本区域看到“hello world”。

# 结论

如果在表单中，我们可以用`querySelector`或`document.forms`得到文本区域。

然后我们可以给`innerHTML`或`value`属性赋值来改变它的内容。