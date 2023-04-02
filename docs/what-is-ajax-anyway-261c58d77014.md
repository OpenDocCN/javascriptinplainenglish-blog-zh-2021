# 面向初学者的 AJAX

> 原文：<https://javascript.plainenglish.io/what-is-ajax-anyway-261c58d77014?source=collection_archive---------7----------------------->

## **AJAX 初学者指南**

*在这篇博文中，我想带你了解 AJAX 的基础知识，并展示一些简单的例子来帮助你入门。*

![](img/b1d3033393fddf1a2491fcddd7cd75e3.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

AJAX 代表 **A** 同步**J**avaScript**A**nd**X**ML。简单地说，就是使用 XMLHttpRequest 对象与服务器通信。更简单地说， **AJAX 是一种从网页访问 web 服务器的技术**。AJAX 允许通过在后台与 web 服务器交换数据来异步更新网页。这意味着无需重新加载整个页面就可以更新部分网页。

现代网站是高度互动的，必须能够动态响应用户的输入。例如，当用户在网站上创建一个新帐户时，必须检查他们的电子邮件，以确保该帐户尚未注册。只有当网站的单个组件可以被操作时，才能做到这一点。

AJAX 最大的好处是网站不再需要完全重新加载来响应用户输入。静态内容保持不变，而动态信息可以根据需要添加到 DOM 中。在上面的例子中，当创建一个新用户时，一个请求被发送到 web 服务器，它检查用户提交的电子邮件地址是否可用于创建一个新的配置文件。然后，这些数据被发送回客户端。

如果没有 AJAX，表单将被提交，整个页面将被重新加载。但是 AJAX 允许您随时使用 JavaScript 向服务器发送请求。

如果需要更多的 AJAX 例子，可以考虑用 Google Maps 交互；用户可以使用鼠标拖动整个地图。或者当你在谷歌上搜索某样东西时，谷歌会在你输入的时候实时向你提供建议。有了 AJAX，网站可以更好地响应用户输入，并具有更深层次的交互性。

## 数据交换

为了交换数据，必须创建一个 *XMLHttpRequest* 对象。 *XMLHttpRequest* 是一个 API，JavaScript 和其他 web 浏览器脚本语言可以使用它来使用 HTTP 在 web 服务器之间传输和操作 XML 数据，因此基本上 *XMLHttpRequest* 对象是客户端和服务器之间的中间人。

有两种方法可以与服务器交换数据。第一种方式是 GET 请求。在 GET 请求中，数据作为 URL 参数发送。不建议使用大量数据(例如表单数据)向服务器发出 GET 请求。在这种情况下，最好使用 POST 请求。在 POST 请求中，数据作为 HTTP 请求体的一部分发送到服务器。

正如我已经提到的，AJAX 使用异步数据传输。这意味着在传输数据的同时，用户可以执行其他操作，并保持与网页的交互。

浏览器从服务器得到的响应可以是 XML、纯文本或 JSON 格式。如果收到纯文本格式的响应，则它可以立即显示在页面上。当收到 XML 响应时，客户端处理 XML 并将数据转换成 HTML。当接收到 JSON 响应时，客户端只需要用 *eval* 函数执行接收到的代码，就可以得到一个完整的 JavaScript 对象。

总而言之，AJAX 是如何工作的:

-页面加载后，用户可以引发一个事件。例如，通过点击按钮。

-单击按钮后，JavaScript 会创建一个 *XMLHttpRequest* 对象。

-对象向服务器发送请求。

-服务器接收请求，处理请求并创建响应。

-响应被发送回浏览器。

JavaScript 读取响应，并根据响应更新部分网页。

在客户机和服务器之间执行 AJAX 通信之前，首先要实例化一个 *XMLHttpRequest* 对象。

```
var request = new XMLHttpRequest();
```

为了创建一个服务器请求，我们使用新创建的对象的 **open()** 和 **send()** 方法。

*   **open( *方法，url，async* )** — ***方法*** 指定请求的类型，GET 或 POST***URL***-将请求发送到哪里； ***async*** —真或假，默认设置为真。服务器请求应该异步发送，因此 JavaScript 可以在等待服务器响应的同时执行其他脚本。
*   **send()**/**send(*body*)**—向服务器发送 HTTP 请求。

下面是一个简单的 GET 请求的例子，它用于从服务器中检索一些不需要任何修改的数据。当用户点击一个按钮时，它触发 **createRequest** 函数。发出请求，然后将执行( **onreadystatechange** )传递给 **alertContents()** 。如果我们收到状态 OK ( **200** )，当我们看到一个带有服务器文件内容的警告弹出窗口。

注意 **onreadystatechange** —它是 *XMLHttpRequest* 对象最重要的属性之一。该属性定义了当**就绪状态**改变**时要执行的功能。**

**readyState** 是指定 HTTP 请求的整数。可能的值有:

0 —未发送—已经创建了一个 *XMLHttpRequest* 对象，但是还没有调用 **open()** 方法；

1 —打开—调用了 **open()** 方法(建立了服务器连接)；

2 — HEADERS_RECEIVED —调用了 **send()** 方法(接收到请求)；

3 —加载—服务器正在处理请求；

4 —完成—请求已处理，响应已准备好。

在检查了请求的状态和响应的 HTTP 状态代码之后，您可以对从服务器接收的数据做任何事情。

为了发布数据，我们需要添加一个带有 **setRequestHeader()** 的 HTTP 头。

*   **setRequestHeader(*header _ name，value* )** —设置请求头的值；

您必须在 **send( *body* )** 方法中指定您想要发送的数据。

总而言之，AJAX 是创建快速动态网页的一种非常有用的技术。使用 AJAX 的主要优点是它简化了用户体验。一个有效使用 AJAX 的构建良好的网站会运行得更快，并为用户提供更好的体验。我希望这篇 AJAX 介绍对您有用。感谢阅读。

资源:

[](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started) [## 入门指南

### 本文将引导您了解 AJAX 基础知识，并提供一些简单的动手示例来帮助您入门。

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started) [](https://www.w3schools.com/js/js_ajax_intro.asp) [## AJAX 简介

### AJAX 是开发人员的梦想，因为您可以:从 web 服务器读取数据-在页面加载后更新网页…

www.w3schools.com](https://www.w3schools.com/js/js_ajax_intro.asp) [](https://www.tutorialspoint.com/ajax/what_is_xmlhttprequest.htm) [## AJAX - XMLHttpRequest

### XMLHttpRequest 对象是 AJAX 的关键。自从 Internet Explorer 5.5 在…发布以来，它就一直可用

www.tutorialspoint.com](https://www.tutorialspoint.com/ajax/what_is_xmlhttprequest.htm)