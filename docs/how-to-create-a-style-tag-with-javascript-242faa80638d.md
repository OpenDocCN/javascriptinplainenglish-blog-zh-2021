# 如何用 JavaScript 创建样式标签？

> 原文：<https://javascript.plainenglish.io/how-to-create-a-style-tag-with-javascript-242faa80638d?source=collection_archive---------9----------------------->

![](img/ba7be49e1deb2e518584bd4e3113b133.png)

Photo by [Joshua Reddekopp](https://unsplash.com/@joshuaryanphoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在网页中动态创建一个`style`标签。

在本文中，我们将看看如何用 JavaScript 动态创建一个`style`标签。

# 用 createElement 创建一个样式元素，用 appendChild 将它附加到 head 标签上

我们可以用`docuemnt.createElement`方法创建一个`style`元素，就像我们创建任何其他类型的元素一样。

然后我们可以通过编写以下代码将创建的元素附加到`head`标签上:

```
const style = document.createElement('style')
style.type = 'text/css';
style.textContent = 'h1 { color: green }';
document.head.appendChild(style)
```

我们用`document.createElement`创建`style`元素。

然后我们将它的`type`属性设置为`'text/css'`。

然后我们将`style`元素的`textContent`设置为我们想要的样式。

最后，我们调用`document.head.appendChild`将`style`元素作为子元素添加到`head`标签中。

我们现在可以添加以下 HTML:

```
<h1>
  hello
</h1>
```

我们知道 h1 文本是绿色的。

# `document.head.insertAdjacentHTML Method`

我们也可以使用`document.head.insertAdjacentHTML`方法将我们自己的 HTML 添加到`head`标签中。

这包括将一个`style`元素插入到`head`标签中。

为此，我们写道:

```
document.head.insertAdjacentHTML("beforeend", `
  <style>
    h1 { color :green }
  </style>
`)
```

我们传入`beforeend`以在结束的`head`标签前插入`style`元素。

所以我们得到了和以前一样的结果。

# 动态插入样式表

我们还可以动态插入 CSS 样式表。

例如，我们可以写:

```
const ss = document.createElement("link");
ss.type = "text/css";
ss.rel = "stylesheet";
ss.href = "https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/css/bootstrap.min.css";
document.head.appendChild(ss);
```

我们用`document.createElement`方法创建了`link`元素。

然后我们将`type`设置为`'text/css'`，使其引用一个 CSS 样式表。

`rel`将`rel`属性设置为`stylesheet`。

`href`将`href`属性设置为我们想要引用的 CSS 文件。

然后我们调用`document.head.appendChild`来追加 CSS。

现在，我们从应用程序中应用的引导样式表中获取样式。

# 结论

我们可以用 JavaScript 创建一个 style 元素或者动态添加一个 link 标签用 JavaScript 引用外部 CSS 来动态添加样式。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)