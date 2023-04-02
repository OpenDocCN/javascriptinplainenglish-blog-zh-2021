# 用 JavaScript 检查滚动条是否可见

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-scrollbar-is-visible-with-javascript-95aced8b420d?source=collection_archive---------13----------------------->

## 如何用 JavaScript 检查滚动条是否可见

![](img/406c9e6f757ccafe63880c84a7bdbf77.png)

Photo by [Dan-Cristian Pădureț](https://unsplash.com/@dancristianp?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要检查滚动条在我们的 JavaScript web 应用程序中是否可见。

在本文中，我们将看看如何用 JavaScript 检查滚动条是否可见。

# 比较 scrollHeight 和 clientHeight

HTML 元素的`scrollHeight`属性是一个只读属性，用于度量元素内容的高度。

它包括由于溢出而在屏幕上不可见的内容。

它是用像素来衡量的。

HTML 元素的`clientHeight`属性是一个只读属性，对于没有 CSS 或内联框架布局的元素为零。

它是内部高度的像素数，包括填充，但不包括边框、边距和水平滚动条。

因此，我们可以比较元素的`scrollHeight`和它的`clientHeight`来决定是否显示滚动条。

如果`scrollHeight`比`clientHeight`大，那么我们知道滚动条会被显示，因为会有溢出的文本。

例如，我们可以编写以下 HTML:

```
<p>
  hello world
</p><div style='height: 100px; overflow-y: auto'>

</div>
```

然后我们可以编写下面的 JavaScript:

```
const scrollbarVisible = (element) => {
  return element.scrollHeight > element.clientHeight;
}const p = document.querySelector('p')
const div = document.querySelector('div')for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}console.log(scrollbarVisible(p))
console.log(scrollbarVisible(div))
```

我们创建了`scrollbarVisible`函数来返回`element`的`scrollHeight`与其`clientHeight`的比较结果。

然后我们用`document.querySelector`得到 p 和 div 元素。

接下来，我们有一个 for 循环来创建 p 元素，并将它们作为 div 的子元素追加。

由于我们将 div 的高度设置为 100 像素，并将`overflow-y`设置为`auto`，所以我们可以滚动我们添加的内容。

最后，我们记录 p 和 div 元素上的`scrollbarVisible`函数的返回结果。

那么第一个控制台日志应该记录`false`，因为没有溢出的内容。

第二控制台日志应该记录`true`，因为有溢出的内容。

# 结论

为了检查一个元素是否有滚动条，我们可以比较`scrollHeight`值和它的`clientHeight`值，两者都是以像素为单位。

*更多内容请看*[***plain English . io***](http://plainenglish.io)