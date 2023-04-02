# 没有 CSS 或 JavaScript 的响应图像，使用<picture>元素</picture>

> 原文：<https://javascript.plainenglish.io/responsive-images-without-css-or-js-using-the-picture-element-9e994ef8d619?source=collection_archive---------9----------------------->

## 通过使用更高级的 HTML 标记来提升 web 开发人员的级别

![](img/18fe09e6ed8f9201eed9c5550b0dbdbc.png)

Credit: unsplash.com

我花了一些时间重温我的基本网络技术知识，尤其是 HTML 和可访问性。很多时候，初级开发人员和高级开发人员的区别不是他们对高级模式的了解，而是他们对这些本地支持的 API 的了解。

一旦你知道你能用 HTML 做多少事情，你就能写出更轻便、功能更全、向后兼容性更强的网站。

浏览器支持的特性之一是`<picture>`元素，所有现代浏览器都支持[。元素允许你只用 HTML 在你的网页上创建可响应的、可访问的图像。](https://caniuse.com/picture)

当一个图像只加载了一个常规的`src`属性时，浏览器不知道它有多宽，直到在之后*才被加载。你对图像所做的任何修改，如修改大小等等。已经太少太晚了。使用`picture`元素，我们可以提前*告诉浏览器我们的每个图像有多宽*。然后，它可以使用该信息根据当时视窗的大小加载最合适的图像，然后在调整窗口大小时加载正确的图像。*

> 快速旁白:
> 
> 在简单的情况下，如果你想提供一些可选的图片来提高你的网站性能，你仍然可以使用带有`srcset` 属性的`img`标签。请参见下面的示例:

img element with screen width image fallbacks based on size

但是我们想要做的不仅仅是基于宽度的图像选择，而`<picture>` 标签就是这项工作的工具。`<picture>`标签包含多个`<source>`图像集，这些图像集可以根据媒体进行加载(这可能意味着不同宽度的屏幕，就像上面的例子一样，但不需要仅限于此)。常见的情况是当您需要根据支持的 mime 类型(jpeg、png、gif 等)更改图像时。)或者当您需要根据屏幕方向更改图像时。

`<source>`旨在表示一幅图像或一组图像的元素，这些图像可以作为要由浏览器按照它们被列出的顺序加载的图像。**顺序很重要，因为浏览器将选择符合条件的第一个源。**

复制上述 img 标记功能的简单示例如下所示:

即使只是像上面这样简单的修改也能极大地提高网站的性能，因为图像是大多数网站需要的最重要的资源。

图片元素比这更灵活。每个`source`有 3 个独立的属性可用于条件匹配:`srcset`用于匹配宽度或像素密度，`type`用于匹配图像类型，`media`用于匹配其他媒体条件。正如您所猜测的，这创造了巨大的灵活性。

在下面的例子中，我试图展示`<picture>`元素的一些常见用例:

使用图片元素的方式有无数种，但是将它整合到任何生产网站中都会对网站性能有很大的帮助。我强烈推荐。

亚历克斯·济托-沃尔夫

来源:

[](https://webdesign.tutsplus.com/tutorials/quick-tip-how-to-use-html5-picture-for-responsive-images--cms-21015) [## 如何使用 HTML5“图片”、“srcset”和“大小”来响应图像

### 是一个 HTML5 元素，旨在为我们提供更多的通用和高性能的响应图像功能。而不是…

webdesign.tutsplus.com](https://webdesign.tutsplus.com/tutorials/quick-tip-how-to-use-html5-picture-for-responsive-images--cms-21015) [](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture) [## :图片元素- HTML:超文本标记语言| MDN

### HTML 元素包含零个或多个元素和一个元素，为不同的应用程序提供不同版本的图像

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)