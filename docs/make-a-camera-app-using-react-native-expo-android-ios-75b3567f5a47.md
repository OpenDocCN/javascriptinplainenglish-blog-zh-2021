# 使用 React Native Expo 制作相机应用程序(Android 和 IOS)

> 原文：<https://javascript.plainenglish.io/make-a-camera-app-using-react-native-expo-android-ios-75b3567f5a47?source=collection_archive---------0----------------------->

## 使用 React 原生 Expo 应用程序拍照。

各位原生开发者好！

如今，几乎所有的社交媒体应用程序都有拍照功能，你可以点击并使用应用程序更新你的个人资料。不仅是社交媒体应用程序，所有电子商务和生产应用程序都有这个功能。那么，作为一个初学者，如何在你的应用程序中添加这样一个特性呢？如果您正在使用 React Native 构建这样一个应用程序，那么喝杯咖啡，让我们看看这些东西是如何工作的。

![](img/70ca25cf14e41b36f494c11ffb758d1d.png)

Photo by [Artem Maltsev](https://unsplash.com/@art_maltsev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您正在寻找视频教程，那么它就在这里:

# React 本地 Expo 应用程序的设置和安装

使用命令:Expo init***camera app***在您的首选目录中启动 expo-CLI 项目(您可以根据自己的选择命名)。选择空白模板并完成 javascript 依赖项的安装。之后，使用命令在父目录中安装以下软件包:

```
npm install expo-camera
```

expo-camera 具有内置功能，可帮助您使用移动设备点击照片。

我们已经完成了安装部分。让我们现在开始黑吧。

# React Native 中相机应用程序的代码(JavaScript)

**App.js**

```
import React, { useState, useEffect } from 'react';
import { StyleSheet ,Text, View, Button, Image} from 'react-native';
import { Camera } from 'expo-camera';
```

从各自的包中导入上述组件，因为我们将在我们的项目中使用它们。

```
const [hasCameraPermission, setHasCameraPermission] = useState(null);
const [camera, setCamera] = useState(null);
const [image, setImage] = useState(null);
const [type, setType] = useState(Camera.Constants.Type.back);useEffect(() => {
    (async () => {
      const cameraStatus = await Camera.requestPermissionsAsync();
      setHasCameraPermission(cameraStatus.status === 'granted');})();
  }, []);
```

我们请求用户允许我们使用摄像机。许可的初始状态被设置为空，但是当用户允许访问摄像机时，许可的状态将会改变。这就是为什么我们在这里使用 react-hook 的 useState。

我们的手机上有两种类型的摄像头，前置摄像头和后置摄像头。我们在它们之间切换，点击我们选择的图片。而相机之间的切换就是状态的变化。初始状态设置为“后”,但您可以将其更改为“前”,当您更改它时，状态会更改为“前”。这就是为什么我们在这里使用 type 作为钩子。同样的挂钩概念也适用于相机和图像。

useEffect 的数据异步存储在一个数组中。如果你删除了这个阵列，那么每次用户打开应用程序时，应用程序都会询问相机的许可，这有点烦人，也给用户带来了不好的体验。

```
const takePicture = async () => {
    if(camera){
        const data = await camera.takePictureAsync(null)
        setImage(data.uri);
    }
  }
 if (hasCameraPermission === false) {
    return <Text>No access to camera</Text>;
  }
```

这个箭头功能将允许您拍摄图片，并将图像的 URI 设置为 setImage hook。你也可以在这里控制台记录数据，它会给你 URI，高度，宽度，和图像的其他细节。

如果用户拒绝访问图库，屏幕上将出现“禁止访问摄像头”的文字。

```
<View style={{ flex: 1}}>
   <View style={styles.cameraContainer}>
       <Camera 
            ref={ref => setCamera(ref)}
            style={styles.fixedRatio} 
            type={type}
            ratio={'1:1'} />
    </View>
    <Button
            title="Flip Image"
            onPress={() => {
              setType(
                type === Camera.Constants.Type.back
                  ? Camera.Constants.Type.front
                  : Camera.Constants.Type.back
              );
            }}>
     </Button>
     <Button title="Take Picture" onPress={() => takePicture()} />
     {image && <Image source={{uri: image}} style={{flex:1}}/>}
</View>
```

现在将这些代码添加到 App 函数的返回片段中。这将给你一个在屏幕上观看该项目的体验。我将摄像机视角的比例设置为 1:1。您可以对其进行相应的定制。大多数人更喜欢 4:3 的观点。

因为我们主要关注这些东西的功能而不是样式。您可以相应地设计它们的样式。现在，在终端窗口中运行这个应用程序，并在您的设备上运行 expo 应用程序。点击一张你自己的照片，嘣..！！你在屏幕上看到自己。恭喜你，你使用 react native expo 成功构建了一个相机应用程序。

本文到此为止。如果你在某个地方丢失了，那么完整的代码在这里。

```
import React, { useState, useEffect } from 'react';
import { StyleSheet ,Text, View, Button, Image} from 'react-native';
import { Camera } from 'expo-camera';

export default function App() {
  const [hasCameraPermission, setHasCameraPermission] = useState(null);
  const [camera, setCamera] = useState(null);
  const [image, setImage] = useState(null);
  const [type, setType] = useState(Camera.Constants.Type.back);useEffect(() => {
    (async () => {
      const cameraStatus = await Camera.requestPermissionsAsync();
      setHasCameraPermission(cameraStatus.status === 'granted');})();
  }, []);const takePicture = async () => {
    if(camera){
        const data = await camera.takePictureAsync(null)
        setImage(data.uri);
    }
  } if (hasCameraPermission === false) {
    return <Text>No access to camera</Text>;
  }
  return (
   <View style={{ flex: 1}}>
      <View style={styles.cameraContainer}>
            <Camera 
            ref={ref => setCamera(ref)}
            style={styles.fixedRatio} 
            type={type}
            ratio={'1:1'} />
      </View>
      <Button
            title="Flip Image"
            onPress={() => {
              setType(
                type === Camera.Constants.Type.back
                  ? Camera.Constants.Type.front
                  : Camera.Constants.Type.back
              );
            }}>
        </Button>
       <Button title="Take Picture" onPress={() => takePicture()} />
        {image && <Image source={{uri: image}} style={{flex:1}}/>}
   </View>
  );
}const styles = StyleSheet.create({
  cameraContainer: {
      flex: 1,
      flexDirection: 'row'
  },
  fixedRatio:{
      flex: 1,
      aspectRatio: 1
  }
})
```

感谢阅读！如果这篇文章对你有帮助，你可以尽情鼓掌。

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*