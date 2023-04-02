# 使用 Vonage 进行 OTP 验证

> 原文：<https://javascript.plainenglish.io/otp-verification-with-vonage-b7ddc4a64b28?source=collection_archive---------8----------------------->

![](img/2ff88dfdefb5c78ac2e98ddec7662ab2.png)

Photo by [Firmbee.com](https://unsplash.com/@firmbee?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/sms?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

OTP 验证已经成为现代 web 和移动应用程序的一个常见特征。无论是用户注册、多因素认证还是密码更改机制，OTP 验证似乎都是最完美的选择。此外，短信或电话验证被认为比电子邮件链接更安全可靠。

在本文中，我将解释 Vonage 与 Node.js (Express)服务器集成的验证 API。它还提供了一个 OTP 特性，因此您不必每次都重新发明轮子。你可以点击查看更多信息[。](https://www.vonage.com/communications-apis/verify/)

让我们从一个非常基本的 express 服务器开始。

**server.js** 文件包含一个非常基本的 web 服务器，有 2 个路由。

*   /API/请求令牌
*   /API/验证令牌

每个端点的业务逻辑都在`vonage.service.js` **中。**服务文件使用`@vonage/server-sdk`；Vonage API 的官方 JS 库。订购该服务后，可在仪表板上获得`Vonage API Key`和`API Secret`。

服务文件有三种方法:请求、验证和取消令牌。

首先，`vonage`对象用从 Vonage 获得的 apiKey 和 secret 首字母签名。整个工作流程有两部分:请求代码&验证。让我们深入探讨每一个问题。

# 请求 OTP

该方法的一项工作是向给定的电话号码发送 OTP 令牌。Vonage 验证服务以一种冷静的方式处理它。截至写这篇文章的时候，它发送短信给指定的号码。如果 OTP 在这段时间内没有被验证，它会调用 SIM 卡上的号码，或者在我的情况下，它会调用 Viber 上的号码。当你得到 OTP 代码后，你可以把它发送给 API 进行验证。这一过程看似简单，但在实施过程中可能会很棘手。

> 我遇到的一些警告:
> 
> -无法在 30 秒间隔内向电话号码发送并发 OTP。
> 
> -无法多次取消 OTP 请求。如果这样做，它将反复抛出错误。

考虑到这几点，让我们从代码开始。首先让我们完成`vonage.service.js`文件中的`requestCode`方法。

该方法获取一个电话号码，并返回最重要的内容`request_id`。

> 通常情况下，您无法访问 Vonage 发送的 OTP 代码。如果您需要，请访问他们的[定价部分](https://www.vonage.com/communications-apis/verify/pricing/)。

如果您得到了响应`request_id`，这是一个成功的请求，否则就有一些错误。

该机制的另一部分是取消令牌请求。可能存在需要取消 OTP 请求的情况。其中一个突出的原因是:Vonage 对 OTP 到期有 5 分钟的限制。在现实世界中，这是一个漫长的等待。最坏的情况:谁等了 5 分钟才收到 OTP😂

因此，您可能需要取消挂起的请求并重新发送另一个 OTP。取消请求的代码如下所示。

这是一个非常简单的代码，需要 OTP 的`request_id`来取消它。正如您可能已经看到的，`request_id`是跟踪您的 OTP 的唯一方法。所以，要安全存放。

这两种方法足以申请一个动态口令。现在让我们转到`server.js`来实现这些方法。

首先，检查电话号码是否存在。然后删除所有现有的空白。有时电话号码的格式很奇怪(+12 345 678 890)。这可能会给 Vonage 等服务带来问题。但是它需要国家代码。

基本上，上面的代码通过`vonage.service.js`请求 OTP。如果成功，则执行`onOtpSuccess`功能，如果错误，则执行`onOtpError`。如果在 5 分钟内并发 OTP 请求相同的号码，Vonage 抛出状态为 10 的错误。这种情况是通过用其`request_id`取消 OTP 并重新发送请求来处理的。如果它再次失败，它被标记为错误。

至此，您已经了解了如何请求 OTP，如何取消它(如果需要的话)。另一个难题是验证 OTP。

# 验证 OTP

回想一下:我们有两个文件`server.js`、`vonage.service.js`和`request_id`是跟踪您的 OTP 的唯一方法。

与 OTP 请求机制不同，验证的逻辑非常简单。首先，我们来看一下`vonage.service.js`的实现。

验证通过以下方式完成

*   `request_id`存储在数据库中或从用户处接收
*   用户通过手机短信或电话收到的 OTP 代码。

成功验证将返回状态为 0 的结果。

转到`server.js`文件，`verifyOtp`方法是这样使用的。

这里，OTP 和`request_id`都是从 API 请求中获取的。这可能取决于您的实现。

这样，您可以将 OTP 代码发送到用户的设备，并使用 Vonage 的验证 API 对其进行验证。你也可以在 Vonage 的 JS 指南中找到一个基本的实现。本文为在 Express JS 服务器上实现它提供了更详细的指导。

*更多内容看*[***plain English . io***](http://plainenglish.io/)