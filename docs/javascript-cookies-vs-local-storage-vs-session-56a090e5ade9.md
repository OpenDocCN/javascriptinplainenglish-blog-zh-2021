# JavaScript Cookies vs 本地存储 vs 会话

> 原文：<https://javascript.plainenglish.io/javascript-cookies-vs-local-storage-vs-session-56a090e5ade9?source=collection_archive---------10----------------------->

## JavaScript 中的 Cookies vs 本地存储 vs 会话，举例说明。

![](img/15f0f599c8be9515e62cf70aa0cd6ac3.png)

Photo by [Claudio Schwarz](https://unsplash.com/@purzlbaum?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 向我们展示了在浏览器中存储数据的三种主要方式，即通过 cookies、本地存储或会话。当您希望在浏览器中存储一些数据用于身份验证或其他目的时，这三种方法都非常重要。

根据您的偏好，许多人喜欢选择在浏览器上存储数据的所有三种方式。所有这些方法都有它们的不同和相似之处，这就是为什么我们更喜欢一些而不是另一些的原因。在本文中，我们将探讨在浏览器中存储数据的所有这三种方式，并比较它们之间的潜在差异。

## **饼干**

Cookies 是在用户浏览器上存储数据的一种方式。Cookies 在一个独立的 bowser 上存储信息。假设你使用的是 chrome 浏览器；网站 cookies 将存储在 chrome 浏览器上，而不是您系统中的任何其他浏览器上。

在这种情况下，cookie 是独立于浏览器的，用户不能在它们之间共享 cookie。因此，使用 cookies 来存储特定用户信息是很重要的。
Cookies 始终可用，并且可从您使用的任何浏览器中的任何窗口选项卡访问。

另一方面，支持 HTML4 和 HTML 5 的浏览器也支持 cookies。使用 cookies 时，过期时间被手动设置为某个时间，在此之后，它将不再可用和可访问。与其他存储类型不同，对于大多数浏览器，cookies 最多只能存储 4 千字节的信息。

与本地存储和会话存储相比，这使得 cookies 在信息存储方面要小得多。
cookie 存储在浏览器中，每当用户向服务器发出请求时，就会发送到服务器。

cookies 较小的原因是因为它们可以在服务器上高效地实现，从而加快响应速度。假设 cookies 较大，并且被发送到服务器，这将导致服务器的响应较慢。这就是为什么建议将 cookies 做得尽可能小和有限，以确保更快的服务器响应时间的主要原因。

**如何使用 cookies 存储数据并设置到期日期。**

```
document.cookie= “user=John; expires=’+ new Date(2021, 9, 24).toUTCString()
```

这里我们设置了 cookie，它在 2021 年 9 月 24 日到期。这只是一个简单的方法，我们可以设置一个 cookie，并定义其到期时间。

## **本地存储**

本地存储是我们在浏览器中存储信息的另一种方式。与 cookies 不同，只有支持 HTML5 的浏览器才支持本地存储。

同样，本地存储一经设置，也可在同一浏览器的任何浏览器窗口选项卡上使用。本地存储比所有其他方法具有更高的存储容量，可以存储高达 10 兆字节的信息。

与随请求一起发送到服务器的 cookie 不同，本地存储只在浏览器上可用，不会随请求一起发送到服务器。就过期而言，本地存储不会像其他方法那样过期。

**如何使用本地存储器存储数据。**

```
//set itemlocalStorage.setItem(‘user’, ‘John’)//remove itemlocalStorage.removeItem(‘user’)
```

## **会话存储**

会话存储是我们可以在浏览器上存储数据的另一种方法。与我们上面看到的其他方法不同，会话存储略有不同。

会话存储像本地存储一样将信息存储在浏览器上，并且在服务器发出请求时不会随请求一起发送。会话存储可以存储高达大约 5 兆字节的信息。就容量而言，它似乎介于 cookie 和本地存储之间。当您关闭浏览器选项卡时，会话存储正好到期。

它们也只能在同一选项卡上访问。这意味着如果您打开另一个选项卡，它们将无法在该窗口选项卡上使用和访问。这与 cookiess 有很大的不同，在 cookie 中我们可以设置过期时间和永不过期的本地存储。
就像 cookie 和本地存储一样，在支持 HTML5 的浏览器中也支持会话存储。

**如何使用会话存储来存储数据。**

```
sessionStorage.setItem(‘user’, ‘John’)
```

所有这些用来在浏览器上存储信息的方法都有其相关的区别和相似之处，正如我们在上面所看到的。这取决于你在做什么，它们都很重要，而且在今天仍然相关。

## **最终想法**

感谢您花时间阅读这篇文章，希望对您有所帮助。

如果你有同事或朋友会喜欢这篇文章，如果你能告诉他们，我会很高兴。

## **更多内容:**

[](/5-projects-you-can-build-in-a-week-that-will-get-you-hired-c9e88c17753b) [## 你可以在一周内完成 5 个项目，让你被录用

### 如何建立一个基于项目的编程组合，给招聘人员留下深刻印象并吸引他们，让你被聘用。

javascript.plainenglish.io](/5-projects-you-can-build-in-a-week-that-will-get-you-hired-c9e88c17753b) [](/how-to-handle-registration-forms-with-vue-js-da3cdeb659e) [## 如何用 Vue.js 处理注册表单

### 用 Vue.js 向 API 端点发送用户信息。

javascript.plainenglish.io](/how-to-handle-registration-forms-with-vue-js-da3cdeb659e) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)