# 如何在 Quasar 中为网络和电子应用程序创建 QR 码扫描仪

> 原文：<https://javascript.plainenglish.io/how-to-create-a-qr-code-scanner-for-web-and-electron-app-in-quasar-fdbc3787bf06?source=collection_archive---------6----------------------->

![](img/408592d9065b42b2821eb3a3fd1989d6.png)

我们都知道，Quasar 是一个建立在 Vue.js 之上的伟大的库，我最喜欢 Quasar 的一点是，它可以轻松地为 Android、iOS、Windows、Linux 等不同环境创建应用程序或网站。

今天，我将向您展示如何在 Quasar 中轻松创建二维码扫描仪。如果你想在 Vue.js 中构建一个 QR 扫描仪，这个教程也是有用的。

## 要求

*   [vue-qrcode-reade](https://www.npmjs.com/package/vue-qrcode-reader) r

1.  从创建一个类星体项目开始。

```
quasar create appname
```

2.现在我们将安装 vue-QR 码阅读器到我们的 quasar 项目中。

```
npm install vue-qrcode-reader#or yarn add vue-qrcode-reader
```

3.现在从 **pages** 目录打开你的 **Index.vue** 文件，用下面的代码替换整个代码。

4.现在运行你的应用程序`quasar dev`，在浏览器上打开`[http://localhost:8080](http://localhost:8080)`。它会要求您的浏览器摄像头许可，以允许摄像头打开。现在将二维码放在摄像头前，检测到二维码后，它会在最后一个**结果文本**旁边显示结果。

5.按照您的要求修改和设计应用程序后，您现在需要运行下面的命令来生成 SPA 的构建。

```
quasar build
```

6.在创建了 **SPA** 构建之后，现在您可以运行下面的命令来为 windows 环境创建电子应用程序。

```
quasar build -m electron
```

如需更多文档，您可以访问此链接:[https://gruhn . github . io/vue-QR code-reader/API/QR code stream . html](https://gruhn.github.io/vue-qrcode-reader/api/QrcodeStream.html)

所以你可以看到在类星体中创建一个 QR 扫描仪是多么简单。下面我分享了 GitHub 的资源库，供参考。

[](https://github.com/Medium-Quasar/medium-qrscanner) [## 中等类星体/中等 QR 扫描仪

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/Medium-Quasar/medium-qrscanner) 

*更多内容看* [***说白了. io***](http://plainenglish.io/)