# 曲奇简介🍪在 JavaScript 中

> 原文：<https://javascript.plainenglish.io/cookies-in-javascript-f7fe9b5c01c2?source=collection_archive---------10----------------------->

## 了解 JavaScript 中的 Cookies。

![](img/5cf31479ceda18a5fe3e24a81117900d.png)

Photo by [Daria Shevtsova](https://unsplash.com/@daria_shevtsova?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/laptop-and-cookie?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

> 一个 **HTTP cookie** (网络 cookie，浏览器 cookie)是服务器发送给用户网络浏览器的一小段数据。浏览器可以存储 cookie，并将其与稍后的请求一起发送回同一服务器。通常，HTTP cookie 用于判断两个请求是否来自同一个浏览器——例如，保持用户登录。它为无状态的 HTTP 协议记住有状态的信息。—([MDN cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies))

# **另外，**

**Cookies** 主要用于存储和跟踪信息，如偏好、会话管理和其他改善用户体验或网站统计所需的详细信息。cookie 包含字符串形式的信息(用分号分隔的名称-值对模式)。我们可以使用 JavaScript 直接创建、检索和修改 cookies。

> **注意**:可以限制 cookie 的名称、值和长度。

# 曲奇中的字段

一个 Cookie 可以存储如下五个字段—

*   **到期**—cookie 的到期日期。如果没有提供到期时间，那么 cookie 将在访问者退出浏览器时到期。
*   **域**—您站点的域名。
*   **路径**—设置 cookie 的目录或网页的路径。如果要从任何目录或网页中检索 cookie，请将此字段留空。
*   **安全**——仅当该字段包含单词“安全”时，才会通过安全服务器检索 cookie。如果此字段为空，则不存在此类限制。
*   **Name = Value**—cookie 以键值对的形式进行设置和检索。

> **注意:**请记住，最终用户可以看到并修改所有 cookie 值。

# **饼干的种类**

1.  **第一方 cookie**—仅由您的网站创建和阅读的 cookie。
2.  **第三方 cookies** —由第三方广告在您的网站上制作的 cookies。由任何运行广告代码的网站阅读，用于个性化或特定目标的广告。
3.  **会话 cookie**—保存在浏览器上的 cookie，在浏览器关闭时销毁。

# 正在创建 Cookie

我们可以在 JavaScript 中使用字符串格式的`document.cookie`属性创建 cookie，用分号分隔成对(键值)。

示例:

```
document.cookie = "key1=value1; expires=date; path=/;";
```

现在让我们看看下面不同的 cookie 示例:

**存储信息**如用户名:

```
document.cookie = "username=medium/nikhil";
```

**cookie 的有效期**:

```
document.cookie = “username=medium/nikhil; expires=Thu, 28 Dec 2021 12:00:00 UTC”;
```

如果未提供到期日期，则关闭浏览器时会删除 cookie。

**Path** 让浏览器知道 cookie 属于哪个路径:

```
document.cookie = “username=medium/nikhil; expires=Thu, 28 Dec 2021 12:00:00 UTC; path=/”;
```

默认情况下，如果在创建 cookie 时没有声明，cookie 属于当前页面。

> **注意**:我们可以用这个方法设置/更新一个 cookie

# 阅读 Cookie

将 JavaScript 中的 cookie 读作如下是简单而容易的:

```
let cookies = document.cookie;
```

> **注意** : `document.cookie`像`cookies=”key1=value1; key2=value2; key3=value3”`一样在单个字符串中返回所有的 cookies

# 更新 Cookie

与我们创建 cookie 的方式类似，我们也可以更新它们:

```
document.cookie = “username=medium/new; path=/”;
```

> **注意**:这将覆盖先前的 cookie 值

# 删除 Cookie

很简单，我们可以根据何时删除 cookie 的要求给 cookie 添加一个截止日期。

```
document.cookie = “expires=Thu, 28 Dec 2021 12:00:00 UTC; path=/”;
```

如果我们想马上删除它，那么就把`max-age`更新为零

```
document.cookie = “max-age=0”;
```

或者，将到期日期更新为过去的日期。

另外，别忘了我们只处理一个 cookie。因此，一旦创建，我们总是更新或附加到现有的 cookie，以避免覆盖 cookie。

> **注意**:有些浏览器需要路径值来允许删除 cookie

# RT21【参考文献

*   [https://developer . Mozilla . org/en-US/docs/Web/API/Document/cookie](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie)
*   [https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
*   [https://www.npmjs.com/package/js-cookie](https://www.npmjs.com/package/js-cookie)

# **直到下一次**

希望这篇文章对你有用，感谢你阅读它。如果您有任何反馈，也请分享。

我在@buymeacoffee 上。如果你喜欢我的作品，你可以给我买一幅☕，分享你的想法🎉[https://www.buymeacoffee.com/nikhilwali2](https://www.buymeacoffee.com/nikhilwali2)

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*