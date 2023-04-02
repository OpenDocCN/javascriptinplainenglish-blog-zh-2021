# 使用交叉点观察器 API 延迟加载图像的简要指南

> 原文：<https://javascript.plainenglish.io/lazy-load-images-with-intersection-observer-api-on-webpages-2270d29922c7?source=collection_archive---------13----------------------->

![](img/e153813a5d2b1104eff62810ab016269.png)

Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 什么是懒装？

延迟加载意味着在稍后阶段，当用户将要看到一个特定的项目或与之交互时，在网页上加载项目。

# 为什么有用？

假设你有一个在线商店网站，向用户展示成千上万的产品。当页面被加载时，您在视窗中只显示 10 到 20 个产品，因此为它们加载图像，但是您可能不想加载底部的产品图像，因为
如果我们在前面加载这些图像，而用户没有向下滚动来查看这些图像，那么将会浪费浏览器资源和下载这些资源的不必要的数据消耗。

# 如何使用交集观察者 API 来实现？

还有其他外部库支持这个特性，但是我们也可以使用 Intersection Observer API 来实现，这是一个本地的 web API。

默认情况下，所有图像都有`dataSrc`标签(而不是`src`标签),这对于浏览器是未知的，并且图像不会提前加载。

然后，我们在网页上的每个图像上设置一个交叉点监听器，一旦该图像与浏览器视窗相交，回调函数就会被触发。在回调函数中，我们通过从`dataSrc`标签复制值来设置`src`属性，现在由于`src`标签为浏览器所知，它将加载图像。最后，观察者从该图像中移除。

就是这样。你可以在 https://github.com/SaurabhGarg1/Lazy-load-images[找到完整的源代码](https://github.com/SaurabhGarg1/Lazy-load-images)