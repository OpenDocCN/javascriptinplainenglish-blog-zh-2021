# 在 JavaScript 中使用环境变量

> 原文：<https://javascript.plainenglish.io/introduction-to-dotenv-f2bdf93e4a1?source=collection_archive---------11----------------------->

## Dotenv 简介

![](img/9c738dd407587b4f68daa068f80dbf6c.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/locked-files?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

如果您以前使用过任何 API，如 Google Firebase、Twitter API、脸书 API 或任何其他需要某种身份验证的 API，您就会知道保证密钥安全是非常重要的。因为有了这些密钥，有人可能会删除你的数据库或发送你不想发送的推文。

这就是为什么要开发`[dotenv](https://www.npmjs.com/package/dotenv)`文件的原因。至少，这是其中的一个用例。它们本质上是一个文件，你可以在开发者之间共享，但不会推送到包含这些重要私钥的 GitHub repo。

# 注意

此时，也就是 2021 年，你可能正在使用 NextJS、GatsbyJS、Create-React-App 等框架。这些有时有他们自己的使用环境变量的方法，不需要 dotenv。所以一定要检查你选择的框架的文档，看看使用 dotenv 是否是最好的选择。

大多数框架的环境变量的工作方式与 dotenv 非常相似，所以这篇文章对那些开发人员仍然有用。

# 安装 DotEnv

安装 DotEnv 就像 1，2，3 一样简单。有了 NPM 或纱，你可以像你期望的那样简单地安装它。

```
npm install dotenv
```

这比建立一个完整的框架要容易得多。让我们看看 Dotenv 文件在我们的应用程序中是如何工作的！

# 使用 DotEnv

我将不会使用任何 API 键来展示 Dotenv 文件的功能，而是在控制台中记录来自`.env`的值。

`.env`文件的一个原则是它们只应该是本地的。生产服务器应该需要与本地机器不同的密钥，除非绝对必要，否则**永远不要**将自己的`.env`文件提交给版本控制。

一个`.env`文件应该包含用于任何类型开发的本地键。从 API 键到简单的`debug`标志。

要使用 DotEnv 文件，我们需要在项目的根目录下创建一个文件，文件扩展名为`.env`。为此，我将创建`process.env`。

```
PRIVATE_KEY=abc
PUBLIC_KEY=xyz
```

但是你将如何使用这个文件呢？或者至少是文件中的键。为此，我们需要导入并配置 dotenv 包。

```
require('dotenv').config()
```

您应该在应用程序中尽早这样做。越早越好。如果您选择预加载密钥，则不必导入包。但稍后会详细介绍。

现在你应该可以在任何需要的地方使用这些钥匙了。

另外请注意，环境变量不应该被推送到 GitHub 或其他版本控制。它们应该包含您个人开发应用程序所需的密钥。

# 预加载

[当使用`import`代替`require`时，预加载](http://$ node -r dotenv/config your_script.js)是导入变量的首选方式。您可以使用节点的`require`命令行选项来预载 dotenv。

```
$ node -r dotenv/config your_script.js
```

您可以在[dot NV](https://www.npmjs.com/package/dotenv)的 NPM 页面上了解更多信息。

# 结论

对任何开发人员来说，使用环境变量都是一件重要的事情。保持私钥的私密性对于保持安全性和将密钥远离那些可能不需要它们的人很有用。

你不会把开发数据库 API 的钥匙给现在在前端工作的实习生吧？

无论如何，非常感谢你的阅读，祝你有一个美好的一天。