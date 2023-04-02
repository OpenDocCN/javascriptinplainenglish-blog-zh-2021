# 如何保护 Node.js/Express 应用程序？

> 原文：<https://javascript.plainenglish.io/how-to-secure-node-js-express-apps-1d32312ff0a4?source=collection_archive---------8----------------------->

## 可以保护您的节点应用免受安全攻击的快速提示

![](img/5841d4adbccbb78695847576eb39ad70.png)

Node.js 是与 Express 等框架一起使用的最流行的运行时之一。它有一个蓬勃发展的开发者社区，深受每个人的喜爱。虽然使用 Node.js 进行开发是一种乐趣，但从安全角度考虑您构建的应用程序也很重要。

[John Au-Yeung](https://medium.com/u/5253c50d76c1?source=post_page-----1d32312ff0a4--------------------------------) 也写了一篇关于这个主题的快速阅读文章[这里](https://medium.com/swlh/node-js-best-practices-improving-security-2c772419d475)介绍了防止针对授权、根用法、eval 语句等的暴力攻击的方法。在本文中，我们将讨论一些简单而有效的技巧来保护您的 Node.js/Express.js 应用程序免受攻击，这将在本文中进一步展开。总之，这可以成为改进 Node.js 应用程序安全机制的有益指南。

让我们开始吧！

# 验证用户的输入

## 表单验证

开发任何软件应用程序的一个关键原则是确保流入应用程序的数据总是根据您的条件进行验证。如果没有验证，恶意输入可能会进入您的应用程序。

在 Node.js 中，我们可以充分利用拥有大量库的 NPM 注册中心。出于验证的目的，我们可以使用[验证器](https://www.npmjs.com/package/validator)和 [express-validator](https://www.npmjs.com/package/express-validator) 库。

例如，使用 validator 包，您可以进行简单的验证来检查输入的字符串是否是电子邮件:

```
const validator = require('validator');
validator.isEmail("abc@xyz.com");
```

同样，它提供了大量的操作，如`isAlpha`和消毒功能，如`escape`或`trim`。

Express validator 是另一个库，它是 Express.js 的中间件。这里显示了一个验证 API 调用的请求体中的字段的简单示例:

```
// ...rest of the initial code omitted for simplicity.
**const** { body, validationResult } = require('express-validator');

app.post(
  '/user',
  // username must be an email
  body('username').isEmail(),
  // password must be at least 5 chars long
  body('password').isLength({ min: 5 }),
  (req, res) => {
    // Finds the validation errors in this request and wraps them in an object with handy functions
    **const** errors = validationResult(req);
    **if** (!errors.isEmpty()) {
      **return** res.status(400).json({ errors: errors.array() });
    }

    User.create({
      username: req.body.username,
      password: req.body.password,
    }).then(user => res.json(user));
  },
);
```

详细文件请参见本页。

## 阻止 SQL 注入

再一次，当来自用户的输入没有被净化时，SQL 注入攻击就会出现。这会导致在表单字段中提交的 SQL 查询在数据库上执行。想象一下`DROP DATABASE dbName;`这样的操作会如何影响你的应用！它会清除数据。

在这种情况下，最直接的方法也是使用 validator(如上所述)这样的库来彻底净化输入，以确保特殊字符、奇怪的查询字符串等。在进入代码中的数据库层之前被移除。

## 避免类型不匹配

接下来，我们需要避免代码中的类型不匹配。例如，当我们的函数期望一个数字时，我们不能接收一个字符串。JavaScript 是一种弱类型语言。我们不需要预先指定变量的类型，JavaScript 会相应地尝试“键入”它。

虽然这在开发时可能更容易，但它可能会导致一些安全缺陷和错误。为了避免这种情况，我们可以在 JavaScript 中使用本机转换函数，例如:

*   号码(“123”)
*   字符串(123)

您可以使用许多其他类型转换。请务必查看[这一页](https://www.w3schools.com/js/js_type_conversion.asp)了解更多信息。

# 账户管理

## 密码哈希

应用程序的一个关键部分是用户管理。您的应用程序很可能包含允许用户登录的用户帐户。此类功能很可能会使用一些密码来登录。

密码被归类为敏感信息，应该以尽可能安全的方式存储，以免被错误的人滥用。密码管理的基本方法是加盐和散列。

哈希是指一种单向函数，它将输入转换为一串不可解码的字节。然而，仅仅使用散列并不能解决问题。攻击者可以很容易地使用查找表，其中包含最常用密码的预计算哈希，以比较您的应用程序数据库中的哈希(以防黑客攻击)。

这就是盐的用武之地。通过添加一个随机的“salt ”,我们将一个独特的字符串附加到用户提供的明文密码中，然后对其进行哈希处理。这样，使用查找表解码散列密码的概率大大降低。

对于 Node.js 或 Express.js 应用程序，我们可以利用 [BCrypt 库](https://www.npmjs.com/package/bcrypt)。

```
const bcrypt = require('bcrypt');
const saltRounds = 10;bcrypt.genSalt(saltRounds, function(err, salt) {
    bcrypt.hash(userPassword, salt, function(err, hash) {
         dbHelper.save(hash);
    });
});
```

上面是一个简单的例子，告诉你如何用几行代码就能做到这一点！

`saltRounds`是 salt 过程的回合数，它与散列的安全性相关。更多轮次=更安全，然而更多轮次=更昂贵的操作。

## 批准

帐户管理的下一部分是授权。简单来说，

> 授权是指定对资源的访问权限/特权的功能，它与一般信息安全和计算机安全有关，尤其与访问控制有关。
> 演职员表:[维基百科](https://www.wikipedia.com/en/Authorization)

因此，使用授权，我们可以确保只有正确的人/用户才能访问正确的资源。

在 Node.js/Express.js,，我们可以使用 [ACL 库](https://www.npmjs.com/package/acl2)来实现这一点。举个例子，

```
// allow function accepts arrays as any parameter
acl.allow("member", "blogs", ["edit", "view", "delete"]);
```

上述文档中的例子表明，我们允许“成员”对名为“博客”的资源进行“编辑”、“查看”和“删除”。

授权和认证都很重要。不要混淆这两者，每一方面都很重要。

> **认证**是确定某人确实是他们所声称的那个人的过程。
> 
> **授权**指的是决定谁被允许做什么的规则。例如，Adam 可能被授权创建和删除数据库，而 Usama 仅被授权读取。
> 学分: [StackOverflow](https://stackoverflow.com/questions/6556522/authentication-versus-authorization)

# 网络安全性

## HTTPS 和 SSL

除了您的应用程序，您还需要以安全的方式传输和接收数据，以避免任何窥探。今天，每个应用程序都应该支持 HTTPS 作为事实上的标准。

虽然不是 Node.js/Express.js,独有的，但对应用程序实施 SSL 加密的最简单方法是使用 LetsEncrypt。这是一项免费使用的服务，提供免费的 SSL 证书来保护您的应用程序域。

这应该适用于 web 服务器级别，比如 Nginx。请务必在此查看文档[。](https://letsencrypt.org/)

另一种方法当然是从你的云提供商那里获得 SSL 证书，比如 AWS 上的[Amazon Certificate Manager(ACM)](https://aws.amazon.com/certificate-manager/)。

## 安全标题

许多攻击可以通过一些关键安全报头的存在来防止。为了实现这个，我们可以使用[头盔](https://www.npmjs.com/package/helmet)。只需一行代码，您就可以启用多个安全头:

```
app.use(helmet());
```

以上内容翻译过来就是:

```
app.use(helmet.contentSecurityPolicy());
app.use(helmet.dnsPrefetchControl());
app.use(helmet.expectCt());
app.use(helmet.frameguard());
app.use(helmet.hidePoweredBy());
app.use(helmet.hsts());
app.use(helmet.ieNoOpen());
app.use(helmet.noSniff());
app.use(helmet.permittedCrossDomainPolicies());
app.use(helmet.referrerPolicy());
app.use(helmet.xssFilter());
```

简单，容易，有效！

# 其他人

## CSRF / XSRF 缓解

您可能需要缓解的另一种常见攻击是跨站点请求伪造。这种攻击诱使合法用户提交恶意内容。例如，让用户在登录时执行恶意脚本(已验证状态)。

使用 [csurf 库](https://www.npmjs.com/package/csurf)可以缓解这种攻击。这个包需要使用会话中间件或 cookie 解析器。最常见的是，它作为中间件与 Express.js 一起使用。点击查看文档[。](http://expressjs.com/en/resources/middleware/csurf.html)

这个中间件帮助创建一个 csrf 令牌，它将与网络调用一起传递。然后，将根据用户的会话或 cookie 来验证该令牌。在这里阅读更多。

## 包和依赖项

虽然 NPM 存储库非常庞大，并提供了一种简单易用的方法来扩充您的应用程序，但我们也需要采取预防措施，以应对由于过时的软件包而带来的安全风险。

因此，定期监控以确保所有软件包都是最新的是必要的。我们可以使用`npm audit`命令很容易地做到这一点，并用`npm audit fix`自动修复可修复的问题。

就这么简单！

# 结论

今天，我们开发的应用程序的安全性在确保您的服务的稳定性、可靠性和持久性方面占据了极大的优先地位。保护用户信任当然是我们作为开发者的另一个巨大责任。以上提示是我们可以增强节点应用程序的一些方法，以使其安全运行并最大限度地降低安全风险。

编码快乐！💻

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)