# 你可能不知道的 7 个有用的 HTML 属性

> 原文：<https://javascript.plainenglish.io/7-useful-html-attributes-that-you-probably-dont-know-661784fe21e?source=collection_archive---------2----------------------->

## 每个 web 开发人员都应该知道的强大的 HTML 属性。

![](img/da8c942ae0aee9cf2eed17acc0188ebb.png)

Photo by [Anthony Riera](https://unsplash.com/@frenchriera?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

HTML 是每个 web 开发人员必备的技能。不了解这种标记语言，就不能称自己是 web 开发人员。你在网上看到的每一个网站都是用 HTML 创建的，因为它有许多有用和强大的功能，作为开发人员，你可以从中受益，从而创建网页。尽管如此，HTML 也有一些属性，可以附加到元素或标签上，以便为 HTML 元素添加某些交互特性。

在本文中，我们将给出一些有用的 HTML 属性的列表，这些属性你可能还没有听说过。所以让我们开始吧。

# 1.接受

如你所知，HTML 允许你创建输入，你可以上传你的文件。除此之外，HTML 属性`accept`用于上传输入，以指定文件类型或用户可以上传到服务器的唯一格式。

例如，我们可以接受只上传`jpg`和`png`到我们的服务器。

这里有一个例子:

```
<input type="file" **accept=".jpg, .png"** >
```

您可以在下面的代码栏中查看:

Codepen by author.

# 2.多重

HTML 中的属性`multiple`可以附加到标签`<input>`和`<select>`上。它基本上允许用户输入多个值。

例如，我们也可以在 HTML 上传输入中使用属性`multiple`来允许用户上传多个文件。

下面是一个代码示例:

```
<input type="file" **multiple** />
```

# 3.内容可编辑

属性`contenteditable`用于使 HTML 内容在网页上可编辑。它基本上允许用户编辑属性为`contenteditable`的页面元素。

这里有一个例子:

```
<div>
      <h1> Employees: </h1>
      <ul **contenteditable="true"**>
        <li> 1\. John </li>
        <li> 2\. Mehdi </li>
        <li> 3\. James </li>
      </ul>
  </div>
```

上面的例子允许我们在网页上编辑员工列表。

您可以在下面的代码栏中查看:

Codepen by author.

# 4.[计] 下载

HTML 中的属性`download`指定当用户点击链接时，链接将被下载。此属性允许用户从您的网站下载文件。

这里有一个例子:

```
<div>
 <a href="index.html" **download="fileName"**>Download this</a>
</div>
```

你只需要在属性`download`上指定文件名，在`href`上指定文件路径。

您可以查看下面的 Codepen 示例:

Codepen by author.

# 5.翻译

属性`translate`用于告知内容是否应该翻译。它可以附加到所有的 HTML 标签上，因为它是一个全局属性。

例如，该属性可以用在文本徽标上，以便在页面被翻译成另一种语言时保持相同的品牌名称。

下面是代码示例:

```
<p **translate="no"**>Mehdi</p>
```

# 6.海报

属性`poster`用于在下载 HTML 视频时显示图像，或者在用户点击播放按钮之前显示图像。

下面是代码示例:

```
<video **poster="picture.jpeg"** controls>
   <source src="file.mp4" type="file/mp4">
   <source src="file.ogg" type="file/ogg">
</video>
```

图像将显示为视频的缩略图，直到您单击播放按钮。

# 7.模式

属性`pattern`允许您轻松地将正则表达式添加到表单内部的输入元素中。

我们还可以使用另一个属性`title`和这个属性`pattern`来帮助用户在输入中书写正确的文本形式。

下面是一个代码示例:

```
<form >
  <label for="input">Country Code:</label>
  <input type="text" id="input" **pattern="[A-Za-z]{3}"** title="Three letters country code.">
  <input type="submit">
</form>
```

为了更好地理解，您可以查看下面的 Codepen:

Codepen by author.

# 结论

正如您所看到的，HTML 属性非常有用，了解它非常重要。它们允许你给你的 HTML 元素添加额外的有用特性。这就是我鼓励你从其他资源中了解更多属性的原因。

感谢您阅读这篇文章。希望你觉得有用。

# 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，也可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*

*您可能还喜欢:*

[](/10-awesome-front-end-project-ideas-for-code-newbies-b0ba03dc0bd) [## 给代码新手的 10 个很棒的前端项目想法

### 有用的前端 web 开发项目，提高您的编码技能。

javascript.plainenglish.io](/10-awesome-front-end-project-ideas-for-code-newbies-b0ba03dc0bd)