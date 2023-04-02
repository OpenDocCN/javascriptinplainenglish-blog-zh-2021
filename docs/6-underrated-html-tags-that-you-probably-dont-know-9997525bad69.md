# 你可能不知道的 6 个被低估的 HTML 标签

> 原文：<https://javascript.plainenglish.io/6-underrated-html-tags-that-you-probably-dont-know-9997525bad69?source=collection_archive---------4----------------------->

## 没人谈论的不受欢迎的 HTML 标签。

![](img/ce884322a7e47ef2da742986c3f8b67c.png)

Photo by [Arif Riyanto](https://unsplash.com/@arifriyanto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

HTML 是一种非常重要的网络标记语言。它是你在互联网上看到的任何网页的框架。除此之外，它很容易学习，并且有很多有用的特性，你可以作为一个 web 开发者来使用。

如你所知，HTML 使用标签来创建网页的元素。有很多标签你需要知道。正因为如此，我们只学习重要的。然而，有一些被低估的 HTML 标签非常有用。

这就是为什么在这篇文章中，我们将看看那些不受欢迎的 HTML 标签。让我们开始吧。

# 1.字段集

标签`<fieldset>`允许你在一个表单中组合一组 HTML 元素。它在元素周围画一个方框。

`<fieldset>`所有主流浏览器都支持。除此之外，它还接受诸如 form 属性之类的属性，该属性指定字段集所属的表单。

下面是一个代码示例:

```
<form>
 **<fieldset>**
   <label for="fname">First Name:</label>
   <input type="text"><br><br>
   <label for="lname">Last Name:</label>
   <input type="text"><br><br>
   <input type="submit" value="Submit">
 **</fieldset>**
</form>
```

您可以查看下面的 Codepen 来查看输出:

Codepen by author.

正如你所看到的，标签`<fieldset>`将元素分组，并在它们周围画了一个边框。

# 2.图例标签

标签`<legend>`被用作`<fieldset>`元素的标题。如果您在 legend 标记内放置一些文本，它会将这些文本放在 fieldset 元素的边框内。

看看下面的例子:

```
<fieldset>
 **<legend>Awesome:</legend>** <label for="fname">First Name:</label>
   <input type="text"><br><br>
   <label for="lname">Last Name:</label>
   <input type="text"><br><br>
   <input type="submit" value="Submit">
 </fieldset>
```

请在下面的代码栏中查看:

Codepen by author.

如您所见，标签`<legend>`允许您将字段集标题放在字段集元素的边框内。您还可以添加一些 CSS，让它看起来对用户更有吸引力。

# 3.数据列表

`<datalist>`在 HTML 中是一个非常有用却被低估的标签。它允许你在一个 input 元素中创建一个下拉和可搜索的文本。

标签`<datalist>`为具有自动完成特性的输入元素提供了一个预定义的选项列表。您只需要使用标签`<option>`将选项列表放入元素`<datalist>`中。

看看下面的代码:

```
<input **list="fruits"**>**<datalist id="fruits">**
    <option value="Apple">
    <option value="Orange">
    <option value="Banana">
    <option value="Mango">
    <option value="Avocado">
  **</datalist>**
```

注意，`<datalist>` ID 必须等于输入的列表属性。

您可以在下面的代码栏中查看输出:

Codepen by author.

# 4.进度标签

标签`<progress>`允许你使用本地 HTML 轻松创建进度条。

这里有一个例子:

```
**<progress value="50" max="100">50%</progress>**
```

您只需要指定属性`value`中的值和最大值，该值在大多数情况下是 100。

请在下面的代码栏中查看:

Codepen by author.

# 5.仪表标签

标签`<meter>`允许我们在进度条中定义和高亮显示数量，而无需使用任何 JavaScript 或 CSS。

下面是代码示例:

```
<label>Low:<label>
**<meter min="0" max="100" low="30" high="75" optimum="80" value="25"></meter>**<label>Medium:<label>
**<meter min="0" max="100" low="30" high="75" optimum="80" value="50"></meter>**<label>High:<label>
**<meter min="0" max="100" low="30" high="75" optimum="80" value="80"></meter>**
```

您可以在下面的代码栏中查看输出:

Codepen by author.

# 6.细节标签

HTML 中的标签`<details>`允许我们添加额外的元素，我们可以在点击放入其中的元素`<summary>`后查看或隐藏这些元素。

这里有一个例子:

```
**<details>**
  <summary>HTML</summary>
  <p>HTML is also Awesome.</p>
**</details>**
```

现在，您可以单击 summary 元素来查看或隐藏该段落。请在下面的代码栏中查看:

Codepen by author.

你也可以添加更多的 CSS，让它看起来更吸引人。

# 结论

如你所见，所有这些标签都不受欢迎。不是所有的开发人员都使用它们，因为他们可能不知道它们。它们非常有用，可以让你在不需要 JavaScript 或 CSS 的情况下创造出令人惊叹的东西。

感谢您阅读这篇文章。希望你觉得有用。

**延伸阅读**

[](/7-useful-html-attributes-that-you-probably-dont-know-661784fe21e) [## 你可能不知道的 7 个有用的 HTML 属性

### 每个 web 开发人员都应该知道的强大的 HTML 属性。

javascript.plainenglish.io](/7-useful-html-attributes-that-you-probably-dont-know-661784fe21e)