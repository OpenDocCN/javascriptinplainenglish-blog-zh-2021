# 如何在 Ionic 5/Angular 10 中实现 OAuth 2 认证

> 原文：<https://javascript.plainenglish.io/how-to-implement-oauth-2-authentication-in-ionic-5-angular-10-36c571260299?source=collection_archive---------2----------------------->

## 使用 SafariViewController 和电容器。

![](img/e1a25f6c22777668456e049159ac09ef.png)

Photo by [Christian Erfurt](https://unsplash.com/@christnerfurt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我的公司的主要项目是建立一个应用商店和谷歌 Play 商店应用。我决定使用 Ionic，当我在 2021 年初开始这个项目时，它已经是第 5 版了。

到目前为止，在将我的纯 Angular web 应用程序重写为混合 Ionic 应用程序时，我遇到的最大障碍之一是重新设计用户登录过程中的一个重要步骤:OAuth 2 身份验证。

OAuth 2 过程包括将用户发送到第三方网页，用户在那里登录，并使用一些凭证重定向回来。第三方只需要一个重定向 URL。然而，在原生应用程序上，将用户带到网页并让他们返回原生应用程序并不那么直观。

很难想象我最终想出的方法能在一个本地应用上实现这一点。我在网上找到的关于 Ionic 5 和电容的信息有限。

在解释我做了什么之前，我想说明一下，到目前为止，我只在运行 iOS 14 的 iPhone 上进行了测试。此外，我最初使用 Ionic 的[应用内浏览器插件](https://ionicframework.com/docs/native/in-app-browser)完成了 OAuth 2 认证。然而，我的方法很粗糙，利用了应用内浏览器允许访问用户在会话中访问的每个 URL 这一事实。因此，我让 OAuth 2 服务器将用户重定向到一个名为`https://lazytexts?…`的虚假 URL。我监听代码中要加载的 URL，提取查询参数，然后像往常一样继续。

经过进一步的研究，包括阅读雅克·l·切罗的这篇文章，我意识到，不出所料，应用内浏览器是不安全的，不推荐使用。而且，它看起来不太美观。

SafariViewController 显然是正确的选择。SafariViewController 优于 InAppBrowser 的一个具体优势是，用户可以访问 iCloud 钥匙串、自动填充和 cookies。因此，对于已经登录了自己的帐户或保存了密码的用户来说，登录第三方 OAuth 2 服务器要顺畅得多。

由于 SafariViewController 禁止读取用户访问的 URL，我不得不将用户重定向到一个自定义的 URL 方案，将他们带回应用程序。 [Ionic Deeplinks 插件](https://ionicframework.com/docs/native/deeplinks)允许我创建这个自定义网址`lazytexts://`，如果在 Safari 中输入，会将用户带到应用程序。不幸的是，这个插件的本意是在用户被重定向回来时调用一个函数，但是它从来没有被调用过。

这让我想到了一个名为 App 的[电容插件，它附带了一个功能，可以为将用户带到你的应用的 URL 添加一个监听器，非常适合我设置的自定义 URL 方案。随着函数被调用，我收到了带有 OAuth 凭证的 URL，并可以关闭 SafariViewController，继续正常运行。](https://capacitorjs.com/docs/apis/app#addlistener)

希望这对你有所帮助。如果你有任何问题，请在评论中告诉我，我很乐意回答。

*—查理·莱文*

*更多内容请看*[*plain English . io*](http://plainenglish.io/)