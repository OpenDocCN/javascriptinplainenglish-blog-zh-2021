# 只用 HTML 就能做的 4 件了不起的事情

> 原文：<https://javascript.plainenglish.io/4-awesome-things-you-can-do-using-only-html-10ab13a245ef?source=collection_archive---------2----------------------->

## HTML 比你想象的更有用。在以下情况下不需要 JavaScript。

![](img/c3c3dd6fd222d31599076c273ec1f245.png)

Photo by [Jackson So](https://unsplash.com/@jacksonsophat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

HTML 是网络的头号标记语言。它允许我们轻松地为网页创建元素。您可以使用标签、属性、添加脚本等等。

如果我告诉你，只用 HTML 你就能创造出一些需要 JavaScript 代码的神奇的东西，那会怎么样？

在这篇文章中，我们将介绍一些仅使用 HTML 就可以轻松创建的强大功能。所以让我们开始吧。

# 1.颜色选择器

HTML 允许您通过给标签`<input>`一个类型为`"color"`的属性，使用标签`<input>`轻松创建一个颜色选择器。

下面是代码示例:

```
<label for="color-picker">Pick a color: </label>
**<input type="color"** id="color-picker"**>**
```

正如你在上面看到的，为了更好的可访问性，我们使用了标签`label`。这就是不使用任何 JavaScript 就可以轻松创建颜色选择器的方法。

下面是一个 Codepen 示例:

Pen by the author from [Codepen](https://codepen.io/)*(external link outside Medium)*.

# 2.自动刷新文档

是的，你可以在一段时间后使用 HTML 自动刷新文档。

您可以在 HTML 的 meta 标签中使用属性`http-equiv`来实现。

这里有一个例子:

```
<!DOCTYPE html>
<html>
<head>
  **<meta http-equiv="refresh" content="10">**
</head>
<body><h1>Auto refresh</h1>
<p>Will automatically refresh after 10s.</p></body>
</html>
```

正如你在上面看到的，我们在属性`content`中以秒为单位指定每次刷新后的时间。

Codepen 示例来检查它:

Pen by the author from [Codepen](https://codepen.io/)*(external link outside Medium)*.

如果它在这个框架上不起作用，您可以自己尝试看看结果。

# 3.显示和隐藏文本

在 HTML 中，有一种不用 JavaScript 就可以在网页上显示和隐藏文本的方法。

是的，它是通过使用标签`<details>`和`<summary>`实现的，如下所示:

```
**<details>**
  **<summary>**HTML**</summary>**
  <p>HTML is Awesome and powerful.</p>
**</details>**
```

现在通过点击 HTML，你可以显示和隐藏段落元素。

下面是一个 Codepen 示例:

Pen by the author from [Codepen](https://codepen.io/)*(external link outside Medium)*.

# 4.下拉列表和可搜索文本

我们可以只用 HTML 在输入中创建一个下拉和可搜索的文本。

标签`<datalist>`允许我们这样做。它允许我们为具有自动完成功能的输入元素提供一个下拉选项列表。我们还可以搜索输入中的元素。所有这些都只需要原生 HTML，不需要任何 JavaScript。

这里有一个例子:

```
<input **list="cars"**>**<datalist id="cars">**
    <option value="BMW">
    <option value="Mercedes">
    <option value="Ford">
    <option value="Lambo">
    <option value="Ferrari">
  **</datalist>**
```

正如您在上面看到的，您只需要标签`<datalist>`外的输入和标签内的元素列表`<option>`。

另外，请记住标签`<datalist>`的 ID 必须等于输入中列表属性的值。

您可以在下面的代码栏中查看输出:

Pen by the author from [Codepen](https://codepen.io/)*(external link outside Medium)*.

# 结论

这些是我们可以在不使用任何 JavaScript 的情况下在 HTML 中做的一些强大的事情。有了所有这些有用的 HTML 特性，您可以轻松地创建令人惊叹的东西，而不必用 JavaScript 编写代码。因此，您将节省更多的时间。

另外，感谢您阅读这篇文章。希望你觉得有用。

**延伸阅读:**

[](/5-common-css-mistakes-that-you-need-to-avoid-53e51ed98d04) [## 你需要避免的 5 个常见 CSS 错误

### 避免这些 CSS 错误来改进您的代码和样式。

javascript.plainenglish.io](/5-common-css-mistakes-that-you-need-to-avoid-53e51ed98d04) [](/6-websites-that-pay-developers-to-write-technical-articles-7f6c691b56b6) [## 6 个付钱给开发者写技术文章的网站

### 一些向你支付技术内容的出版物的列表。

javascript.plainenglish.io](/6-websites-that-pay-developers-to-write-technical-articles-7f6c691b56b6) 

*更多内容尽在*[plain English . io](http://plainenglish.io/)