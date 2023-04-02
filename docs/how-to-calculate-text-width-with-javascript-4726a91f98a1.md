# 如何用 JavaScript 计算文本宽度？

> 原文：<https://javascript.plainenglish.io/how-to-calculate-text-width-with-javascript-4726a91f98a1?source=collection_archive---------6----------------------->

![](img/a4c96f74b446fa5788b5e6e719aca6e1.png)

Photo by [Alexander Schimmeck](https://unsplash.com/@alschim?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须计算 JavaScript 代码中文本内容的宽度。

在本文中，我们将研究如何在 JavaScript 代码中计算文本内容宽度。

# 客户端高度和客户端宽度

HTML 元素对象的`clientHeight`和`clientWidth`属性让我们获得元素的高度和宽度。

因此，我们可以编写下面的 HTML:

```
<p id='text'>
  hello world
</p>
```

来创建元素。

然后，我们可以编写 JavaScript 编码器来获取元素的高度和宽度:

```
const fontSize = 12;
const text = document.getElementById("text");
text.style.fontSize = fontSize;
const height = text.clientHeight
const width = text.clientWidth
console.log(height, width);
```

我们用`getElementById`得到 p 元素。

然后我们使用`clientHeight`和`clientWidth`属性分别得到 p 元素的高度和宽度。

然后我们用控制台记录下来。

我们应该得到这样的结果:

```
18 222
```

从控制台日志中。

数字以像素为单位。

# Canvas.measureText 方法

HTML canvas 元素有一个`measureText`方法，让我们测量一段文本的大小。

这意味着我们可以将文本放入画布，然后调用它来测量其大小。

例如，我们可以写:

```
const text = 'hello world'
const font = "bold 12pt arial"
const canvas = document.createElement("canvas");
const context = canvas.getContext("2d");
context.font = font;
const {
  width
} = context.measureText(text);
console.log(width)
```

我们有分别包含文本内容和字体样式的`text`和`font`变量。

然后我们用`createElement`创建一个画布。

我们调用`getContext`来获取上下文。

接下来，我们用字体样式设置`font`属性。

然后我们用`text`变量调用`measureText`来测量`text`的大小。

我们从返回的对象中获取`width`属性。

我们应该会在控制台日志中看到类似 84.4453125 的数字。

数字也是以像素为单位的。

# 结论

我们可以用元素的`clientHeight`和`clientWidth`属性来测量文本大小。

此外，我们可以将文本放入画布，并使用`measureText`方法来测量文本宽度。