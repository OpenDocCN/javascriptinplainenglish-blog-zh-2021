# 如何调整 HTML5 画布的大小以适应窗口

> 原文：<https://javascript.plainenglish.io/how-to-resize-html5-canvas-to-fit-the-window-26935bf301c4?source=collection_archive---------2----------------------->

![](img/e58255ccc85df8bb16a72c41211aaccd.png)

Photo by [Jem Sahagun](https://unsplash.com/@jemsahagun?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要调整 HTML5 画布的大小以适应它所在的窗口。

在本文中，我们将看看如何调整 HTML5 画布的大小以适应窗口。

# 设置画布的宽度和高度属性

我们可以在窗口调整大小时设置画布的`width`和`height`属性，以设置画布的宽度和高度来改变其大小。

例如，我们可以写:

```
const draw = (canvas) => {
  const ctx = canvas.getContext("2d");
  ctx.beginPath();
  ctx.arc(95, 50, 40, 0, 2 * Math.PI);
  ctx.stroke();
}const canvas = document.querySelector("canvas");
canvas.width = window.innerWidth
canvas.height = window.innerHeight
draw(canvas)window.addEventListener('resize', () => {
  canvas.width = window.innerWidth
  canvas.height = window.innerHeight
  draw(canvas)
})
```

要更改画布的大小，请使用以下命令初始化为窗口的尺寸:

```
canvas.width = window.innerWidth
canvas.height = window.innerHeight
```

我们在 resize 事件侦听器中做同样的事情，它是用`addEventListener`方法添加的。

当画布调整大小时，内容消失了，所以每当我们通过设置`width`和`height`属性来调整画布大小时，它们必须被再次绘制。

# 用 CSS 设置大小

我们也可以用 CSS 设置画布的大小，让它充满屏幕。

例如，我们可以编写以下 HTML:

```
<canvas></canvas>
```

和下面的 CSS:

```
html,
body {
  width: 100%;
  height: 100%;
  margin: 0;
}canvas {
  background-color: #ccc;
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
}
```

将画布的`width`和`height`都设置为 100%。

我们还将`position`设置为`absolute`并将`top`、`left`、`right`和`bottom`设置为 0，以使画布填满屏幕。

此外，我们通过将`width`和`height`设置为 100%来使`html`和主体元素填充屏幕。

我们可以利用它:

```
const canvas = document.querySelector("canvas");
const ctx = canvas.getContext("2d");
ctx.beginPath();
ctx.arc(95, 50, 40, 0, 2 * Math.PI);
ctx.stroke();
```

我们用`arc`方法画一个圆。

我们将中心 x 和 y 坐标、半径以及以弧度表示的开始和结束角度作为参数，按此顺序排列。

# 结论

我们可以用 JavaScript 或 CSS 调整画布的大小以适应屏幕。

*更多内容请看*[***plain English . io***](http://plainenglish.io)