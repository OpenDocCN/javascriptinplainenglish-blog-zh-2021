# 如何将我用 Vue.js 3 创建的项目部署到 Firebase？

> 原文：<https://javascript.plainenglish.io/how-can-i-deploy-my-project-created-with-vue-js-3-to-firebase-78ec84de6781?source=collection_archive---------7----------------------->

如果你有一个没有太多负担的项目，你不想向非免费托管系统付费(如果你刚刚开始使用 Vue.js 开发)，并且你没有购买域名，你还在等什么，这个方法适合你。

*如果你愿意，以后你可以添加自己的域名。*

![](img/02633a8ad7150071ee2c2633d91b67bb.png)

Photo by [Paulius Andriekus](https://unsplash.com/@paulando14?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我心中有一个小项目，我计划很快做。我不打算为这个项目支付一定的费用。由此，我进入了调查。有许多网站提供免费主机。但是众所周知，他们都有自己的品牌。我选择转向 Firebase 而不是他们。

Firebase 允许开发人员在一定程度上。它是免费的，我认为它在实时性方面非常有用。选择 Firebase 的最大因素之一是我没有将数据库结构构建得太复杂。因为是个人站点，数据传输-接收不会很多。它见效很快。域又回到了它的结构中。如果愿意，我们可以添加自己的域名。

如果你有一个小项目，想提升自己，我推荐用 Firebase。

**我将在项目中使用的技术**

*   Vue.js 3
*   重火力点

**我在项目中使用的 IDE**

*   [Visual Studio 代码](https://code.visualstudio.com/)

我在 GitHub 上创建了一个项目源代码库。我将与你分享你的链接作为一个来源。

我要说 Vue.js 3 是我最近用过的最漂亮的框架。

[](https://medium.com/geekculture/developing-at-devtools-and-hot-reload-fault-after-that-what-can-you-do-a3d24c5b4414) [## 在 DevTools 开发，热重装故障，之后能做什么？

### 点击 CTRL+S 后，坐下来几秒钟，哭着，打开 Devtools，重新开始编码同样的东西。

medium.com](https://medium.com/geekculture/developing-at-devtools-and-hot-reload-fault-after-that-what-can-you-do-a3d24c5b4414) [](/how-can-i-create-a-search-box-from-a-json-file-with-the-composition-api-c36058753c07) [## 如何用组合 API 从 JSON 文件创建一个搜索框

### 如何使用 Composition API 制作搜索框，如何从 JSON 文件中读取数据，如何在屏幕上显示数据…

javascript.plainenglish.io](/how-can-i-create-a-search-box-from-a-json-file-with-the-composition-api-c36058753c07) 

我们正在用 Vue.js 建立一个项目。

`vue create app-name`

我们手动安装项目，而不是默认安装。这部分我们会选择 Vue 3。

然后让我们调整 Firebase 设置。我们正在从 Firebase 控制台创建一个新项目。

![](img/428ffc551c89eac84382afba3940015c.png)

在这一部分，我们创建我们的 web 项目。我们可以将它添加到这一部分，因为我们将使用托管。可以以后再补充。

在下一步中

`npm install firebase`

`npm install -g firebase-tools`

如果给出不接受最后一行的错误，可以用`sudo`试试。(适用于 Mac 用户)

创建项目后，我们进入项目设置。在移动端使用 Firebase 的人都知道我们下载了一个 JSON 文件。我将使用网络配置。我们从 SDK 设置中选择配置。

![](img/53327c0e752373030c055144800609f6.png)

在这一部分之后，我们将把我们的应用程序连接到 Firebase。让我们打开 VS 代码。

让我们在 *src* 文件夹下创建一个 firebase 文件夹，并创建 *Config.js* 文件。让我们粘贴我们复制的`firebaseConfig`配置对象。

```
const firebaseConfig = { 
   apiKey: “AIzaSyC8kyNQ_nnpfEmSk5Ua9MUQzkItQPjP1FE”, 
   authDomain: “fir-vue-3-app.firebaseapp.com”, 
   projectId: “fir-vue-3-app”, 
   storageBucket: “fir-vue-3-app.appspot.com”, 
   messagingSenderId: “1062406189911”, 
   appId: “1:1062406189911:web:7f9841efd9e0a656ebc412”, 
   measurementId: “G-1GXFME5VEK”
};
```

在本文中，我将只展示 Firebase 集成和部署部分，保留项目的默认设置。

现在是时候为我们的 Vue 应用获得 *build* 了。得到 b *uild* 后，就会形成 ***dist*** 文件夹。我们将使用此文件夹进行部署。

`npm run build`

让我们从 Firebase 控制台转到托管选项卡并开始。

作为第一步，需要安装，我们已经这样做了。

然后他想让我们登录 Firebase。让我们用用户名和密码登录。

`firebase login`

`firebase init`

![](img/6c6be053d58e19439413928368de8bd8.png)

首先，它询问我们想要使用什么。我们现在只使用托管。

我们把后面的问题叫做“n”。

当购买构建时，我们已经更新了我们的索引文件。如果我们覆盖 Firebase init，我们为 UI 创建的索引将会改变，当我们部署项目时；

![](img/cd3ddac862eaa385edc32cfef6c59a0f.png)

我们会遇到这样的屏幕。首先，让我们小心不要做它。

通过这些步骤，我们已经将文件上传到 Firebase。现在是时候部署了。

`firebase deploy`

我们以非常简单的方式执行这个过程。

我将与您进一步分享这个项目的部署版本。你可以从那里检查它。

 [## firebase-vue-3-app

### 编辑描述

fir-vue-3-app.web.app](https://fir-vue-3-app.web.app/)  [## firebase-vue-3-app

### 编辑描述

fir-vue-3-app.firebaseapp.com](https://fir-vue-3-app.firebaseapp.com/) [](https://github.com/besteenurk/firebase-vue-3-app/tree/firebase-entegration) [## GitHub-besteenurk/firebase-vue-3-app at firebase-ente gration

### 通过在 GitHub 上创建一个帐户，为 besteenurk/firebase-vue-3-app 开发做出贡献。

github.com](https://github.com/besteenurk/firebase-vue-3-app/tree/firebase-entegration) [](/how-to-use-the-composition-api-to-get-data-from-service-with-vue-js-4da1eca19ad6) [## 如何使用组合 API 通过 Vue.js 从服务中获取数据

### 通过使用组合 API 而不是选项 API，可以使服务结构更加可用。

javascript.plainenglish.io](/how-to-use-the-composition-api-to-get-data-from-service-with-vue-js-4da1eca19ad6) [](https://bestte.medium.com/introduction-to-vue-js-fbe12ff58f86) [## Vue.js 简介

### 这里有一个答案，我该如何开始？

bestte.medium.com](https://bestte.medium.com/introduction-to-vue-js-fbe12ff58f86) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)