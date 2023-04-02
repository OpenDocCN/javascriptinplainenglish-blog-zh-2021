# 提高网页性能的 JavaScript 技巧

> 原文：<https://javascript.plainenglish.io/javascript-tips-to-improve-your-webpage-performance-43eb2fe77ba6?source=collection_archive---------18----------------------->

## JavaScript 技巧

## 一些小技巧会让访问你的网站变得更加愉快。

![](img/3edcdcf35fea38932e20ab4780d2f11c.png)

Photo by [Domenico Loia](https://unsplash.com/@domenicoloia?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/site?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当你建立一个网站时，最重要的事情之一就是确保它的良好性能。当人们访问你的网页时，他们不想等待 10 分钟直到页面(和所有的图片)加载完毕。在一项调查中发现，47%的访问者期望网站在不到 2 秒的时间内加载，如果加载时间超过 3 秒，40%的访问者会离开网站。

许多网站都是基于 JavaScript 构建的，提高性能并不是一件容易的事情。然而，我会告诉你一些有效的方法。

## 1.局部变量

每当你调用某个函数时，用来定义该函数的变量都存储在里面。变量可以分为两种类型。

*   局部变量—仅在自身内部定义的变量。
*   全局变量—在整个脚本中使用的变量。

当你调用一个函数的时候，浏览器会进行一个叫做范围查找的活动。随着作用域链中作用域数量的增加，访问当前作用域之外的变量所需的时间也会增加。

这就是引擎访问全局变量比访问局部变量要花更长时间的原因。这意味着，如果您在本地定义大多数变量，那么引擎搜索它们所需的时间将会迅速减少。因此，它将提高应用程序的整体速度。

## 2.网络包

当通过分别添加新的 JavaScript 模块或脚本来增加文件大小时，您的代码只会越来越慢。

Webpack 是一个开源的 JavaScript 模块捆绑器。它主要是为 JavaScript 设计的。Webpack 使用现有模块创建依赖图。Webpack 浏览这些包并创建一个新包，其中包含运行应用程序所需的最少数量的文件。

## 3.位置

提高性能的最简单、最容易的方法之一是将 JavaScript 代码移到页面底部。因为当您的页面第一次加载时，它需要文本、图像等，只有在那时它才需要执行 JavaScript 代码。

## 4.Gzip 压缩

JavaScript 文件可能非常大，这可能会影响网站的加载时间。Gzip 是一个可以用来压缩你的 JavaScript 文件的软件。

当浏览器请求资源时，服务器在将响应发送到 web 浏览器之前对其进行压缩。该软件减小了 JavaScript 文件的大小，节省了带宽，并提高了网站的性能。

## 5.JavaScript 缓存 API

提高站点性能的第二种方法是在浏览器中使用缓存。当您的浏览器启动您的代码时，它会重复地再次打开相同的脚本。如果您正确使用缓存，它将在下次打开已经保存的脚本，性能将立即提高。

## 6.对 DOM 的访问

**DOM(文档对象模型)**是网页的面向对象表示，可以用脚本语言修改，比如 JavaScript **。**每当您在 JavaScript 本地环境之外与 DOM 交互时，浏览器都必须刷新页面。将 DOM 访问保持在最低限度或者在您的 web 应用程序中是很好的。

## 结论

我试图用 JavaScript 技巧找到提高网页性能的最佳方法。我自己已经用了一年多了。我只是想让你记住，人们喜欢他们打开的网页没有延迟和错误。这也是一件重要的事情。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)