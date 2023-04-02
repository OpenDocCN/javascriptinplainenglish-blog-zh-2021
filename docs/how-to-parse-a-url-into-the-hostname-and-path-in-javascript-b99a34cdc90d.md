# 如何用 JavaScript 把一个 URL 解析成主机名和路径？

> 原文：<https://javascript.plainenglish.io/how-to-parse-a-url-into-the-hostname-and-path-in-javascript-b99a34cdc90d?source=collection_archive---------20----------------------->

![](img/3cf11086df6f6bfd8d318500e12cc541.png)

Photo by [Kenan Kitchen](https://unsplash.com/@kitchen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 将 URL 解析成主机名和路径部分。

在本文中，我们将研究如何用 JavaScript 将 URL 解析成主机名和路径部分。

# 创建一个 a 元素

我们可以创建一个`a`元素并将它的`href`属性设置为我们想要解析的 URL，

然后我们可以得到它的属性来得到我们想要的部分。

例如，我们可以写:

```
const parser = document.createElement('a');
parser.href = "http://example.com:3000/pathname/?search=foo#hash";console.log(parser.protocol)
console.log(parser.host)
console.log(parser.hostname)
console.log(parser.port)
console.log(parser.pathname)
console.log(parser.hash)
console.log(parser.search)
console.log(parser.origin)
```

`protocol`有协议，是`'http:'`。

`host`是主机名和端口，也就是`'example.com:3000'`。

`hostname`是主机名，也就是`'example.com'`。

`port`是端口，是 3000。

`pathname`有路径名，是主机之后的路径，主机是`'/pathname/'`。

`hash`有 hash，也就是`#hash`。

`search`有前面带问号的查询字符串，就是`'?search=foo'`。

`origin`有协议和主机在一起，就是`‘ http://example.com:3000’`。

# URL 构造函数

URL 构造函数让我们无需创建`a`元素就可以解析 URL 的各个部分。

例如，我们可以写:

```
const url= new URL("http://example.com:3000/pathname/?search=foo#hash")console.log(url.protocol)
console.log(url.host)
console.log(url.hostname)
console.log(url.port)
console.log(url.pathname)
console.log(url.hash)
console.log(url.search)
console.log(url.origin)
```

我们将 URL 传递给`URL`构造函数，我们得到和以前一样的结果。

大多数现代浏览器都有`URL`构造函数。

# 结论

为了用 JavaScript 解析 URL，我们可以创建一个`a`元素并设置它的`href`属性。

或者我们可以将 URL 传递给`URL`构造函数来获得相同的结果。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)