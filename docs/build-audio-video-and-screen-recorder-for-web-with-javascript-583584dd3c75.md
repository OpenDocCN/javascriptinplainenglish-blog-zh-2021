# 用 JavaScript 构建一个视频、音频+屏幕录制的 Web 应用程序

> 原文：<https://javascript.plainenglish.io/build-audio-video-and-screen-recorder-for-web-with-javascript-583584dd3c75?source=collection_archive---------0----------------------->

![](img/18d45edb66a1bf2be2289193b9dd9304.png)

Photo by [Surface](https://unsplash.com/@surface?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这个疫情，发生了很多变化，因此工作文化中有一些我们无法摆脱的东西，是的*“远程会议”*。在其中一次会议上，我对[会议平台](https://meet.google.com)产生了好奇，经过一番搜索，我了解到我们的浏览器能够做什么(内置浏览器 API)。

因此，我计划开发一个简单的记录器，支持音频、视频和屏幕记录，可从[http://recorder . dhruv 479 . dev](https://recorder.dhruv479.dev)获得

如果你喜欢这篇文章，不要错过鼓掌和关注。

要继续学习，您应该熟悉一些术语:

**MediaRecorder:**[media stream API](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream_Recording_API)的 media recorder 接口提供了轻松录制媒体 [*ref: MDN*](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder) 的功能

**media devices:**media devices 接口提供对连接的媒体输入设备(如照相机和麦克风)的访问，以及屏幕共享 [*ref: MDN*](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices)

好了，准备好了吗？让我们添加一些代码！

**记录处理程序:**首先，我们将编写一个函数来获取`stream`和`mimeType`，收集数据块，然后允许从浏览器下载本地机器上的文件。

handle-stream-record.js

首先，用输入流创建一个`MediaRecorder`实例。然后，为`ondataavailable`(当数据进入数据流时)和`onstop`(当数据流停止时)添加事件。

在 chunk 可用之后，它被推入数组，在 stop 事件之后，所有的 chunk 被放在一起形成一个指定 mimeType 的`[Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)`。

稍后，为 blob 对象创建 URL，并且可以从浏览器下载。

**音频记录器:**接下来，我们将编写一个函数来调用音频记录，该函数进一步调用带有所需参数的`handleRecord`。

audio-stream-record.js

这里，我们将使用`mediaDevices.getUserMedia`来访问用户机器上的资源。调用这个之后，我们会在浏览器中得到一个请求许可的提示，确认之后，我们就可以访问那些资源了。此外，我们可以向约束传递额外的参数，比如减少声音回声的`audio: { echoCancellation: true }`。

**录像机:**与录音类似，我们需要在 *getUserMedia* 函数的参数中添加`video`。

video-stream-record.js

在`getUserMedia`中添加`video`约束后，你会得到一个额外的相机许可提示，确认后，你猜怎么着，我们可以访问相机流了。另外，额外的参数可以传递到`video`，例如:`video: { width: {min: 640}, height: {min: 480}}`

**屏幕记录器:**这是最有趣的，因为显示流由`getDisplayMedia`提供，音频由`getUserMedia`提供。因此，如果需要屏幕记录的音频背景，我们需要在这里合并不同的流。

screen-stream-record.js

我们合并不同的流来创建一个新的流，并将其传递给`handleRecord`函数。这里，我们也可以根据需要添加更具体的约束。

*传递给捕获媒体的约束可以更具体，如分辨率、回声、光标，而不是真/假。*

# 结论

瞧，JavaScript 部分完成了😁。我们只需要添加一些基本的 HTML 来调用这些功能，停止记录，当然，下载文件。

以下是完整代码的参考:

[](https://github.com/dhruv479/recorder/blob/master/index.html) [## DH ruv 479/记录器

### 在 GitHub 上创建一个帐户，为 DH ruv 479/记录器的开发做出贡献。

github.com](https://github.com/dhruv479/recorder/blob/master/index.html) 

希望你喜欢这篇文章，鼓掌并关注更多内容。