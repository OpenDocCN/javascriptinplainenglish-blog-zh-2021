# 如何观看 JavaScript 窗口调整大小事件？

> 原文：<https://javascript.plainenglish.io/how-to-watch-the-javascript-window-resize-event-7637acecd036?source=collection_archive---------1----------------------->

![](img/00f4d3787be4ffe33f4d12c79aef7555.png)

Photo by [Jem Sahagun](https://unsplash.com/@jemsahagun?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们可以用 JavaScript 观察窗口大小调整事件，以检测任何类型的屏幕大小变化。

在本文中，我们将研究如何观察 JavaScript 窗口大小调整事件来检测窗口大小调整。

# 将事件处理程序分配给 window.onresize 属性

为窗口调整大小事件添加事件处理程序的一种方法是将事件处理程序函数分配给`window.onresize`属性。

例如，我们可以写:

```
window.onresize = (event) => {
  console.log(event)
};
```

将功能分配给`window.onresize`。

`event`参数有一个事件对象，它是窗口`resize`事件发出的数据。

# 调用 window.addEventListener 以附加 Resize 事件处理程序

我们还可以调用`window.addEventListener`方法来为`window`附加一个事件监听器。

为了监听 resize 事件，我们传入`'resize'`作为第一个参数。

第二个参数是 resize 事件的事件处理程序。

例如，我们可以写:

```
window.addEventListener('resize', (event) => {
  console.log(event)
});
```

`event`参数与我们在前面的例子中分配给`onresize`方法的参数相同。

# resize 观察者

观察元素大小调整的更现代的方法是使用`ResizeObserver`构造函数。

它让我们用 tyhe `observe`方法创建一个对象，该对象接受我们想要观察其大小调整的元素。

例如，我们可以写:

```
const ro = new ResizeObserver(entries => {
  for (const entry of entries) {
    const cr = entry.contentRect;
    const {
      width,
      height,
      top,
      left
    } = cr
    console.log(entry.target);
    console.log(width, height, top, left)
  }
});
ro.observe(document.querySelector('html'));
```

我们用一个函数调用`ResizeObserver`构造函数，这个函数循环遍历`entries` whyich，它拥有我们正在观察的项目。

在循环体中，我们从`entry.contentRect`属性中获取维度。

`width`和`height`有元素的宽度和高度。

`top`和`left`分别是左上角的 x 和 y 坐标。

`entry.target`拥有我们正在观察的元素。

然后我们用我们正在观察的元素调用`ro.observe`。

如果我们想观察浏览器窗口的大小调整，那么我们可以观察`html`元素。

我们可以用`document.querySelector`来选择它。

# 结论

我们可以通过给`window`对象分配一个 resize 事件监听器来监听 resize 事件。

或者我们可以使用`ResizeObserver`构造函数来创建一个对象，让我们观察元素的大小调整。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*