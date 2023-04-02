# 如何在 React Native 中下载文件

> 原文：<https://javascript.plainenglish.io/downloading-files-in-react-native-with-rnfetchblob-f78b18b46a36?source=collection_archive---------1----------------------->

## 在 React 本地应用程序中下载文件的简明易懂的指南。

![](img/bd467cd3e03977f5b0227e42175f784d.png)

Photo by [Christin Hume](https://unsplash.com/@christinhumephoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在之前的一篇文章中，我向您展示了如何将这个库添加到您的项目中，以及如何使用它将文件上传到远程服务器。将库添加到项目的步骤也可以在那里找到。(TLDR；`yarn add rn-fetch-blob`)。

现在，为了用 RNFetchBlob 下载文件，需要做一些额外的配置。

由于我们将使用 Android 下载管理器，我们必须将以下意图过滤器添加到`AndroidManifest.xml` (app):

```
<intent-filter>
  <action android:name="android.intent.action.DOWNLOAD_COMPLETE" /></intent-filter>
```

如果您还计划将下载限制到 wifi，那么您还需要清单文件中的以下权限:

```
<uses-permission      android:name="android.permission.ACCESS_NETWORK_STATE" />
```

让我们看看代码:

我现在要分解一下。

根据当前的平台，文件将被下载到安卓系统的`DownloadDir`和 iOS 系统的`DocumentDir`。我们使用选择器来选择正确的一个。

在代码片段中，GenericFile 只不过是一个接口，它有一些关于文件的基本信息(名称、扩展名等)。您需要知道扩展名，以便在设备上正确存储文件。否则，你会陷入手机下载的噩梦。pdf 和。无法正常打开的 png 文件，因为它们被视为二进制文件。

根据扩展，我们选择正确的 mimeType。我最初在配置中省略了`mime`字段。天啊，这么小的东西有多少无用的调试。

关于片段中确定`mimeType`的方式，有一点需要注意:这更像是一种概念验证的方式。在现实世界的应用程序中，你可能想要重构它。我将 3 个方法提取到一个`utils`文件中，每个方法返回一个布尔值:`isImage`、`isPdfFile`和`isVideoFile`。也许你也想支持音频文件。世界是你的！但是，您可能应该导出一些包含您支持的类型的列表，并检查文件的扩展名是否包含在适当的列表中。

确保良好用户体验的一个必须做的事情是在 Android 端将`useDownloadManager`设置为 true(第 46 行),并将其与设置为 true 的`notification`标志相结合。这样，用户将在通知面板中看到下载的文件。

[DownloadManager](https://developer.android.com/reference/android/app/DownloadManager) 将在后台妥善处理 Android 设备上的文件下载，考虑到重启设备或失去互联网连接等特殊情况。因此，通过使用这个系统服务，您可以确保用户最终能够成功下载他们通过您的应用程序请求的文件。

iOS 上的下载方式略有不同。如你所见，如果平台是 iOS，我们调用

```
RNFetchBlob.ios.openDocument(resp.data);
```

以便打开下载的 PDF、图像或视频，并向用户提供预览以及将文件下载到他们的设备或简单地观看它的可能性。

在 iOS 上下载文件的一个小提示:如果文件下载(这里是文件预览)操作是从底部的对话框开始的，确保在开始预览操作之前关闭对话框。根据经验，我可以告诉你，除非你这样做，否则预览不会起作用。

正确配置 RNFetchBlob 后，获取文件本身就是小菜一碟。如您所见，下载本身发生在以下代码段中:

```
RNFetchBlob.config(configOptions as RNFetchBlobConfig) 
  .fetch('GET', downloadUrl)     
  .then((resp) => {        
    console.log(resp);        
    signalSuccess();        
    if (isIOS) {          
        RNFetchBlob.ios.openDocument(resp.data);        
    }      
  })
  .catch((e) => {        
    // your error handling approach
  });
```

您的错误处理可能只是一个通知用户不幸事件的 snackbar。以同样的方式，您可能还想在下载确实成功的情况下显示一个 snackbar(谁不喜欢应用程序中的好消息呢？)

## 结论

暂时就这样了。非常感谢你的阅读，我希望这对你有所帮助！

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)