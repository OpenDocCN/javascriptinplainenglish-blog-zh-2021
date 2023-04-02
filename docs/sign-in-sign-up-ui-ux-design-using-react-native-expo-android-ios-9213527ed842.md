# 登录-注册用户界面-使用 React Native Expo 进行 UX 设计(Android 和 IOS)

> 原文：<https://javascript.plainenglish.io/sign-in-sign-up-ui-ux-design-using-react-native-expo-android-ios-9213527ed842?source=collection_archive---------3----------------------->

## 使用 JavaScript 代码构建一个高度设计的登录注册 UI-UX 设计

你好，德夫斯！

好吧，这会很快的。设计是编程的一个重要部分，因为它改善了用户体验，使应用程序变得动态和用户友好。让我们开始设计一个登录和注册页面，因为几乎每个移动应用程序都需要它。如果你是一名 UI 开发人员，那么你必须在你的编程生涯中处理它。

![](img/b455a7cc4179dcda297b0f55428388cb.png)

Login-Signup UI-UX Desing in React Native

我们项目的结果看起来和上面的图片一样。

如果您正在寻找基于视频的教程，那么它就在这里:

**第一部分:**

第 2 部分(注册屏幕):

# 设置和安装

我们使用最新的 [React navigation 6](https://reactnavigation.org/docs/getting-started) 在屏幕和 [NativeBase](https://nativebase.io/) 组件之间切换来制作 UI。要使用它，我们必须进行一些安装。所以，让我们安装它。确保您已经安装了高于或等于 41 的 expo 版本。

## 为了导航

*   `**npm install** [**@react**](http://twitter.com/react)**-navigation/native**`
*   `**npm install react-native-screens react-native-safe-area-context**`
*   `**npm install** [**@react**](http://twitter.com/react)**-navigation/stack react-native-gesture-handler**`

## 对于 NativeBase

*   `**npm install native-base styled-components styled-system**`
*   `**expo install react-native-svg**`
*   `**expo install react-native-safe-area-context**`

## **用于图标**

*   `**npm install** [**@expo/vector-icons**](http://twitter.com/expo/vector-icons)`

这是一个很长的安装列表，但是我们必须安装它们，因为我们要在我们的应用程序中使用它们。

# 代码部分

**App.js**

我们在这里添加两个屏幕，一个是 login，另一个是 stack navigator 中的 signup。

**Login.js 和 Signup.js**

两个屏幕的 UI 都是由 NativeBase 组件构成的。我们在密码部分添加了安全文本输入功能。并添加了一个使用脸书、谷歌、Twitter 或 Apple ID 登录的框(之前称为 card)。

**Github 代码链接:** [**登录-注册设计**](https://github.com/imrohit007/Login-UI-UX-React-Native)

感谢阅读。确保点击评论框，如果你正面临这个项目的任何问题。如果这篇文章有帮助，请与您的社区分享。

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯***](http://newsletter.plainenglish.io/) ***。*** *在我们的* [***社区获得独家写作机会和建议***](https://discord.gg/GtDtUAvyhW) ***。****