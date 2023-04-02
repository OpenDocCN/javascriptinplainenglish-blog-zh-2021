# Web 开发人员在使用 React Native 之前应该知道的事情

> 原文：<https://javascript.plainenglish.io/building-with-react-native-23139cf4959?source=collection_archive---------12----------------------->

![](img/38b2d940d14ad31e38ba36d20f16316e.png)

Image credits to [Daria Shevtsova](https://www.pexels.com/photo/bokeh-photography-of-person-holding-turned-on-iphone-1440727/) at Pexels

Web 开发是我对软件工程的最初介绍。然而，在我成为一名更好的工程师的过程中，我挑战自己去学习更多关于前端开发的知识。这意味着理解客户端和服务器端渲染之间的差异，建立一个包含 UX 趋势的网站，并将 React Hooks 整合到我的项目中。

关于这一点，我最近使用 React Native 构建了一个项目，React 是 React 的一个扩展。React Native 是一个开源框架，用于移动前端开发。在我看来，如果你有 React 的坚实基础，那么 React Native 不会有太多的学习曲线。也就是说，有一些关键的差异，这是我在构建时亲身经历的。让我们深入研究一下。

## 入门指南

我面临的第一个挑战是测试。在 web 开发中，我习惯于使用多个屏幕来查看我的代码是如何在浏览器上呈现的。我还经常使用浏览器内的 Chrome 开发工具来设计和记录任何错误。在 React Native 上非常不同——主要是因为你必须在你的移动设备上测试。

在这里，我将链接 [React 本地文档](https://reactnative.dev/)——我发现它们非常有用，并使用 Expo CLI 启动和测试我的项目。Expo 是一个很好的解决方案，因为测试你的项目的替代方案是使用 Android 模拟器。一旦你在本地机器上安装并设置了 Expo，并在你的手机上下载了 Expo 应用程序，只要这两个设备都连接到同一个 WiFi，你就可以看到你的作品了！

## 好了，我已经开始了。还有什么？

我看到的下一个大的不同是对本地事件的反应。在 React 中，对于一般的 web 开发来说，您有一些基于用户如何与 web 交互的给定事件。例如，当你点击网络上的某个东西时，它可能会把你带到一个新的页面，或者在 YouTube 上播放某个东西。如果将鼠标悬停在某个项目上，您可能会看到动画。

这在移动设备上复制起来有点困难(这也是我的观点)。在您的移动设备上，您通常会在手机上按下或滑动:按下以查看某些内容，将商品添加到购物车，滑动以查看设置，等等。事实上，在 React 中，您可以传入 event 或`e`作为事件侦听器的参数。你**不能**在 React Native 里这么做。相反，您有诸如 onChangeText 之类的事件侦听器，它为您处理更新文本(或字符串)。

## 式样

React Native 附带了许多专用于移动开发的标签。这包括`<View>`、 `<Text>`、`<TextInput>`和`<Image>`，它们取代了传统的 HTML 标签。除了预先确定的组件之外，您还必须将一个样式表导入到您想要样式化的组件中。react Native**不**允许 CSS。

## 其他考虑

除此之外，开发一个手机 app 还要考虑很多因素。对我来说，这包括调整键盘。或许，你和我一样，认为在手机上输入东西后键盘会自动消失是理所当然的。开发我的应用让我开始考虑用户交互:我想让键盘消失吗？我希望一个组件如何相对于键盘出现？

React Native 是一个流行的移动开发框架。使用和构建它很快，如果你理解 React 或其他前端框架，它相对容易掌握。也就是说，当涉及到移动开发时，有太多的东西需要学习和考虑。

## 资源

[](https://reactnative.dev/) [## 反应本地学习一次，写在任何地方

### React Native 将本机开发的最佳部分与 React 相结合，React 是用于构建…

反应性发展](https://reactnative.dev/) [](https://medium.com/@thinkwik/react-native-what-is-it-and-why-is-it-used-b132c3581df) [## React Native:是什么？还有，为什么要用？

### 说手机是每个人的半个灵魂并没有错，说到安卓…

medium.com](https://medium.com/@thinkwik/react-native-what-is-it-and-why-is-it-used-b132c3581df) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)