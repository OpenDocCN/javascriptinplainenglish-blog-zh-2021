# 立即通过 Expo 开始开发您的 React 原生应用

> 原文：<https://javascript.plainenglish.io/getting-started-with-app-development-with-expo-ef8b81ac2491?source=collection_archive---------15----------------------->

手机 app 开发最简单的入门方式！

![](img/b47c0600c0b0c62e1af475eec0e2fe6b.png)

Photo by [Caspar Camille Rubin](https://unsplash.com/@casparrubin?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

应用程序开发是一个蓬勃发展的行业。许多公司雇佣开发人员为他们的商店开发应用程序，或者像麦当劳一样提供优惠券代码。许多公司通过利用跨平台工具(如 React Native 或 Flutter)的功能来实现这一产品。

[React Native](https://reactnative.dev/) 是一个用 JavaScript 构建的跨平台 app 开发库。它的工作原理是提供 React 组件，这些组件直接翻译成本地元素，比如文本、图像和 ScrollView。

因为 React 相当容易学习，我觉得 React Native 是创建一个在 iOS 和 Android 上都能工作的应用程序的最简单的方法。e [xpo](https://expo.io/) 提供了开发工具，如简单的应用程序签名，并提供了一个应用程序，您可以在开发过程中运行您的应用程序，以便您可以在任何设备上无线测试应用程序。

# 设置

React 本地开发人员支持使用 expo 设置新项目，这是开始应用程序开发的最简单方式。

如果您已经是一名 JavaScript 开发人员，您可能已经安装了 Node。Expo 在 Node.js 12 LTS 或更高版本上运行。你也可以用纱线来安装工具。

```
npm install -g expo-cli
# or 
yarn global add expo-cli
```

安装 expo 的 global CLI 工具后，您可以创建一个新项目，并从控制台启动它。

```
expo init AwesomeProject
cd AwesomeProject
npm start 
# You can also use: expo start
```

要在手机上运行该应用程序，您需要 expo 应用程序。它是一个应用程序，充当你的计算机和 React Native 之间的中间层。该应用程序可以在 Google Play 或苹果应用商店中找到。

# 运行您的应用

当您使用`npm start`或`expo start`运行应用程序时，您的电脑将打开浏览器，显示一些调试信息和一个二维码。可以在世博 app 上扫码打开自己的 app。Android 手机在 expo 应用程序中提供了一个 QR 扫描仪，iOS 设备可以使用相机应用程序扫描它。

当你第一次运行你的应用程序时，需要一段时间将应用程序安装到世博环境中。之后运行应用程序将花费更少的时间。

编辑项目时。您很可能会从编辑`App.js`文件开始。你可以添加一个`Text`组件，或者添加几个里面有东西的`View`组件。当你保存文件时，应用程序应该快速刷新。不过，在添加新文件时，你可能需要重启应用程序，这是快速刷新功能的常见情况。

# 结论

移动应用程序开发比以往任何时候都更容易，尤其是有了 expo。但是请注意，expo 可能会增加您构建的应用程序的文件大小。有很多方法可以减小文件的大小。但是对于学习构建应用程序来说，expo 要简单得多，它可以帮助你专注于代码，而不是构建应用程序的技术细节。

感谢您的阅读，祝您度过美好的一天。

*阅读更多来自 M. Vissers:*

[](/4-more-javascript-features-you-might-not-know-a49c91fd29b3) [## 4 个您可能不知道的 JavaScript 特性

### JavaScript 很好玩！

javascript.plainenglish.io](/4-more-javascript-features-you-might-not-know-a49c91fd29b3) [](https://medium.com/quick-programming/stop-using-react-for-small-projects-and-use-this-instead-93c3f1326d20) [## 停止对小项目使用 React，而使用这个

### React 就像一辆装甲车。做好一切准备，即使你不需要。

medium.com](https://medium.com/quick-programming/stop-using-react-for-small-projects-and-use-this-instead-93c3f1326d20) 

*更多内容尽在*[plain English . io](http://plainenglish.io/)