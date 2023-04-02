# 没有人谈论的 5 个 HTML 技巧

> 原文：<https://javascript.plainenglish.io/5-html-tricks-nobody-is-talking-about-a0480104fe19?source=collection_archive---------0----------------------->

## 2021 年你应该知道的 HTML 标签和属性

![](img/9be766cf4b3adb1212e1b19cf5634cee.png)

Photo by [Jamie Haughton](https://unsplash.com/@haughters?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

不管你选择哪种框架或后端语言，所有的 web 开发人员都必须广泛使用 HTML(超文本标记语言)。

框架和编程语言可能来来去去，但 HTML 会一直存在。但是尽管使用如此广泛，仍然有大多数开发人员没有意识到的标签和属性。

虽然有各种各样的模板引擎，比如 Pug，但是你仍然需要很好的掌握 HTML 和 CSS。

如果您经常使用 CSS，请查看我最近的博客，了解一些不太为人所知的最有用的 CSS 属性。

[](https://medium.com/javascript-in-plain-english/6-css-properties-nobody-is-talking-about-e6cab5138d02) [## 6 没有人谈论的 CSS 属性

### 许多人从未听说过的有趣特性。

medium.com](https://medium.com/javascript-in-plain-english/6-css-properties-nobody-is-talking-about-e6cab5138d02) 

在我看来，尽可能使用 HTML 特性比使用 JavaScript 实现相同的功能更好，尽管我承认编写 HTML 可能会变得重复和枯燥。

尽管许多开发人员每天都在使用 HTML，但他们并没有尝试提升自己的水平，真正利用一些很少被提及的 HTML 特性。

下面是你应该知道的 5 个 HTML 标签和属性:

## 1.延迟加载图像

延迟加载图片有助于提高网站的性能和响应速度。

延迟加载可以防止屏幕上不需要的图像被立即加载。但是，当您向下滚动或靠近图像时，图像开始加载。

换句话说，当用户滚动并且图像变得可见时，图像被加载，否则，图像不被加载。

这可以通过普通的 HTML 轻松实现。

您所要做的就是将`loading= “lazy”`属性添加到您的图像文件中。

添加属性后，您的图像元素应如下所示:

```
<img src="image.png" loading="lazy" alt="…" width="200" height="200">
```

通过使用[谷歌的 Lighthouse](https://developers.google.com/web/tools/lighthouse/) 工具，你可以获得一些关于这个技巧将节省的字节的见解。

## 2.输入建议

当你试图寻找某样东西时，得到有用的和相关的建议真的很有帮助。

输入建议和自动完成功能如今相当普遍，你一定在像[谷歌](http://www.google.com)和[脸书](http://www.facebook.com)这样的网站上注意到了。

您可以使用 [JavaScript 添加输入建议](https://www.w3schools.com/howto/howto_js_autocomplete.asp)，方法是在输入字段上设置一个事件监听器，然后将搜索的术语与预定义的建议进行匹配。

然而，HTML 允许您使用`<datalist>`标签显示一组预定义的建议。

请记住，该标签的 ID 属性必须与输入字段列表属性相同。

```
<label for="country">Choose your country from the list:</label>
<input list="countries" name="country" id="country">

<datalist id="countries">
  <option value="UK">
  <option value="Germany">
  <option value="USA">
  <option value="Japan">
  <option value="India">
</datalist>
```

## 3.图片标签

你有没有遇到过图像没有像你期望的那样放大的问题？我当然有很多次。

这通常发生在您试图建立画廊网站或使用大图像并将其显示为缩略图时。

当您更改视口宽度时，您可能会注意到某些图像没有按预期放大和缩小。

幸运的是，HTML 让开发人员有机会通过使用`<picture>`标签很容易地解决这个问题，允许您添加适合不同宽度的多个图像，而不是放大和缩小单个图像。

您的代码将如下所示:

```
<picture>
  <source media="(min-width:768px)" srcset="med_flag.jpg">
  <source media="(min-width:495px)" srcset="small_flower.jpg">
  <img src="high_flag.jpg" alt="Flags" style="width:auto;">
</picture>
```

如您所见，我们指定了特定图像必须显示的最小宽度。

这个标签非常类似于`<audio>`和`<video>`标签。

## 4.基本 URL

这是我在创建网站索引或网站地图时最喜欢的标签之一。

当你有很多锚标签重定向到某个 URL，并且所有的 URL 都以相同的基地址开始时，这个标签就派上用场了。

例如，如果我想指定 Elon Musk 和 Bill Gates 的 Twitter 句柄的 URL，URL 的开头(域)将是相同的，但后面将是他们各自的 id。

通常情况下，我必须用同一个域名粘贴链接两次。

但是，HTML 有一个`<base>`标记，它使您能够设置一个基本 URL，如下所示:

```
<head>
  <base href="https://www.twitter.com/" target="_blank">
</head>

<body>
<img src="elonmusk" alt="Elon Musk">
<a href="BillGates">Bill Gate</a>
</body>
```

上面的代码将生成一个重定向到“https://www . Twitter . com/elon musk”的图像和一个重定向到"https://www.twitter.com/billgates"的锚标记。

`<base>`标签必须有“href”或目标属性。

## 5.文档刷新者

如果您想在一段时间不活动之后或者甚至立即将用户重定向到另一个页面，那么您只需使用普通的 HTML 就可以轻松实现。

你可能已经注意到这个功能，当你打开某些网站时，会弹出“你将在 5 秒钟内被重定向”这样的提示。

这个行为被嵌入到 HTML 中，你可以通过`<meta>`标签并在上面设置`http-equiv= “refresh”`来使用它。

```
<meta http-equiv="refresh" content="4; URL='https://google.com' />
```

这里的`content`属性指定了重定向发生的秒数。

值得注意的是，尽管 Google 声称像对待其他重定向一样对待这种形式的重定向，[使用这种类型的重定向并不明智，除非你真的不得不这样做。](https://help.ahrefs.com/en/articles/2433739-what-is-meta-refresh-redirect-and-why-is-it-considered-a-critical-issue)

因此，只在某些情况下使用它，如在大量不活动后重定向页面。

## 最后的想法

HTML 和 CSS 的功能非常强大，你可以只用这两个就能建立很棒的网站。

然而，尽管这两种语言被大量使用，许多开发人员并没有真正深入研究它们并从中获得乐趣。

除了我上面分享的几个，还有很多这样的技巧和窍门，它们肯定值得在你的项目中尝试。

如果你也打算使用 JavaScript，那么一定要看看我最近的博客，讨论一些可能会节省你时间的技巧。

[](https://medium.com/javascript-in-plain-english/5-modern-javascript-tips-and-tricks-to-save-time-7773aff6be26) [## 节省时间的 5 个现代 JavaScript 技巧和窍门

### 使用这些 JavaScript 技巧减少工作量并编写干净的代码

medium.com](https://medium.com/javascript-in-plain-english/5-modern-javascript-tips-and-tricks-to-save-time-7773aff6be26) 

学习任何东西并精通它都需要时间、奉献和练习，HTML 也不例外。

希望你喜欢看我的文章！