# 如何用 Dotenv 保护环境变量

> 原文：<https://javascript.plainenglish.io/how-to-secure-environment-variables-with-dotenv-c534fe46c8a?source=collection_archive---------9----------------------->

## 使用 dotenv 保护环境变量的分步指南。

![](img/2006e100cf7b88f78fd92151879e9fdb.png)

Photo by [Possessed Photography](https://unsplash.com/@possessedphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在开发阶段，您可能需要在应用程序中使用环境变量或键。

将密钥与您的项目包含在一起可能是一种危险的尝试，因为有人可以访问您的密钥，并恶意地用它们做危险或违反规则的事情。

我们不希望这种情况发生在我们和我们的应用程序上。尤其是当你把代码提交给 GitHub 的时候，它会暴露在很多威胁之下，这在很多人眼里是显而易见的。

在本文中，我们将了解什么是 dotenv，以及我们如何利用它来保护我们的环境变量。

## **什么是 dotenv？**

[Dotenv](https://www.npmjs.com/package/dotenv) 是一个零依赖模块，将环境变量从**T5 env文件加载到**process . env**中。**

将配置存储在独立于代码的环境中是基于十二因素应用程序方法的。

Dotenv 使我们能够将我们的环境变量存储在一个单独的文件中，我们可以单独调用和使用它们。

另一方面，我们可以将这个文件添加到**中*。gitignore*** 文件，这样它就不会将该文件的内容提交给存储库。这意味着我们的环境变量对我们来说是唯一的，我们是唯一能够使用它们的人。

## **什么时候用 dotenv？**

Dotenv 可以用在你的开发阶段，你想存储一些独立的和私有的环境变量。

维护这一点是必要的，不要共享这些信息，主要是在为开源或其他项目做贡献的时候，在这些项目中，你想秘密地拥有你的私钥。

## **如何使用 dotenv？**

Dotenv 是一个超级轻量级的库，大小约为 25kb，这意味着它不会占用您很大的开发空间。在这一部分，我们将看看如何在我们的开发过程中使用 dotenv。

根据您喜欢的软件包管理器，您可以安装它，如下所示。

**NPM**

```
# with npmnpm install dotenv
```

**纱线**

```
# with Yarnyarn add dotenv
```

之后，我们将已经在我们的应用程序中安装了 dotenv，现在我们可以使用它了。

## **创建 dotenv 文件。**

最好在应用程序的根目录下，创建一个文件并将其命名为. env。该文件将包含我们所有的环境变量。

要创建我们的环境变量，您可以创建它们，如下所示。

在您的应用程序入口文件上，您可以如下所示导入它

因此，假设我们想要使用一个环境变量来连接我们的 mongo DB 数据库，我们可以如下使用它。

所以在任何我们需要环境变量的地方，我们只需要调用***process . env . db _ CONNECT***。

您可以将 ***DB_CONNECT*** 替换为您想要使用的 ***env*** 变量。

## 使用 dotenv 时的最佳实践

*   不要将字符串放在引号中，如下所示

DB_CONNECT = '您的 mongodburihere '

*   不要设置如下所示的环境变量。始终坚持使用等号。

DB_CONNECT:“您的 mongodburihere”

这就是我们如何在我们的应用程序中实现和使用 dotenv。

## **结论**

谢谢你一直关注这篇文章，如果你觉得它有帮助，如果你能和别人分享它，对我来说意义重大。

谢谢你，祝你写安全代码愉快。

## **更多阅读:**

[](/top-9-css-frameworks-to-check-out-for-your-next-project-ca0a57d69a58) [## 为你的下一个项目检查的前 9 个 CSS 框架

### 下一个前端项目的 CSS 框架。

javascript.plainenglish.io](/top-9-css-frameworks-to-check-out-for-your-next-project-ca0a57d69a58) [](/5-portfolio-tips-that-will-land-you-an-interview-aef81512328a) [## 让你获得面试机会的 5 个投资技巧

### 建立一个能让你脱颖而出的文件夹。

javascript.plainenglish.io](/5-portfolio-tips-that-will-land-you-an-interview-aef81512328a) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)