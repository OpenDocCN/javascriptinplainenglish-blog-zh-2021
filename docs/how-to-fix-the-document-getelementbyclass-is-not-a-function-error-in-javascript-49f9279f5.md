# 如何修复 JavaScript 中的“document.getElementByClass 不是函数”错误？

> 原文：<https://javascript.plainenglish.io/how-to-fix-the-document-getelementbyclass-is-not-a-function-error-in-javascript-49f9279f5?source=collection_archive---------4----------------------->

![](img/1c70502c7aaf35037d08041648c08824.png)

Photo by [Leonel Fernandez](https://unsplash.com/@leonelfdez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，当我们运行 JavaScript 代码时，我们可能会在控制台中遇到`“document.getElementByClass is not a function”`错误。

在本文中，我们将看看如何修复 JavaScript 代码中的`“document.getElementByClass is not a function”`错误。

# 正确的方法名是 document.getElementByClassName

我们用来获取具有给定类名的元素的方法的正确方法名是`document.getElementByClassName`方法。

例如，如果我们有下面的 HTML:

```
<div class='text'>
  foo
</div>
<div class='text'>
  bar
</div>
<p>
  baz
</p>
```

然后，我们可以通过编写以下代码获得 class 属性设置为`text`的所有元素:

```
const texts = document.getElementsByClassName("text");
console.log(texts)
```

我们用我们想要选择的元素的`class`属性值调用`document.getElementsByClassName`。

因此,`texts`是一个 HTMLCollection 对象，其中包含带有类`text`的 div。

# 结论

为了获得具有给定`class`属性值的所有元素，我们使用`document.getElementsByClassName`方法。

浏览器中没有`document.getElementsByClass`方法。

这将阻止我们在运行 JavaScript 代码时遇到`“document.getElementByClass is not a function”`错误。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)