# 你应该避免的 5 个常见 HTML 错误

> 原文：<https://javascript.plainenglish.io/5-common-html-mistakes-that-you-should-avoid-bdbc28fe39d7?source=collection_archive---------4----------------------->

## 如果您想编写高质量的代码，请避免这些 HTML 错误。

![](img/02c575a5281c59a74ceccd1801605594.png)

Photo by [Avinash Murugappan](https://unsplash.com/@avinash27?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

HTML 是 web 开发的女王。这是每个 web 开发人员都必须知道的标记语言。它允许您通过在代码中使用标记和属性来轻松创建网页元素。

HTML 有很多很酷的特性，作为 web 开发人员，你可以从中受益。然而，编写语义和质量的 HTML 代码并不容易。有一些错误是很多开发人员没有注意到的。

这就是为什么在这篇文章中，我们将涵盖一些常见的 HTML 错误，每个开发人员都应该避免。所以让我们开始吧。

# 1.使用内嵌样式

许多开发人员在 HTML 中使用内联样式来减少他们的 CSS 文件。然而，这不是一个好的实践，因为它没有遵循分离关注点的设计原则。

你应该把你的程序分成多个部分。因此，在 JavaScript 文件中，始终只有结构(HTML)、样式(CSS)和功能。尽可能避免在 HTML 代码中使用内联样式。

*不好的做法:*

```
<h1 **style="color: #000"**>Hello World</h1>
```

*良好实践:*

```
h1{
 color: #000;
}
```

# 2.不使用图形标签

为了更好的可访问性，你总是需要给你的图片添加一个标题。唯一的方法是在 HTML 中使用 figure 标签。但是，我看到很多开发者只单独使用 image 标签。所以他们不给图片加说明。

这是每个人都需要避免的错误。始终使用图形标签。

*不要这样:*

```
<img src="images/img" alt="alt text" />
<p>This is an image.</p>
```

*改为这样做:*

```
**<figure>**
  <img src="images/img" alt="alt text">
  <**figcaption**>This an image of a car.</**figcaption**>
**</figure>**
```

# 3.不使用语义标签

许多初学者犯的另一个错误是他们没有使用语义 HTML 标签。这些类型的标签是好的和可读的，尤其是为了可访问性的目的。

语义标签就是你所知道的标签，比如`<header>`、`<nav>`、`<main>`、`<article>`、`<footer>`、`<section>`等等。像`<div>`、`<span>`等标签并不是语义标签，我们只是有时用它们来构建布局。

所以不要使用 div 或 spans 来创建页眉、节和页脚。

*不要这样:*

```
<div class="header">This is a header</div><div class="section">This is a section</div><div class="footer">This is a footer</div>
```

*改为这样做:*

```
<**header**>This is a header</**header**><**section**>This is a section</**section**><**footer**>This is a footer</**footer**>
```

# 4.替换行内元素中的块元素

在块元素中总是替换行内元素是一个好习惯，而不是相反。块元素是像 div、标题等元素。另一方面，像链接和图像这样的元素是内联的。

所以总是避免在内联元素中替换块元素。

*不要这样:*

```
**<a>**
 <h2>This is a link</h2>
**</a>**
```

*改为这样做:*

```
**<h2>**
 <a>This is a link</a>
**</h2>**
```

# 5.使用粗体和斜体标签

标签`<b>`和`<i>`用于 HTML 中的粗体和斜体。然而，这些标签根本没有语义。

如果你想在不使用这些标签的情况下加粗和倾斜文本，使用 CSS 或者只使用标签`<strong>`和`<em>`来实现。

*所以避免这个:*

```
<i>This text is italic.</i><b>This text is bold.</b>
```

*然后这样做:*

```
<**strong**>This text is italic.</**strong**><**em**>This text is bold.</**em**>
```

# 结论

正如你在上面看到的，这些是你作为开发者需要避免的一些 HTML 错误。我也犯了一些 HTML 错误。这就是为什么我想与你分享它们，这样你也可以避免它们。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读:**

[](/5-useful-javascript-regex-methods-every-developer-must-know-20ebb5993c8) [## 每个开发人员都必须知道的 5 个有用的 JavaScript Regex 方法

### JavaScript 中必须知道的正则表达式方法列表。

javascript.plainenglish.io](/5-useful-javascript-regex-methods-every-developer-must-know-20ebb5993c8) [](/10-awesome-front-end-development-tools-to-boost-your-productivity-b1d2efc4c4ba) [## 10 个令人敬畏的前端开发工具来提高您的生产力

### 你可能需要用到的有用的前端开发工具。

javascript.plainenglish.io](/10-awesome-front-end-development-tools-to-boost-your-productivity-b1d2efc4c4ba) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)