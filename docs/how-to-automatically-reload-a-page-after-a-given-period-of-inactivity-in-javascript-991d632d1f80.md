# JavaScript 中如何在给定的不活动时间后自动重新加载页面？

> 原文：<https://javascript.plainenglish.io/how-to-automatically-reload-a-page-after-a-given-period-of-inactivity-in-javascript-991d632d1f80?source=collection_archive---------2----------------------->

![](img/7b89e3131031e34d734194c6936ef0cd.png)

Photo by [Dunamis Church](https://unsplash.com/@dunamis_church?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在网页上不活动一段时间后自动重新加载页面。

在本文中，我们将研究如何用 JavaScript 在一段给定的不活动时间后自动重新加载页面。

# 记录有活动的时间

我们可以监听`mousemove`和`keypress`事件，让我们分别监听鼠标和键盘活动。

然后，我们可以在事件侦听器中记录用户最后一次使用页面的时间。

然后我们可以用这个时间来计算用户最后一次使用这个页面是多久以前。

为此，我们写道:

```
let time = new Date().getTime();
const setActivityTime = (e) => {
  time = new Date().getTime();
}
document.body.addEventListener("mousemove", setActivityTime);
document.body.addEventListener("keypress", setActivityTime);const refresh = () => {
  if (new Date().getTime() - time >= 60000) {
    window.location.reload(true);
  } else {
    setTimeout(refresh, 10000);
  }
}setTimeout(refresh, 10000);
```

我们有`time`变量，它以毫秒为单位的时间戳作为初始值。

然后我们有了`setActivityTime`事件监听器，我们用它来设置用户最后一次使用页面的`time`。

我们监听`mousemove`和`keypress`事件，并使用`setActivityTime`作为事件监听器来记录用户最后一次与页面交互的时间。

然后我们有了`refresh`函数，它检查用户最后一次与页面交互的时间。

如果时间超过 60 秒，那么我们调用`location.reload`重新加载页面。

否则，我们在 10 秒后再次调用`refresh`再次检查。

现在，如果超过 60 秒没有交互，页面应该会刷新。

# 结论

我们可以记录用户与页面交互的最新时间。

然后，我们可以检查最后一次页面活动是在多久之前，如果需要，可以根据时间比较进行刷新。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)