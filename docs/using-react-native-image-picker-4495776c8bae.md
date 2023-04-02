# 如何使用 React-Native-Image Picker

> 原文：<https://javascript.plainenglish.io/using-react-native-image-picker-4495776c8bae?source=collection_archive---------0----------------------->

## 如何从多媒体资料或照相机中选择媒体

![](img/9b0290eeb5e481453d1c6361466168dd.png)

Photo by [Lilly Rum](https://unsplash.com/@rumandraisin?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/camera?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

从图库或相机中挑选图像是使用 React native 开发应用程序的最流行和最基本的任务之一。我们如何做到这一点？

今天，我回来谈谈我们如何轻松地从您的设备库中选择图像或使用相机捕捉照片。我给你介绍一下`[React Native Image Picker](https://github.com/react-native-image-picker/react-native-image-picker)`。

在本文中，我将通过开发一个上传图片的应用程序来展示 React Native Image Picker。该应用程序将使我们能够选择和显示照片。

# 设置项目

在开始之前，我需要用下面几行代码创建一个新的 React 本地项目:

```
react-native init react_native_image_avatar_picker
cd react_native_image_avatar_picker
npm run ios
```

太棒了，我们已经成功创建了 React 本机应用程序。

现在，我将使用`[React Native Image Picker](https://github.com/react-native-image-picker/react-native-image-picker)`库来实现图像拾取器组件。这是一个 React 本机模块，允许您从设备库或相机中选择照片/视频。让我们用以下命令安装它:

```
yarn add react-native-image-picker
cd ios && pod install && cd ..
```

接下来，我们需要给我们的应用`Info.plist`添加 iOS 权限:

```
<key>NSPhotoLibraryUsageDescription</key>
<string>Your message to user when the photo library is accessed for the first time</string>
<key>NSCameraUsageDescription</key>
<string>The camera is accessed for the first time</string>
<key>NSMicrophoneUsageDescription</key>
<string>The microphone is accessed for the first time</string>
```

我们对 Android 不要求权限(`saveToPhotos`要求权限[检查](https://github.com/react-native-image-picker/react-native-image-picker#note-on-file-storage))。

之后，如果我们运行应用程序，一切正常，那么我们就可以开始编码了！

# 创建基础应用程序屏幕

基本想法是建立一个图像拾取器组件，允许用户从设备的库中上传新照片或通过相机拍摄照片。

首先，我们将使用新的绿色标题和背景更新一个基础应用程序屏幕。让我们创建一个`ImagePickerHeader`组件:

接下来，我将创建一个主`ImagePickerAvatar`组件，它允许您上传图像。

结果如下:

![](img/e96d625e41b24ea00b9ea227f057b5bd.png)

Main Image Avatar Picker Screen

# 从设备中挑选照片

在本教程中，我们将实现两个通过相机选择或捕捉照片的功能。我将使用一个可定制的动画模型，使用`[React Native Modal](https://github.com/react-native-modal/react-native-modal)`包向用户展示两个选项。为此，我们需要安装它:

```
yarn add react-native-modal
```

接下来，我将创建一个`ImagePickerModal`组件:

最后但同样重要的是，我们需要实现两个功能:

*   `onImageLibraryPress` —从库中选择图像
*   `onCameraPress` —使用相机拍照

现在，让我们更新我们的`App.js`文件:

# 让我们演示一下我们的图像拾取器应用程序

![](img/cee0ebcece0d21bd2f878d7464f27e75.png)

React-Native-Image-Avatar-Picker

如果你想检查所有代码，这里有 [Github](https://github.com/Gapur/react-native-image-avatar-picker) 的链接。

感谢阅读，希望这篇文章对你有用。编码快乐！

# 资源

[](https://github.com/react-native-image-picker/react-native-image-picker) [## 一个 react 本机模块，允许你…

### sunrise_over_mountains:一个 React 本机模块，允许您使用本机 UI 从设备库中选择媒体…

github.com](https://github.com/react-native-image-picker/react-native-image-picker) [](https://github.com/react-native-modal/react-native-modal) [## GitHub-React-native-Modal/React-native-Modal:一个增强的、动画的、可定制的 React…

### React Native 的增强的、动画的、可定制的模型。-GitHub-react-native-modal/react-native-modal:An…

github.com](https://github.com/react-native-modal/react-native-modal) [](https://github.com/Gapur/react-native-image-avatar-picker) [## GitHub-Gapur/React-Native-Image-avatar-Picker:使用 React-Native-Image-Picker

### 使用 React-Native-Image-Picker 为 Gapur/react-native-image-avatar-picker 开发做出贡献，创建一个…

github.com](https://github.com/Gapur/react-native-image-avatar-picker) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)