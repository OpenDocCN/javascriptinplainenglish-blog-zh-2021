# 用画布把你的鼠标变成画笔

> 原文：<https://javascript.plainenglish.io/turn-your-mouse-into-a-paintbrush-710d06646e76?source=collection_archive---------8----------------------->

[在上一篇文章](https://medium.com/p/e7594e77a8e8)中，我们学习了如何使用画布绘制一些基本的形状，在这篇文章中，我们开始做一些有趣的演示。

这张 gif 展示了我们在文章中的最终项目:

![](img/d74829c5a0d9ac1697445a2e43c4d57c.png)

效果是:当我们的鼠标在页面上移动时，页面会自动生成一个轨迹。这是绘图软件中很常见的功能，那么我们是如何实现的呢？

首先要明白一个基本原理，就是这种曲线可以看成是大量的点。如果我们在鼠标每次经过的位置画一个点，连续画很多个点之后，这些点看起来就像一条曲线。

那么如何画出这些点呢？其实一个点就是一个圆，我们在上一篇文章中已经介绍过了。

这里我们可以写一个专门用来画点的函数:

在画点的时候，我们需要从外部传入`context`对象和圆心的坐标，我们在函数中自己设置圆的颜色和半径。

之后我们要监听 canvas 元素的`onmouseover`事件，每次触发事件都要在鼠标当前位置画一个点。

```
document.getElementById("canvas").onmousemove = function (event) {
  drawPoint(context, event.clientX, event.clientY)
}
```

但是上面的代码有一个缺陷:我们想只在用户按住鼠标的时候画，鼠标按下的时候不再画。所以我们可以优化上面的代码。

所以我们可以把代码改成这样:

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)