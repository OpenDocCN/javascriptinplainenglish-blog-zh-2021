# 使用新的 CSS“内容可见性”属性提高呈现性能

> 原文：<https://javascript.plainenglish.io/improve-rendering-performance-with-the-new-css-content-visibility-property-7e0c9b425b58?source=collection_archive---------6----------------------->

## WEB 性能

## 了解内容可见性属性

![](img/3999f1ccd0aac384276cf4d183536760.png)

今年早些时候，Chromium 85 发布了，它低调地包含了一个新的 CSS 属性，当时我完全被它迷住了。属性允许你指示用户代理跳过所有的渲染工作，包括布局和绘画，直到需要的时候。

## 这个什么时候有用？

如果您的内容最初是隐藏的或不在屏幕上，那么那些包含文本甚至多媒体的部分就不必呈现。这可以极大地提高页面呈现性能，因为不需要加载任何内容，甚至是节中包含的图像或 iFrames。

马上，我能想到这方面的几个应用:

*   长页面上折叠线以下的所有内容
*   下拉菜单
*   侧板
*   情态动词

## 如何使用它

属性基本上是 CSS 包容规范的简写。该属性有三个唯一的值:

*   `**visible**`:这是默认值，没有任何效果。元素的内容被正常布局和呈现。
*   `**hidden**`:元素完全跳过其内容。用户代理功能(如在页面中查找、tab 键顺序导航)无法访问内容，也无法选择或聚焦内容。这在效果上类似于给出元素的内容`display: none;`。
*   `**auto**`:元素接受布局、风格、油漆包容。如果元素与用户无关，它也会跳过其内容。与`hidden`值不同，被跳过的内容仍可访问用户代理功能，如页面查找、tab 键顺序导航，并且必须是可聚焦和可选择的。

这意味着我们可以使用下面的 CSS 来实现这样的效果，即某个元素的内容不会被呈现、绘制、样式化，或者它的任何媒体资产不会被加载，直到它需要出现在屏幕上。

不过有一个小问题。元素的高度现在是 0，就像你在元素上使用`display: none;`一样。这并不理想，因为当元素变得可见时，你可以看到滚动条移动，这是很糟糕的 UI。

为了解决这个问题，我们可以使用`contain-intrinsic-size`属性来设置元素的占位符宽度和高度，直到需要并呈现实际内容。

## 隐藏具有内容可见性的内容:隐藏

使用`content-visibility: hidden;`将内容隐藏在用户的视野之外，从用户代理特性中删除它，并像`display: none;`一样使内容不可选择和不可聚焦。区别在于缓存的呈现状态。

当使用`display: none;`时，它完全破坏了渲染状态。这意味着从一个元素中移除`display: none;`和呈现一个具有相同内容的全新元素实际上没有区别。

然而，当使用`content-visibility: hidden;`时，缓存的渲染状态被保持。这意味着内容可以更有效地呈现在屏幕上。这对于可以重复显示/隐藏的内容块非常有用，就像单页应用程序中的视图一样。

## 浏览器支持

`content-visibility`是在 Chromium 85 中添加的，目前在 Chrome、Edge 和 Opera 的最新版本上工作。Firefox 认为它值得进行原型开发，而 Safari 目前还没有对此功能发表任何评论。

这意味着在生产网站上使用`content-visibility: hidden;`需要记住一些事情。你不能安全地使用`content-visibility: hidden;`作为隐藏内容的唯一方法。要么使用某种形式的特征检测，要么将其与`display: none;`结合使用。

## 结论

这个简单的 CSS 属性可以为您的工具包带来令人兴奋的性能优化。有关资源`content-visibility`和 CSS 包容规范的更多信息，请查看以下资源:

*   [内容可见性:提升渲染性能的新 CSS 属性](https://web.dev/content-visibility/) [web.dev]
*   [内容可见性文档](https://developer.mozilla.org/en-US/docs/Web/CSS/content-visibility)【MDN 网络文档】
*   [CSS 包容上的 MDN 文档](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Containment)

感谢您的阅读。如果你对此有任何想法，请在下面的评论中告诉我。

你可以在 Twitter 上关注我。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)