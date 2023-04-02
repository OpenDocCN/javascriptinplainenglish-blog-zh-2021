# 如何使用 Count API 计算页面浏览量

> 原文：<https://javascript.plainenglish.io/how-to-count-page-views-with-the-count-api-afc9369c1f8f?source=collection_archive---------2----------------------->

## 用 JavaScript 计算页面浏览量的简单方法。

![](img/fb5832d545882cb575a090f9cc3c4601.png)

Image created with ❤️️ By [author.](https://mehdiouss315.medium.com/)

# 介绍

你可能需要在你的网站上有一个有用的功能，那就是计算你的网页浏览量的计数器。最简单的方法是通过 CountAPI，它给了你这个惊人的功能。

在这篇文章中，我们将学习如何使用 JavaScript 中的 CountAPI 来计算页面浏览量。让我们开始吧。

# CountAPI

这个 API 允许你制作数字计数器。这是一个非常有用的 API 来跟踪一个页面的点击数。例如，它还允许您知道点击按钮的用户数量。所以它也计算事件。

每次调用 [CountAPI](https://countapi.xyz/) 提供一个命中端点，计数器就会加 1。

请点击以下链接查看:

```
[https://api.countapi.xyz/hit/](https://api.countapi.xyz/hit/namespace/key)[**namespace**](https://api.countapi.xyz/hit/namespace/key)[/](https://api.countapi.xyz/hit/namespace/key)[**key**](https://api.countapi.xyz/hit/namespace/key)
```

您应该知道，每个计数器都是用一个*键*在一个*名称空间*中标识的。*名称空间*应该是唯一的，所以您需要用您的网站域来替换它。

# 例子

假设您想要统计和显示您的网页浏览量，CountAPI 允许您通过使用他们的 NPM 包、JSONP、XHR 或 jQuery 来做到这一点。

在下面的例子中，我们将使用 JSONP。你可以稍后在他们的[网站](https://countapi.xyz/)上查看其他方式。

我们要做的第一件事是创建我们的 HTML:

```
<body>

  <h1>This page got <span id="**visits**"></span> views.</h1></body>
```

在 head 标签中，您必须为 CountAPI 添加一个脚本 CDN。它将如下所示:

```
<head><script async src="https://api.countapi.xyz/hit/**mysite.com**/visits?  callback=**callbackName**"></script></head>
```

你必须用你自己的域名替换`mysite.com`。此外，用我们将在下面的 JavaScript 中创建的任何回调名称替换`callbackName`。

现在我们将使用 JavaScript 来创建一个回调函数，该函数将获取访问量，并将其替换到 ID 为`visits`的元素中。

```
function **callbackName**(response) {
    document.getElementById('visits').innerText = response.value;
}
```

我们不会调用这个函数，因为它已经在上面的 CDN 中被调用过了。

如果您想了解一下，下面是 Codepen 示例:

The CountAPI.

正如你所看到的，这是统计你的网页访问量的最简单的方法。

# 结论

CountAPI 使得统计页面浏览量并在页面上显示它们变得更加容易。这个 API 也有更多的功能，我鼓励你去他们的网站上查看。

感谢您阅读本文，希望您觉得有用。

# 更多阅读

*如果你也对 JavaScript 和 web 开发相关的更有用的内容感兴趣，也可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*

*下面是另一篇有用的文章，请点击下面的链接查看:*

[](https://medium.com/javascript-in-plain-english/fetching-data-with-useeffect-in-react-604ed53edffe) [## 在 React 中使用 UseEffect 提取数据

### 通过真实的例子了解 React UseEffect。

medium.com](https://medium.com/javascript-in-plain-english/fetching-data-with-useeffect-in-react-604ed53edffe)