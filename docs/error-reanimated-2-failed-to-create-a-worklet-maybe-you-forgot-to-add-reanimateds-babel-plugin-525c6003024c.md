# 错误:Reanimated 2 未能创建一个 work let——可能你忘了添加 Reanimated 的 babel 插件？

> 原文：<https://javascript.plainenglish.io/error-reanimated-2-failed-to-create-a-worklet-maybe-you-forgot-to-add-reanimateds-babel-plugin-525c6003024c?source=collection_archive---------3----------------------->

## 解决方案是…

![](img/8ff506590d2e90f09cfe9a85d2f540ac.png)

Photo by [Richard Loader](https://unsplash.com/@fhfpix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你偶然犯了这个错误，不要烦恼。弹出到 babel.config.js，只需在`'module.exports'`中的**“插件”**下添加`'react-native-reanimated/plugin'`

## 解决方案:

在 **babel.config.js** 中，

```
module.exports = {
presets: ['module:metro-react-native-babel-preset'],
plugins: ['react-native-reanimated/plugin'],
};
```

(以上是重现错误和解决方案的基本示例。你的`babel.config.js`可能会不同。只要`'react-native-reanimated/plugin'`添加正确，重启开发服务器并运行`npx react-native start --reset-cache`后，错误应该会得到解决。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***

[](https://minidev.dev/blog/2022/06/18/easiest-way-to-remove-a-password-from-an-unlocked-pdf-in-mac/) [## 在 Mac 中从解锁的 PDF 中移除密码的最简单方法

### 而不需要安装任何密码移除软件。即使锁定的文件使您无法使用，它也能正常工作…

迷你开发](https://minidev.dev/blog/2022/06/18/easiest-way-to-remove-a-password-from-an-unlocked-pdf-in-mac/) [](https://forelsketaura.medium.com/subscribe) [## 每当 Aurora 发布时收到一封电子邮件。

### 每当 Aurora 发布时收到一封电子邮件。注册后，如果您还没有中型帐户，您将创建一个…

forelsketaura.medium.com](https://forelsketaura.medium.com/subscribe)