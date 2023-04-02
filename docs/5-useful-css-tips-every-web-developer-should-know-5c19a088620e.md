# 每个 Web 开发人员都应该知道的 5 个有用的 CSS 技巧

> 原文：<https://javascript.plainenglish.io/5-useful-css-tips-every-web-developer-should-know-5c19a088620e?source=collection_archive---------3----------------------->

## 作为一名 web 开发人员，你应该知道的一些 CSS 技巧。

![](img/41f17e242e3dab3bd4f589d88fd6a9f6.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

CSS 是一种很棒的样式表语言，它允许你通过描述 HTML 元素应该如何显示来创建好看的网页。CSS 节省了很多工作。它可以一次控制多个网页的布局。我一直在很多项目中使用它，我学到了一些技巧，我想与你分享。

在这篇文章中，我们会给你一些你作为一个网页开发者应该知道的 CSS 技巧。让我们开始吧。

# 1.使 div 居中的简单方法

用 CSS 居中 div 的最简单的方法之一是使用 Flexbox。这使得定位和对齐元素更加容易。

这里有一个例子:

```
.parent {
  **display: flex;
  align-items: center;
  justify-content: center;**
  height: 100vh;
  width: 100wh;
}

.child {
  width: 100px;
  height: 100px;
  background-color: #20126f;
}
```

请点击这里查看:

Centering a div with Flexbox.

如果你想看的话，我写了一整篇关于 Flexbox 的文章。

[](https://medium.com/javascript-in-plain-english/css-flexbox-explained-with-examples-85efa38e4770) [## CSS Flexbox 举例说明

### 通过实例了解 CSS flexbox。

medium.com](https://medium.com/javascript-in-plain-english/css-flexbox-explained-with-examples-85efa38e4770) 

# 2.混合模式

CSS 可以做很多惊人的事情，其中之一就是混合模式。混合模式有两个属性:`mix-blend-mode`，它定义元素及其后面的元素之间的混合，以及`background-blend-mode`，它定义元素的背景图像和背景颜色之间的混合。

下面是一个 div 中包含图像和文本的示例:

*HTML:*

```
<div class="blend">
  <img src="imageSrc" />
   <h1>NATURE</h1>
</div>
```

*CSS:*

```
.blend {
  width: 100vw;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
}.blend img {
  position: absolute;
}.blend h1 { 
  font-size: 150px;
  **mix-blend-mode: overlay;**
}
```

检查这个 Codepen 示例:

Blend mode.

# 3.响应网格

您可以使用 CSS 网格功能轻松制作自动响应的布局。这里有一个例子:

```
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-gap: 10px;
}
```

例如，假设您必须为一个电子商务应用程序显示产品列表。您的任务是使其响应迅速，因此您决定在桌面上每行显示三个产品，在平板电脑上每行显示两个产品，在移动设备上每行只显示一个产品。看看下面的例子:

*HTML 代码:*

```
<div class="grid"><div class="item">Product 1</div><div class="item">Product 2</div><div class="item">Product 3</div><div class="item">Product 4</div><div class="item">Product 5</div><div class="item">Product 6</div></div>
```

*CSS:*

```
*{
 margin: 0;
 padding: 0;
 box-sizing: border-box;
 font-family: sans-serif;
}
body{
 height: 100vh;
 margin-top: 150px;
}
**.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-gap: 10px;
}**
.item{
 background: red;
 padding: 20px;
 color: wheat;
}
```

你可以检查下面的 Codepen，只需在一个新的标签中打开它，并调整你的屏幕大小，以查看不同之处。

Responsive grid.

# 4.对图像使用滤镜功能

功能`**filter()**`将图形变化应用于输入图像和元素的外观。我们能达到的效果有:(`blur`、`brightness`、`contrast`、`grayscale`、`hue-rotate`、`opacity`、`invert`、`sepia`、`saturate`、`drop-shadow`……)。

这里有一个例子:

```
.element1 {   
  **filter**: drop-shadow(0.25rem 0 0.75rem #ef9035);
 }
// Or:.element2 {
  **filter**: blur(20px);
}
```

看看下面的代码笔:

The filter function.

# 5.背面可见度

CSS 属性`backface-visibility`设置一个元素的背面在面向用户时是否可见。

```
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  **backface-visibility: hidden;**
}
```

下面是一个代码笔示例:

Backface visibility.

# 结论

正如您所看到的，CSS 是一个强大的工具。不用框架，你可以用它实现更多的事情。你只需要一些创造力和激情，因为可能性是无穷无尽的。

# 更多阅读

*如果您对 JavaScript 和网络开发相关的更有用的内容感兴趣，您也可以* [*订阅我们的时事通讯*](https://mehdiouss.ck.page/) *。*

*以下链接中还有一篇有用的文章可以查看:*

[](https://medium.com/javascript-in-plain-english/html-drag-and-drop-api-explained-with-examples-35cda91bce56) [## 用例子解释的 HTML 拖放应用编程接口

### 通过实例学习如何拖放。

medium.com](https://medium.com/javascript-in-plain-english/html-drag-and-drop-api-explained-with-examples-35cda91bce56)