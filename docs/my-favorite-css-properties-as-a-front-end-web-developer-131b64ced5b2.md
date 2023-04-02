# 作为前端 Web 开发人员，我最喜欢的 CSS 属性

> 原文：<https://javascript.plainenglish.io/my-favorite-css-properties-as-a-front-end-web-developer-131b64ced5b2?source=collection_archive---------5----------------------->

## 你可能不知道的 7 个有用的 CSS 属性。

![](img/ee0ed159b45422690ad87dcda33eb25f.png)

Photo by [Christina @ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

CSS 是 web 开发的女王。一种强大的样式表语言，让我们能够制作出好看且响应迅速的网页。许多开发人员都同意 CSS 易学但难掌握的事实。

这是真的，因为它有很多有用的特性和属性供您使用。除此之外，我们还有 CSS grid 和 flexbox 特性，这些特性允许我们轻松地创建复杂且响应迅速的布局，而无需使用表格或浮动的旧方法。

在这篇文章中，我决定与你分享我最喜欢的 CSS 属性，这些属性是我作为前端开发人员使用的。所以让我们开始吧。

# 1.滚动行为属性

CSS 中的属性`scroll-behavior`允许我们定义网页的滚动行为。例如，我可以给属性一个值`smooth`。因此，我将在我的网页上有平滑的滚动效果。

这里有一个例子:

```
html{
 **scroll-behavior: smooth;**
}
```

您也可以查看下面的 Codepen 示例:

Example from [Codepen](https://codepen.io/)(external link outside Medium).

# 2.过滤器属性

我也喜欢 CSS 中的属性`filter`,因为它允许我们对图像进行图形化修改。

它可以把很多函数作为它的值。这些功能允许我们实现不同的图形效果，如亮度、阴影、对比度、模糊等。

这里有一个例子:

```
.filter1 img {
  **filter: grayscale(80%) sepia(11%) saturate(650%);** 
}

.filter2 img {
  **filter: hue-rotate(-35deg);** 
}

.filter3 img {
  **filter: contrast(160%) saturate(75%) blur(1px);**
}
```

这里还有一个 Codepen 示例可供查看:

Example from [Codepen](https://codepen.io/)(external link outside Medium).

# 3.写入模式属性

CSS 给了你改变文本方向或书写模式的能力。为此，您可以使用属性`writing-mode`，它接受诸如`vertical-lr`、`horizontal-tb`和`vertical-rl`之类的值。

这里有一个例子:

```
h1{
  **writing-mode: vertical-lr;**
  margin: 10px;
}
h2{
  **writing-mode: horizontal-tb;** }
```

请在下面的代码栏中查看:

Example from [Codepen](https://codepen.io/)(external link outside Medium).

# 4.Flexbox 和网格属性

Flexbox 和 grid 是在 CSS 中轻松创建复杂且响应性强的布局的两种方式。我想每个 web 开发者都应该知道它们，因为它们非常有用。它们有很多你可以利用的强大属性。

有了 Flexbox 和 grid，您再也不需要担心使用 floats 或 tables 了。这就是为什么在创建响应式布局时，Flexbox 和 Grid 属性是我的最爱。

如果你有兴趣，可以看看下面两篇我在 Medium 上写的关于 Flexbox 和 Grid 的文章:

[](/css-flexbox-explained-with-examples-85efa38e4770) [## CSS Flexbox 举例说明

### 通过实例了解 CSS flexbox。

javascript.plainenglish.io](/css-flexbox-explained-with-examples-85efa38e4770) [](/css-grid-explained-with-examples-d64cf241e1cf) [## 用例子解释 CSS 网格

### 通过实例了解 CSS 网格。

javascript.plainenglish.io](/css-grid-explained-with-examples-d64cf241e1cf) 

# 5.背面可见度

CSS 中我喜欢的另一个属性是`backface-visibility`。它允许隐藏或显示一个面向用户的元素的背面。

```
.element{
 **backface-visibility: hidden;**
}
```

例如，我们可以在创建翻转卡时使用这个属性。

您可以查看下面的代码笔示例:

Example from [Codepen](https://codepen.io/)(external link outside Medium).

# 6.属性对象适合

在 CSS 中，当您为图像指定新的高度和宽度时，它可能会失去质量，并且无法容纳它的容器。

这就是房产`object-fit`发挥作用的原因。它允许我们定义如何调整图像或视频的大小以适合其容器。

该属性取值如下:`fill`、`contain`、`cover`、`scale-down`、`none`。

例如，如果我想让图像填充给定的尺寸并具有其原始质量，我可以指定值`cover`。

```
#img1{
  width: 250px;
  height: 180px;
  **object-fit: cover;**
}
```

查看下面的代码笔示例:

Example from [Codepen](https://codepen.io/)(external link outside Medium).

# 7.框阴影属性

在 CSS 中，`box-shadow`是一个流行的属性，它允许你给元素添加阴影效果。我真的很喜欢这个属性，因为它可以让你指定阴影效果的大小和颜色。

```
button:hover{
    background: crimson;
    **box-shadow: 0 0 28px 10px crimson;**
}
```

下面是一个代码笔示例，显示了当我们将鼠标悬停在按钮上时应用于该按钮的阴影效果:

Example from [Codepen](https://codepen.io/)(external link outside Medium).

# 结论

正如您在上面看到的，这些是我作为前端开发人员在构建项目时最喜欢的 CSS 属性。至少在我看来，它们非常有用。让我知道一些您喜欢并发现有用的其他属性。

**更多阅读**

[](/6-important-tips-to-write-clean-react-code-5ef29d6a73a6) [## 写干净反应代码的 6 个重要技巧

### 作为一个有反应的开发人员，编写干净代码的技巧。

javascript.plainenglish.io](/6-important-tips-to-write-clean-react-code-5ef29d6a73a6) 

*多内容于* [***中***](http://plainenglish.io)