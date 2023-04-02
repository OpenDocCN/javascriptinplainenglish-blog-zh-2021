# 如何制作一个能吸引你的追随者的 Twitter 机器人

> 原文：<https://javascript.plainenglish.io/how-to-make-a-twitter-bot-that-will-get-you-followers-5971fdbff88c?source=collection_archive---------14----------------------->

## 制作一个能吸引你的观众的 Twitter 机器人。

![](img/df029f1e7e30c72f48a1aeaf909a557e.png)

Photo by [Claudio Schwarz](https://unsplash.com/@purzlbaum?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编写一个 Twitter 机器人是理解自动化好处的一个好方法。构建一个有吸引力的机器人是测试你编程技能的更好方法。

虽然构建一个与人互动的机器人将确保你在自己的领域获得一些惊人的追随者。

所有这些都可以在你做其他事情的时候由机器人来完成。这就是自动化的美妙之处。

在本教程中，我们将构建一个 Twitter 机器人，在一定时间后与您的观众互动并发出 Twitter 消息。

## **先决条件**

*   拥有一个 Twitter 开发者账户。
*   基本的 JavaScript 知识(对于我们的例子，我们将使用 JavaScript 来构建)。
*   安装 Node.js。

重要的事情先来。我们将安装一个全新的 express 应用程序。

## **创建我们的应用**

要创建我们的应用程序框架，您需要创建一个文件夹来存放我们所有的应用程序文件。在我们的例子中，它将是 ***僵尸*** 。

导航到文件夹的根目录并运行命令:

```
npm run init
```

该命令将指导您创建应用程序。或者类似地，您可以运行下面的命令跳过应用指南。

```
npm run init –yes
```

这是我的应用程序支架程序，如果你卡住了，你可以用它们来代替。

## **安装 Express**

根据您首选的软件包管理器，您可以使用以下命令安装 express:

**NPM**

```
npm install express — save
```

**纱线**

```
yarn add express
```

两者都可以用来在您的应用程序中安装 express。

创建一个文件并将其命名为 app.js。这将是我们的应用程序的入口点。现在让我们制作一个快速服务器。

现在，我们的应用程序可以服务于浏览器，并从浏览器控制台注销一些信息。

## **设置 Twit**

为了设置我们的应用程序，我们将使用一个名为 twit 的包。这个包将使我们能够与机器人无缝连接到我们的 ***Twitter 账户*** 并开始发送推文。

**安装 twit**

要安装 twit，使用下面显示的命令。

```
npm install twit
```

现在我们需要对应用程序进行编码，并生成最初的 tweet。

我们将制作推文，这样推文将被自动化。

在应用程序的根目录下，创建一个文件夹并将其命名为 tweets——在文件夹内创建一个文件并将其命名为 ***tweets.js*** 。

该文件将包含我们希望发送给观众的推文。

记住要发布与你的受众相关的推文。

现在我们可以将它导入到我们的应用程序中，如下所示。

为了确保您的环境变量不被其他人发现，您可以使用 dotenv 包来保护它们，如下所示。

## **安装 Dotenv**

```
npm i dotenv
```

现在我们的应用程序已经准备好发布 tweet 了。只需运行命令 ***npm start*** 即可运行 bot。

## **最后的想法。**

祝贺你完成并制作了你的推特机器人。

如果你觉得这篇文章很有帮助，并认为其他人*在*[*plain English . io*](http://plainenglish.io/)的更多内容可能会从中受益，如果你分享出来，对我来说意义重大。

## **更多内容:**

[](/how-to-double-your-productivity-as-a-software-developer-1431b69869b3) [## 作为软件开发人员，如何让你的生产力翻倍

### 根据这些建议，保持你的工作效率。

javascript.plainenglish.io](/how-to-double-your-productivity-as-a-software-developer-1431b69869b3) [](/how-to-deploy-your-nuxt-js-application-with-vercel-9501cc858c67) [## 如何用 Vercel 部署 Nuxt.js 应用程序

### 使用 Vercel 部署 Nuxt.js 应用程序的分步指南。

javascript.plainenglish.io](/how-to-deploy-your-nuxt-js-application-with-vercel-9501cc858c67) 

*更多内容看* [***说白了. io***](http://plainenglish.io/)