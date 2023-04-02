# 如何通过类名移除 HTML 元素？

> 原文：<https://javascript.plainenglish.io/how-to-remove-html-elements-by-class-name-b0288988dd55?source=collection_archive---------15----------------------->

![](img/e40e8c980a8c279d5a850379d2d77f7b.png)

Photo by [Vlad Hilitanu](https://unsplash.com/@vladhilitanu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在 JavaScript 代码中通过类名删除 HTML 元素。

在本文中，我们将研究如何通过类名移除元素。

# 获取元素的父节点并对其调用 removeChild

我们可以获取元素的父节点，并在每个元素上调用`removeChild`来移除一个元素。

例如，如果我们有下面的 HTML:

```
<div>
  <p class='text'>
    foo
  </p>
  <p class='text'>
    bar
  </p>
  <p class='text'>
    baz
  </p>
</div>
```

然后我们可以写:

```
const text = document.querySelectorAll('.text')
for (const el of text) {
  el.parentNode.removeChild(el);
}
```

选择类别为`text`的所有元素。

然后我们使用 for-of 循环遍历每个元素。

在循环体中，我们用`parentNode`属性获取元素的父节点。

然后我们用`el`元素调用`removeChild`来移除它。

# 调用 remove 方法

元素对象也有`remove`方法让我们删除一个元素。

例如，如果我们有下面的 HTML:

```
<div>
  <p class='text'>
    foo
  </p>
  <p class='text'>
    bar
  </p>
  <p class='text'>
    baz
  </p>
</div>
```

然后我们可以写:

```
const text = document.querySelectorAll('.text')
for (const el of text) {
  el.remove();
}
```

移除用`remove`方法选择的每个元素。

# 结论

我们可以选择给定类中的所有元素，然后在 for-of 循环中逐个删除它们。

每个元件都可以用`remove`或`removeChild`方法移除。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)