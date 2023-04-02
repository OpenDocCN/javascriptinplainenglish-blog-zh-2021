# 编写安全 JavaScript Web 应用程序的 7 个实用技巧

> 原文：<https://javascript.plainenglish.io/7-practical-tips-to-write-a-secure-javascript-web-application-4424fa1facec?source=collection_archive---------8----------------------->

## 你想让自己领先于攻击者吗？

![](img/e61d04d0eb4828b6417e45845f2e707a.png)

Photo by [Kevin Ku](https://unsplash.com/@ikukevk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

与几乎所有编程语言一样，JavaScript 并不缺乏安全漏洞。通过滥用 JavaScript 漏洞，人们可以操纵数据、修改和窃取数据、重定向浏览器会话等。

虽然 JavaScript 通常被认为是一个客户端应用程序，但是 JavaScript 安全性问题也会给服务器端带来挑战。了解常见的 JavaScript 安全漏洞是防范这些漏洞的最佳方法。一个好的防御是意识到威胁并实施适当的控制以最小化风险。

在这篇文章中，我将告诉你编写一个安全的 JavaScript web 应用程序的七个实践。我相信当你一个一个地阅读它们时，会对你有所帮助。

# 1.验证用户输入以限制 SQL 注入和 XSS 攻击

顾名思义，当黑客能够在您的数据库上执行 SQL 语句时，就会发生 SQL 注入攻击。如果来自前端的输入没有被净化，这是可能的。换句话说，如果 Node.js 后端从用户提供的数据中提取参数，并将其直接合并到 SQL 语句中。

有几种方法可以避免这种情况，但基本思想是不要盲目地从前端向数据库查询赋值。

相反，您必须验证或转义用户提供的值。如何做取决于您正在使用的数据库以及您喜欢如何做。一些 JavaScript 数据库库自动执行转义。然而，也可以使用更通用的文库，如 Sequelize 或 Knex。

# 2.实施强身份验证

第二个最常见的漏洞是被破解的、脆弱的或不完整的身份验证机制。这当然是因为许多开发人员认为认证是“我们拥有它，所以我们是安全的。”但在现实中，弱的或不一致的身份验证很容易规避。一种选择是使用预先存在的认证系统，如 Auth 或 Okta。

如果您想使用原生 JavaScript 身份验证解决方案，有一些事情需要记住。创建密码时，避免使用 Node.js 中的内置加密库，而是使用 Bcrypt 或 Scrypt。

限制失败的登录尝试，如果用户名或密码不正确，不通知用户。而是返回一般的“不正确的凭据”错误。此外，还需要适当的会话管理策略。

此外，确保使用双因素身份验证。如果操作正确，它可以显著提高应用程序的安全性。您可以使用 node-2fa 或 speakeasy 之类的模块来实现这一点。 [Rishikesh Dhokare](https://medium.com/u/b7934e106470?source=post_page-----4424fa1facec--------------------------------) 分享了一份关于使用 Node.js 实现双因素认证的指南。请查看:

[](https://rishikesh-dhokare.medium.com/implementing-2-factor-authentication-2fa-a2a6a8dd48d8) [## 实施双因素身份认证(2FA)

### 用 Node.js 和 Authy 实现 2FA

rishikesh-dhokare.medium.com](https://rishikesh-dhokare.medium.com/implementing-2-factor-authentication-2fa-a2a6a8dd48d8) 

# 3.避免暴露太多的错误

这里有一些事情需要记住。

第一步是确保用户不知道错误细节，例如通过向客户端返回完整的错误对象。虽然您可以存储不想公开的信息，比如路径、附加库，甚至是秘密，但是您必须对这些信息进行适当的加密、验证和隐藏。

另一件要注意的事情是用 catch 子句包装路由，因为如果请求触发了错误，Javascript 将会崩溃。通过创建持久请求签名，我们可以防止攻击者试图使您的应用程序崩溃，并一次又一次地发送相同的恶意请求，从而使您的应用程序不断崩溃。

然而，对于您的 JavaScript 应用程序，您应该采取一些额外的预防措施。不要把你的 JavaScript 应用直接放到互联网上。利用一个前端组件，比如云防火墙、负载均衡器，或者使用你已经准备好的 Nginx。这使得您可以在 DoS 攻击到达您的 JavaScript 应用程序之前就对其进行限制。

# 4.运行自动漏洞扫描

另一方面，JavaScript 生态系统由许多可以安装的库和模块组成。在您的项目中包含大量这样的元素是非常常见的。这带来了安全问题，因为你不可能知道别人写的代码是安全的。您应该定期执行自动漏洞扫描来帮助解决这一问题。它们帮助您定位存在已知安全缺陷的依赖项。

# 5.避免数据泄露

你不记得我们之前劝过你不要相信前端了吗？此外，您不应该信任来自前端的数据，也不应该信任您发送给它的内容。在将数据发送到前端之前，不必过滤特定对象的所有数据，可以将所有数据发送到前端，然后应用过滤器。然而，对于黑客来说，获取从后端传输的隐藏数据的挑战是非常低的。

假设您想要显示已注册某个事件的用户列表。您运行一个 SQL 查询来获取该特定事件的所有用户，并将信息发送到前端，在前端对信息进行过滤，只显示名字和姓氏。然而，您不想显示的所有数据，如用户的出生日期、联系信息、电子邮件地址，都可以通过 web developer console 轻松访问。结果导致数据泄露。

你将如何解决这个问题？不要发送除所需数据之外的任何内容。您只需要名字和姓氏，所以只从数据库中检索这些名字。

# 6.设置日志记录和监控

尽管日志记录和监控对安全性很重要，但您可能认为它们实际上并不相关。然而，这不是真的。

毫无疑问，总体目标是从一开始就创建安全的系统，但要真正实现这一目标，必须是一个持续的过程。要启用这些功能，您将需要日志记录和监控。有些人希望看到您的应用程序不可用，这样他们就可以修复导致这种情况发生的漏洞。但是，另一方面，一些黑客会选择长时间不被发现。

有时，当出现问题时，监控日志和指标将帮助您发现是否有问题。如果您只使用基本的日志记录，您将无法收集足够的信息来了解看起来奇怪的请求是来自您自己的应用程序、第三方 API 还是来自黑客。

# 7.使用安全棉绒

我们之前讨论了自动漏洞扫描，但是您可以在编写代码时更进一步，寻找常见的安全漏洞，而不是只检查代码何时编写。要扩张，怎么扩张？为了提高代码质量，应该使用 linter 插件，比如 eslint-plugin-security。每当您使用可能使您的站点暴露于攻击的代码实践时，安全提示会提醒您。

希望你喜欢这篇文章！

加入我，了解更多关于编程的有用见解。

## 进一步阅读

[](/11-javascript-concepts-every-web-developer-should-know-to-take-their-skills-to-the-next-level-37ef6693111a) [## 每个 Web 开发人员都应该知道的 11 个 JavaScript 概念，让他们的技能更上一层楼

### 不了解这些概念，就无法掌握 JavaScript。

javascript.plainenglish.io](/11-javascript-concepts-every-web-developer-should-know-to-take-their-skills-to-the-next-level-37ef6693111a) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)