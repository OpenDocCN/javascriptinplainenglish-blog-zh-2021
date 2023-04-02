# JavaScript 的亮点——类名、获取多个元素和样式

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-class-names-getting-multiple-elements-and-styling-facd3a5cb24f?source=collection_archive---------21----------------------->

![](img/cfd2b53a8300a7a3a6c65141b76e2ae3.png)

Photo by [Hannah Morgan](https://unsplash.com/@hannahmorgan7?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 添加类名

我们可以用 JavaScript 类名 API 给 HTML 元素添加一个类名。

例如，我们可以编写以下 HTML:

```
<img src="https://i.picsum.photos/id/23/200/300.jpg?hmac=NFze_vylqSEkX21kuRKSe8pp6Em-4ETfOE-oyLVCvJo" id="image" onClick="expand();">
```

然后我们可以编写下面的 CSS:

```
.big {
  width: 500px;
}
```

然后我们可以通过编写以下代码来添加`expand`函数:

```
const expand = () => {
  document.getElementById("image").classList.add('big');
}
```

`big`类的宽度设置为 500 像素。

在`expand`函数中，我们调用`class:ist.add`方法将`'big'`类添加到 ID 为`image`的元素中。

我们用`expand()`设置`onClick`属性，以便在单击图像时调用`expand`函数。

当我们点击图像时，图像将被展开。

# 交换图像

当我们将鼠标悬停在一幅图像上时，我们可以将它换成另一幅图像。

例如，我们可以编写以下 HTML:

```
<img src="https://i.picsum.photos/id/23/200/300.jpg?hmac=NFze_vylqSEkX21kuRKSe8pp6Em-4ETfOE-oyLVCvJo" id="image" onMouseover="swap(1);" onMouseout="swap(0)">
```

和下面的 JavaScript 代码:

```
const swap = (index) => {
  const images = [
    'https://i.picsum.photos/id/23/200/300.jpg?hmac=NFze_vylqSEkX21kuRKSe8pp6Em-4ETfOE-oyLVCvJo',
    'https://i.picsum.photos/id/25/200/300.jpg?hmac=ScdLbPfGd_kI3MUHvJUb12Fsg1meDQEaHY_mM613BVM'
  ]
  const image = document.querySelector('#image');
  image.src = images[index];
}
```

当我们将鼠标悬停在图像上时，会运行`swap(1)`表达式。

它被设置为`onMouseover`属性的值，所以当我们将鼠标悬停在图像元素上时，它就会运行。

如果我们将鼠标移出图像，那么运行`swap(0)`来显示原始图像。

这是因为`swap(0)`被设置为`onMouseout`属性的值。

# 设置样式

我们可以用`className`或`style`属性设置样式。

例如，我们可以编写以下 HTML:

```
<p>
  hello world
</p>
```

并编写以下 CSS:

```
.big {
  font-size: 2em
}
```

然后编写以下代码，用 JavaScript 使文本变大:

```
document.querySelector("p").classList.add("big");
```

我们用`document.querySelector`方法得到 p 元素。

然后我们用`classList.add`方法将`big`类添加到`p`元素中。

或者，我们可以将`style`属性设置为我们想要的值:

```
document.querySelector("p").style.fontSize = '2em'
```

`style.fontSize`属性与`font-size` CSS 属性相同。

然而，最好使用 CSS 和类名，因为这比用 JavaScript 设置样式要快。

此外，CSS 代码可重用性更高。

我们可以设置的其他`style`属性包括:

```
document.querySelector("p").style.cssFloat = "left";
```

将 CSS `float`属性设置为`left`。

我们可以通过编写以下代码来设置`visibility` CSS 属性:

```
document.querySelector("p").style.visibility = "hidden";
```

并且可以通过书写来设置边距:

```
document.querySelector("p").style.margin = "0 10px 0 10px;";
```

# 通过标记名定位所有元素

我们可以通过标签名获取所有元素。

这比用 ID 获取单个元素或者用给定的选择器使用`querySelector`获取第一个元素更方便。

例如，我们可以编写以下 HTML:

```
<p>foo.</p>
<p>bar.</p>
<p>baz.</p>
```

然后我们可以得到所有的`p`元素，并通过编写以下代码来遍历它们:

```
const pars = document.getElementsByTagName('p')
for (const p of pars) {
  p.style.fontFamily = "Verdana, Geneva, sans-serif";
}
```

我们获取`p`元素，然后用 for-of 循环遍历它们。

在循环体中，我们设置了`fontFamily`样式来改变文本的字体。

# 结论

我们可以用`classList.add`方法添加类名。

此外，我们可以获取元素，循环遍历它们并改变它们的样式。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**