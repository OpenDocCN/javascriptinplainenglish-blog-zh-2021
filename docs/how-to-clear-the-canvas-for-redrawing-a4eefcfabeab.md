# 如何清空画布进行重绘？

> 原文：<https://javascript.plainenglish.io/how-to-clear-the-canvas-for-redrawing-a4eefcfabeab?source=collection_archive---------3----------------------->

![](img/0f3922a4b26ff4abb180aa0d40c9252d.png)

Photo by [Elena Mozhvilo](https://unsplash.com/@miracleday?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我们有一个画布，我们可能要清除它，以便我们可以在上面画新的东西。

在这篇文章中，我们将看看如何清除画布，以便我们可以再次在其上绘制。

# 清除画布以便重新绘制

我们可以用`clearRect`方法轻松地清除画布，它是画布上下文对象的一部分。

例如，如果我们有下面的 HTML:

```
<canvas></canvas>
<button>
  clear
</button>
```

然后我们可以写:

```
const canvas = document.querySelector("canvas");
const button = document.querySelector("button");
const ctx = canvas.getContext("2d");
ctx.beginPath();
ctx.lineWidth = "6";
ctx.strokeStyle = "green";
ctx.rect(5, 5, 290, 140);
ctx.stroke();button.addEventListener('click', () => {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
})
```

绘制一些东西，并向按钮添加一个单击侦听器，以便在我们单击按钮时清除画布。

我们调用`getContext`来获取上下文对象。

然后我们叫`beginPath`开始画画。

我们设置`lineWidth`来设置线条的宽度。

`strokeStyle`设置笔画样式。

`rect`分别以左上角的 x、y 坐标和宽度、高度绘制矩形。

而`stroke`方法绘制矩形。

接下来，我们用`'click'`调用`addEventListener`来为按钮添加一个点击监听器。

当我们点击按钮时，回调就会运行。

我们使用与`rect`相同的参数调用带有画布上下文的`clearRect`。

它清除画布，而不是在画布上绘制。

# 转换坐标

如果我们在画布上添加了坐标转换，那么我们必须先添加更多的代码来保存转换矩阵。

然后我们可以清空画布，然后恢复变换矩阵。

为此，我们写道:

```
const canvas = document.querySelector("canvas");
const button = document.querySelector("button");
const ctx = canvas.getContext("2d");
ctx.beginPath();
ctx.lineWidth = "6";
ctx.strokeStyle = "green";
ctx.rect(5, 5, 290, 140);
ctx.stroke();button.addEventListener('click', () => {
  ctx.save();
  ctx.setTransform(1, 0, 0, 1, 0, 0);
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.restore();
})
```

在回调中，我们调用`save`来保存转换矩阵。

`setTransform`将变换设置为单位矩阵，以移除变换。

然后我们调用`clearRect`来清除画布。

我们调用`restore`来恢复转换。

# 结论

我们可以通过调用`clearRect`方法来清除画布。

如果我们已经转换了坐标，那么我们可以保存转换矩阵，清除画布，然后恢复转换矩阵。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)