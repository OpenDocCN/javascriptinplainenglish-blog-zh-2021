# 使用 React Native Expo 的二维码和条形码阅读器应用程序

> 原文：<https://javascript.plainenglish.io/qr-code-and-barcode-reader-app-using-react-native-expo-856ce6ce1df4?source=collection_archive---------1----------------------->

## React 本地世博会项目

![](img/772528d9c40e9eaced54af6fa1a4ecfb.png)

QR code and Bar code Scanner in React Native

当你浏览 Google play 商店时，你可以看到有许多应用程序只是为了读取二维码和条形码。众所周知，二维码或条形码有一些隐藏的信息。你只需要一个完美的工具来破解这些信息。

现在，我们准备做这样一个 app。你可以把它作为你的主流应用程序，在 play store 上发布，可以是很酷的风格，也可以是一个附带项目。这是我从一个自由职业项目中得到的。喝杯咖啡，让我们开始吧。

这个项目的视频教程在这里:

# 设置和安装

*   初始化项目

```
expo init ReaderApp
```

*   选择空白的 javascript 模板并安装所有的 javascript 依赖项
*   移动到父目录。安装所需的软件包

```
npm install expo-barcode-scanner
```

*   完成的

# 二维码代码(React Native Expo)

**Scanner.js**

*   导入所需的包

```
import React, { useState, useEffect } from 'react';
import { Text, View, StyleSheet, Button } from 'react-native';
import { BarCodeScanner } from 'expo-barcode-scanner';
```

*   现在在扫描仪函数内部。

```
const [hasPermission, setHasPermission] = useState(null);
const [scanned, setScanned] = useState(false);useEffect(() => {
    (async () => {
      const { status } = await BarCodeScanner.requestPermissionsAsync();
      setHasPermission(status === 'granted');
    })();
  }, []);const handleBarCodeScanned = ({ type, data }) => {
    setScanned(true);
    alert(`Bar code with type ${type} and data ${data} has been scanned!`);
  };if (hasPermission === null) {
    return <Text>Requesting for camera permission</Text>;
}
if (hasPermission === false) {
    return <Text>No access to camera</Text>;
}
```

我们从一些反应钩子开始。我在这里使用了两个 react 钩子。第一个用于摄像头访问，另一个用于扫描。相机权限的初始状态为 null，因为我们希望用户允许它。当用户允许照相机许可时，空状态将把他们的状态从空改变为许可授予状态。这个新状态将存储在“setHasPermission”中。

我们还使用了 useEffect 钩子。您可以在这个钩子中添加一个空数组，因为它是第二个参数。这告诉 React 你的效果不依赖于道具或状态的任何值，所以它永远不需要重新运行。

接下来，我们使用一个箭头函数来处理扫描仪。当我们扫描二维码或条形码时，我们需要类型和数据作为信息。所以，相应地补充说。

*   视角

```
return (
    <View style={styles.container}>
      <BarCodeScanner
        onBarCodeScanned={scanned ? undefined : handleBarCodeScanned}
        style={StyleSheet.absoluteFillObject}
      />
      {scanned && <Button title={'Tap to Scan Again'} onPress={() => setScanned(false)} />}
    </View>
  );
```

返回扫描仪函数，并相应地设置它们的样式。这是二维码阅读器的简单原始代码。您可以相应地运行它们。

我添加了 react-navigation 6，让它变得更加动态。我用了 stack navigator。正如您在特征图像中看到的。

**你可以在这里** **拥有完整的 GitHub 代码访问** [**。**](https://github.com/imrohit007/Qr-code-reader-react-native-expo-)

# 条形码扫描仪支持的格式(IOS 和 Android)

根据官方文档，这些是支持的格式:

```
qr
upc_e
pdf417
interleaved2of5
ean8
ean13
datamatrix
code39mod43
code128
code93
code39
codabar
aztec
```

感谢您的阅读。如果这篇文章听起来信息量很大，那就鼓掌直到你的手流血，并与你的社区分享。

你好，我叫 Rohit Kumar Thakur。我对自由职业者持开放态度。我构建了 **react 原生项目**，目前正在开发 **Python Django** 。随时联系我(**freelance.rohit7@gmail.com**)