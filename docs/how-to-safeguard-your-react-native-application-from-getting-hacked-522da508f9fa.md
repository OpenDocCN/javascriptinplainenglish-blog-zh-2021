# 如何保护你的 React 原生应用程序免受黑客攻击？

> 原文：<https://javascript.plainenglish.io/how-to-safeguard-your-react-native-application-from-getting-hacked-522da508f9fa?source=collection_archive---------1----------------------->

保护 React 本机应用程序的基本技巧。

![](img/941d1561cb1931e202b98154728e5ce3.png)

Photo by [Dan Nelson](https://unsplash.com/@danny144?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为软件开发人员，我们经常低估实现安全特性的需要。为什么这么问？可能性是时间限制，缺乏专业知识，以及没有意识到所涉及的风险。

不管你的理由是什么，你的应用程序没有强大的安全性可能会导致意想不到的后果。就像带着小刀去参加枪战。虽然在 react-native 开发人员社区中，安全性是一个很少被提及的话题，但是让我们来讨论几个可以帮助您提高应用程序安全性的话题。

# 风险

理解风险是构建安全应用程序的第一步。让我们看看有哪些风险。

![](img/c225013badb901adcca7f704d8dd51a5.png)

Photo by [David Perkins](https://unsplash.com/@prkns?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**1。源代码曝光—** 一个应用在发布时，不管是 APK 还是 IPA，都只是一组文件。因此，您的代码文件可以被检索到，并且可以根据黑客的需要进行修改。这个过程被称为**逆向工程**。有许多应用程序在更改名称和徽标后被黑客攻击并重新发布的实例。此外，API 密钥等机密信息也可能会暴露。

> **提示:**将您的 APK 重命名为`.zip`格式，并提取它以访问源代码。您将在 assets 文件夹下找到 JavaScript 包(` index.android.bundle `)。

**2。MITM 攻击(中间人)——**你的应用可能会像往常一样尝试连接到你的服务器，执行一些 CRUD 操作。由于您的应用程序不能直接连接到服务器，必须通过一堆节点传递请求，您永远不知道在传输过程中谁会读取或操作它。如果你正在传输一些机密信息，而中间的一个节点被劫持了，那么，你知道后果！

> **提示:**您可以使用 [traceroute](https://www.geeksforgeeks.org/traceroute-command-in-linux-with-examples/) cmd 来扫描到达您的服务器之前的所有中间节点。

**3。数据窃取—** 一些用户可能喜欢 **Root (Android)** 或 **JailBreak (iOS)** 他们的手机，这样他们就可以完全访问他们的设备。**root 或越狱**是在设备上获得超级用户/管理员访问权限的过程。虽然在某些情况下这可能有利于用户，但它也有风险，我们的应用程序可能会在不知不觉中将存储的机密信息泄露给可能存在于他们设备上的恶意软件。

# 预防

现在我们已经分析了相关的风险，让我们看看可以采取什么预防措施来避免它们。

![](img/6ede87ffb2abc132a0786771531e30e6.png)

Photo by [Franck](https://unsplash.com/@franckinjapan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**1。混淆—** 黑客很容易对你的发布包(APK/IPA)进行逆向工程，读取你的代码来识别一些有用的信息。或者只是运行一个程序在应用程序中堆叠字符串。**混淆** ***是一种将可读代码转换成混乱/不可读格式*的方法。**

考虑下面的例子。

```
const API_KEY = “secret_api_key”
```

虽然上面的代码非常容易阅读，但这是混淆后的样子。

```
const _0xa70b=['532750MhNjLH','5DgGdqr','54874PVlakR','382115TaFbUe','67GENUoI','2GhLNjt','secret_api_key','5024CxydOY','69109HGDkMY','2bpFgSB','83355fDshvP','7aVmHhi','226199XQnyXT'];function _0x41ec(_0x33bd57,_0x3c1d1c){_0x33bd57=_0x33bd57-(-0x1c55+0x8*0x241+0xf*0xcd);let _0x4be608=_0xa70b[_0x33bd57];return _0x4be608;}const _0x1e3b36=_0x41ec;(function(_0x5f34c8,_0x5c6f9a){const _0x103be6=_0x41ec;while(!![]){try{const _0x308fb4=-parseInt(_0x103be6(0x1bb))*-parseInt(_0x103be6(0x1b7))+parseInt(_0x103be6(0x1bf))*parseInt(_0x103be6(0x1bc))+parseInt(_0x103be6(0x1c1))*parseInt(_0x103be6(0x1be))+parseInt(_0x103be6(0x1b6))*parseInt(_0x103be6(0x1bd))+parseInt(_0x103be6(0x1ba))+parseInt(_0x103be6(0x1c2))+-parseInt(_0x103be6(0x1b9))*parseInt(_0x103be6(0x1b8));if(_0x308fb4===_0x5c6f9a)break;else _0x5f34c8['push'](_0x5f34c8['shift']());}catch(_0xb1027a){_0x5f34c8['push'](_0x5f34c8['shift']());}}}(_0xa70b,-0x103d*0x115+-0x12524c+0x2dbf10));const _0x47723e=_0x1e3b36(0x1c0);
```

那是什么？

你看到它是如何让黑客很难理解你的源代码了吗？嗯，它也有一个缺点。正如你在上面所注意到的，这将极大地增加包的大小。

你可以通过使用 [**JavaScript 混淆器**](https://github.com/javascript-obfuscator/javascript-obfuscator) 来实现这一点

也可以 [**在线试试。**](https://obfuscator.io)

**2。SSL 固定—** 为了确保服务器和客户端之间的安全连接，请始终通过 HTTPS 进行连接。 **HTTPS 协议**确保在**证书**的帮助下验证服务器身份，客户端可以在传输任何数据之前验证该证书。

通常在 MITM 攻击的情况下，中间节点中的攻击者可能伪装成合法的服务器。或者可以在您的本地网络中设置一个假的 DNS 服务器，将您的域名映射到一个恶意的 IP 地址。为了避免这种攻击，将证书固定在应用程序中并在连接时执行这两项检查也很重要。

*   **验证服务器提供的证书。**
*   **匹配运输时在应用程序中固定的证书。**

你可以在这个 [**Github 资源库**](https://github.com/MaxToyberman/react-native-ssl-pinning) 找到更多关于 SSL 钉住的信息。

**3。rooted 越狱检测—** 作为一项预防措施，最好检查设备是 root 还是越狱，这样您就不会冒应用程序的敏感数据暴露于恶意软件的风险。如果您发现设备被 rooted，您可以**阻止**用户**访问您的应用**，或者通过非机密设置授予**部分访问**。

你可以使用 [Jail Monkey](https://github.com/GantMan/jail-monkey) 来检测一个设备是否有根或者越狱。

# 结论

根据各种情况，可能无法始终实现最佳的安全特性。但是至少实现了其中的几个，肯定会让黑客更难攻击，你可以争取更多的时间来修复它们。

就是这样。希望你喜欢这篇文章，如果是的话，请随意鼓掌或在下面留下评论并与你的同事分享。那会激励我写更多这样的文章。请让我知道，如果从上述几点需要详细的实施。编码快乐！

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)