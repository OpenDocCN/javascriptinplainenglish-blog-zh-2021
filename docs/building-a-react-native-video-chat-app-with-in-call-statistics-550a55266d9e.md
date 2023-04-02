# 构建一个具有通话统计的 React 原生视频聊天应用程序

> 原文：<https://javascript.plainenglish.io/building-a-react-native-video-chat-app-with-in-call-statistics-550a55266d9e?source=collection_archive---------21----------------------->

![](img/3fd77d1288874247a85d2cea7509daf9.png)

当您构建实时互动应用程序时，需要监控大量指标，以便为最终用户提供流畅的体验。在调试次优用户体验、高 CPU 使用率、低互联网带宽、丢帧等等时，可能会面临许多挑战。通话统计可用于监控、维护和改善用户体验。

在本教程中，我们将在 React Native [快速入门应用](https://github.com/EkaanshArora/Agora-RN-Quickstart)中添加通话统计。如果你是 Agora SDK 的新手，你可以在这里学习演示如何工作。我们将了解如何访问和显示本地视频、远程视频和其他重要呼叫方面的统计数据，如带宽和 CPU 使用率。

# 先决条件

*   Node.js LTS 版本
*   安卓或 iOS 设备
*   一个 [Agora 开发者账户](https://sso.agora.io/en/signup?utm_source=medium&utm_medium=blog&utm_campaign=build-a-react-native-video-chat-app-with-in-call-statistics)
*   对 React Native 和 Agora SDK 的基本了解

快速启动应用程序是一个很好的起点，因为它已经内置了视频通话功能，并且不包含我们不需要的功能。您可以按照`readme.md`中的说明让应用程序在您的设备上运行。如果你只是想要有通话统计的最终应用，你可以在这里找到应用。

# 访问通话统计

![](img/c4ae4b9f8eec33fceb140ca5f28138d7.png)

让我们开始为我们的演示应用程序编写通话统计代码。

## 更新状态

我们将向状态添加三个对象(`remoteStats`、`rtcStats`和`localStats`)，以存储三种不同类型的统计数据。`localStats`和`rtcStats`将是直接包含不同属性的对象。我们将使用`remoteStats`对象将远程用户的 UID 存储为键，并将该用户的统计数据存储为键-值对中的值。我们将添加一个 Boolean `showStats`来隐藏和取消隐藏我们 UI 中的统计数据:

## 收听统计数据

我们可以通过监听`LocalVideoStats`、`RemoteVideoStats`和`RtcStats`事件来访问通话中的统计数据。让我们添加事件侦听器来访问和存储状态中的统计信息。每个事件每两秒触发一次。(如果我们有 *N* 个用户在通话中，`RemoteVideoStats`每 2 秒触发 *N* 次。)

## 切换 showStats 的函数

让我们创建一个当我们按下切换按钮时翻转 showStats 布尔值的函数:

# 显示统计数据

现在我们已经有了所有的逻辑，让我们在 UI 中显示这些统计数据。我们将使用 Boolean showStats 来有条件地呈现统计数据。

## 开关按钮

我们将在 render 方法中的 start 和 end call 按钮旁边添加一个按钮来隐藏和取消隐藏统计信息:

## 本地视频统计和 RTC 统计

我们将定义一个函数`_renderLocalStats`来使用平面列表呈现本地统计数据。我们遍历对象的键，并在文本组件中显示它们的值。(`_localStatItem`和`_rtcStatItem`是我们列表的辅助函数。)

我们将`_renderLocalStats`函数添加到`_renderVideos`函数中，如下所示:

## 远程视频统计

我们将创建一个函数，使用他们的`UID`来呈现给定远程用户的远程统计数据。我们将使用一个 FlatList 来呈现在我们的`remoteStats`对象上迭代的`Text`组件，并将它们的`UID`作为键:

我们将这个组件渲染成我们的`RtcRemoteView`组件的覆盖图。你可以在这里找到样式定义:

# 结论

这就是我们如何收听、监控和显示视频体验中的通话统计数据。您甚至可以构建函数来记录这些值的变化或对这些变化做出反应，从而提供出色的用户体验。

## 其他资源

如果你想了解演示应用程序是如何工作的，请看这个[教程](https://www.agora.io/en/blog/building-a-react-native-video-chat-app-using-agora/)。如果你想了解 Agora SDK 的其他特性，请参见 [API 参考](https://docs.agora.io/en/Video/API%20Reference/react_native/index.html)。我也邀请你加入 Agora [Slack 社区](https://www.agora.io/en/join-slack/)。

*更多内容看*[***plain English . io***](http://plainenglish.io)