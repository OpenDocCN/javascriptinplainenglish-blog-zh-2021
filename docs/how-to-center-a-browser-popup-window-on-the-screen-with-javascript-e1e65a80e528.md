# 如何用 JavaScript 在屏幕上居中一个浏览器弹出窗口？

> 原文：<https://javascript.plainenglish.io/how-to-center-a-browser-popup-window-on-the-screen-with-javascript-e1e65a80e528?source=collection_archive---------16----------------------->

![](img/96f1da1bb5ef4227d3e65808471c0bc0.png)

Photo by [Michał Lis](https://unsplash.com/@mq1?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想在 JavaScript web 应用程序中打开一个弹出窗口。

我们可能希望弹出窗口在屏幕上居中。

在本文中，我们将看看如何用 JavaScript 在屏幕上居中显示一个浏览器弹出窗口。

# 用 JavaScript 在屏幕上居中显示一个浏览器弹出窗口

为了在屏幕上居中显示一个浏览器弹出窗口，我们必须进行一些计算，并将结果传递到选项字符串中，我们将该字符串传递到`window.open`。

为此，我们写道:

```
const popupCenter = ({
  url,
  title,
  w,
  h
}) => {
  const dualScreenLeft = window.screenLeft !== undefined ? window.screenLeft : window.screenX;
  const dualScreenTop = window.screenTop !== undefined ? window.screenTop : window.screenY; const width = window.innerWidth ? window.innerWidth : document.documentElement.clientWidth ? document.documentElement.clientWidth : screen.width;
  const height = window.innerHeight ? window.innerHeight : document.documentElement.clientHeight ? document.documentElement.clientHeight : screen.height; const systemZoom = width / window.screen.availWidth;
  const left = (width - w) / 2 / systemZoom + dualScreenLeft
  const top = (height - h) / 2 / systemZoom + dualScreenTop
  const newWindow = window.open(url, title,
    `
      scrollbars=yes,
      width=${w / systemZoom}, 
      height=${h / systemZoom}, 
      top=${top}, 
      left=${left}
      `
  ) if (window.focus) {
    newWindow.focus();
  }
}popupCenter({
  url: 'http://www.yahoo.com',
  title: 'yahoo',
  w: 900,
  h: 500
});
```

我们创建了`dualScreenLeft`和`dualScreenTop`变量，在用户有两个屏幕而不是一个屏幕的情况下，将弹出窗口的中心移动到左上角。

通过得到`screenLeft`或`screenX`来计算`dualScreenLeft`。

`dualScreenTop`是通过得到`screenTop`或`screenY`来计算的。

然后我们用`clientWidth`、`innerWidth`或`screen.width`计算弹出框的`width`。

弹出窗口的`height`设置为`clientHeight`、`innerHeight`或`scree.height`。

然后我们用`systemZoom`变量得到屏幕的缩放级别。

接下来，我们用`left`和`top`变量计算左上角的坐标。

我们通过设置为缩放级别调整的`width`来计算`left`值。

然后我们用`dualScreenLeft`移动屏幕，以防我们在第二个屏幕上显示窗口。

而我们做一个类似的计算来计算`top`。

接下来，我们用`systemZoom`以及`top`和`left`值调用`window.open`。

如果`focus`方法存在，我们在`newWindow`上调用`focus`。

现在，当我们调用`popupCenter`方法时，无论我们有一个还是两个屏幕，我们都会看到弹出窗口居中。

# 结论

我们可以通过一些计算来获得屏幕上弹出窗口左上角的坐标及其宽度和高度，从而使浏览器弹出窗口居中。

*更多内容看*[***plain English . io***](http://plainenglish.io/)