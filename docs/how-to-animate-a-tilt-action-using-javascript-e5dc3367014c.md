# 如何使用 JavaScript 制作倾斜动作的动画

> 原文：<https://javascript.plainenglish.io/how-to-animate-a-tilt-action-using-javascript-e5dc3367014c?source=collection_archive---------9----------------------->

![](img/19b21983637db4e722cf2ba2c00b2ef0.png)

Photo by [Lena Balk](https://unsplash.com/@lenabalk?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/tilt?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 背景

我最近在我的网站上实现了磨砂玻璃效果和倾斜动画。如果你对实现 glassmporphism 感兴趣，可以看看我的上一篇文章:[霜玻璃效果造型](https://arturocreates.medium.com/implement-frosted-glass-aesthetic-glassmorphism-f93fbb35f416)。如果你想看最终的现场实现，请查看我的网站(【arturocreates.com】T2)。在本文中，我将带您了解如何实现倾斜动画，以及如何处理移动视图。

# JavaScript 实现

下面是完成这项工作的步骤。

1.  下载并保存 [vanilla-tilt.js](https://micku7zu.github.io/vanilla-tilt.js/) 到你的项目中
2.  在 HTML 中引用普通标题文件 javascript

```
<script type=”text/javascript” src=”./src/js/vanilla-tilt.js”></script>
```

3.给你的 HTML 容器一个类名(在我的例子中，我使用的是

)

4.实现以下 JavaScript 代码

```
VanillaTilt.init(document.querySelectorAll(“.card”), {max: 25,speed: 400,glare: true,“max-glare”: 1,});
```

此时，您应该能够将鼠标悬停在卡组件上，它会以倾斜动画做出响应。查看 vanialla-tilt.js 文档了解更多选项。

# 还有一点

在此之后，我面临的问题，也是我写这篇文章的动机，是我不喜欢它在移动浏览器上的样子。当我在一部 iPhone 上测试时，它是静态的，除非当我点击卡片时它显示“悬停”。它只是向一个方向移动了卡片，但没有把它倾斜回原来的位置。在 Android 上，当我给手机命名时，它会倾斜卡片。作为一个概念，这将是很酷的，但在现实中，它是错误的，看起来不太干净，我的口味。我对这两种实现都不感兴趣。为了解决这个问题，我简单地禁用了移动屏幕上的标题动画，我对结果非常满意。

您可以使用以下代码检查触摸屏设备:

```
var touchDevice = ('ontouchstart' in document.documentElement);
```

总之，这是我最后的 JavaScript 代码。

```
<!-- Import the downloaded vanilla-tilt file-->
<script type=”text/javascript” src=”./js/vanilla-tilt.js”></script><!-- Define the Javascript code block -->
<script type=”text/javascript”>// define variablevar touchDevice;// check if it’s a touch device (mobile, tablets)touchDevice = (‘ontouchstart’ in document.documentElement);// only activate tilt on card, if its not mobileif(!touchDevice){VanillaTilt.init(document.querySelectorAll(“.card”), {max: 25,speed: 400,glare: true,“max-glare”: 1,});console.log(‘tilt is active’)} else {console.log(‘tilt is inactive’)}</script>
```

这是最终结果的截图。

![](img/faa19c20d694fdf75cf465bf53cea44c.png)

[arturocreates.com](https://arturocreates.com/)

结论

这应该是让你的 tilt 动画在你的网站上运行所需要的全部代码。如果这篇文章对你有所帮助，请为它“鼓掌”。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)