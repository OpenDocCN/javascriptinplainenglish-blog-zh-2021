# 如何在 React Native 中创建基于令牌的身份验证

> 原文：<https://javascript.plainenglish.io/how-to-use-token-based-authentication-in-react-native-c5739b9d5e45?source=collection_archive---------0----------------------->

想知道如何在 React Native 中处理身份验证吗？本文解释了一些最佳实践以及如何实现基于令牌的身份验证。

![](img/1677219d505af7bbdb04fc654606f0df.png)

Photo by [Micah Williams](https://unsplash.com/@mr_williams_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

那么什么是基于令牌的认证呢？在高层次上，这种策略只验证访问者凭证一次，作为回报，向访问者提供一个令牌。该令牌将允许他们在预定义的时间段内访问。当用户注销时，令牌失效。它相当于一张票，允许用户在你的系统中读写某些信息。

让我们开始吧，首先我们要创建一个新的 React 原生项目。

## 创建新的 React 本机项目

要创建新的 React 本机项目，请运行

```
npx react-native init ReactNativeAuth
```

接下来，让我们清除根目录中的 App.js 文件，并用下面的代码替换它。这将为我们实现身份验证提供一个全新的平台。

让我们通过运行以下命令来运行这个应用程序

```
npx react-native run-ios # or run-android
```

它当前应该显示如下内容

![](img/55b756907add893c5a3b6269fd96d8a2.png)

Hi!

## 计划建造什么

现在，让我们从用户的角度来描述我们希望我们的身份验证如何工作。

*   用户首次下载应用程序
*   用户将创建一个帐户
*   用户现在可以使用该应用程序了
*   当应用程序被杀死，无论什么原因，我们将恢复会话，如果可能的话
*   当令牌过期时，它应该会自动刷新令牌

## 编写身份验证容器

为此，我们需要几样东西。我们需要安全地将令牌保存到用户的手机上，一些文章会告诉你在 React Native 中使用类似 AsyncStorage 的东西。但是，这是不安全的，令牌可能会从内存中取出，因为它保存在原始文本中。这可以用来模拟用户。

首先，我们将安装[https://github . com/emerald Santo/react-native-encrypted-storage](https://github.com/emeraldsanto/react-native-encrypted-storage)，这基本上使用 Android 的 EncryptedSharedPreferences 和 iOS 的 Keychain 来存储敏感数据。

```
npm install react-native-encrypted-storage
```

然后对于 iOS，运行

```
npx pod-install
```

现在，我将使用一个模拟 API 来伪造一个注册端点供应用程序使用。它目前位于以下网址[https://run . mocky . io/v3/DD 598227-c275-48e 8-9840-c 588293 EAD 84](https://run.mocky.io/v3/dd598227-c275-48e8-9840-c588293ead84)。

首先，您可以使用 HTTP 客户端测试端点，或者将这个 curl 命令复制到您的终端。

```
curl -d '{"username":"jonaskuiler"}' \-H "Content-Type: application/json" \"https://run.mocky.io/v3/dd598227-c275-48e8-9840-c588293ead84"
```

基本上，它唯一应该做的就是返回这个响应

```
{"access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvbmFzIEt1aWxlciIsImlhdCI6MTUxNjIzOTAyMn0.jm6f8xMR0aroqQ_YtGPHQbvdp88FKBQZWOUR5m6R_MA"}
```

为了在 React 本机应用程序中使用这个端点，我们将编写一个小容器来处理应用程序中任何与身份验证相关的状态。

请将此代码粘贴到项目根目录下的 Auth.js 名称下。此代码的作用是封装对注册端点的请求，使用 React Context API 将 Auth 上下文传递给应用程序的任何深层嵌套子级，以供以后使用。另外，它将一个对象传递给一个 render prop，这样我们就可以确定用户是否通过了身份验证。这样，我们可以将用户路由到特定的视图。让我们修改 App.js 来实现这个路由。

现在，让我们看看这是怎么回事。这定义了两个视图，注册，当用户未通过身份验证时显示，当用户通过身份验证时显示。当您单击 register 按钮时，它将调用 Auth.js 中定义的 Register 方法，并向我前面提到的模拟端点发出请求。当该请求成功时，它将变为已验证状态。

接下来，当用户出于某种原因关闭应用程序时，我们需要保存从恢复会话的请求中获得的令牌。

我们之前安装了[react-native-encrypted-storage](https://github.com/emeraldsanto/react-native-encrypted-storage)，现在让我们通过对 Auth.js 做一些修改来使用它。

这在 React Native 中拼凑了一个基于令牌的身份验证。当应用程序第一次呈现时，它将通过向服务器发送令牌来获取当前用户。这将返回一些关于用户的信息并恢复会话。

你可以通过刷新应用程序来测试这种行为，在 iPhone 模拟器中，使用 CMD+D 热键，然后按“重新加载”。

就这些了，感谢阅读。我目前正在写一篇文章，介绍如何使用 PIN 和生物识别技术用密码锁定你的应用程序。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)