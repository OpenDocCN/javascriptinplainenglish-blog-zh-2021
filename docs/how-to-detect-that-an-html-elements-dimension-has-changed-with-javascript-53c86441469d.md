# 如何用 JavaScript 检测出一个 HTML 元素的维度发生了变化？

> 原文：<https://javascript.plainenglish.io/how-to-detect-that-an-html-elements-dimension-has-changed-with-javascript-53c86441469d?source=collection_archive---------19----------------------->

![](img/ba37396469c7ad45c814fa2c99e5d027.png)

Photo by [Pavel Neznanov](https://unsplash.com/@npi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想检测一个 HTML 元素的大小是否改变了。

在这篇文章中，我们将看看如何检测一个大小发生变化的 HTML 元素。

# `ResizeObserver`

ResizeObserver API 允许我们观察 HTML 元素大小的变化。

例如，我们可以写:

```
const div = document.querySelector('div')
const sleep = ms => new Promise((resolve) => setTimeout(resolve, ms));(async () => {
  for (let i = 0; i < 10; i++) {
    const p = document.createElement('p')
    p.textContent = 'hello'
    div.appendChild(p)
    await sleep(1000)
  }
})();new ResizeObserver(e => {
  const [{
    borderBoxSize,
    contentBoxSize,
    contentRect,
    devicePixelContentBoxSize: [devicePixelBoxSize]
  }] = e;
  console.log(borderBoxSize, contentBoxSize, contentRect, devicePixelBoxSize)
}).observe(div);
```

我们有一个想要观察大小变化的 div。

我们有一个异步函数，它向 div 添加一个 p 元素，以每秒改变它的大小。

然后我们使用带有回调的`ResizeObserver`来观察大小变化。

我们用`div`元素对象调用`observe`来观察 div 的大小变化。

在`ResizeObserver`回调中，我们在参数中获取一个事件对象，该对象包含关于被监视元素的信息。

我们在`e`对象中获得一些属性。

属性让我们获得被观察元素的边框大小。

属性让我们获得被观察元素的内容框大小。

属性让我们获得被观察元素的新大小。

属性拥有新的内容框大小，以被观察元素的设备像素为单位。

这些属性都是对象。

`borderBoxSize`、`contentBoxSize`和`contentRect`属性具有`blockSize`和`inlineSize`属性，其大小以像素为单位，取决于元素是块元素还是行内元素。

`contentRect`是具有`left`、`right`、`top`和`bottom`属性的矩形的坐标。

`left`和`top`有左上角的 x 和 y 坐标，以像素为单位。

`right`和`bottom`以像素为单位表示右下角的 x 和 y 坐标。

`x`和`y`也有左上角的 x 和 y 坐标，以像素为单位。

# 结论

我们可以使用 ResizeObserver API 来观察给定 HTML 元素的大小变化。

*更多内容看*[***plain English . io***](http://plainenglish.io/)