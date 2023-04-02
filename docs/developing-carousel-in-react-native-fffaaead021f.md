# 在 React Native 中开发轮播

> 原文：<https://javascript.plainenglish.io/developing-carousel-in-react-native-fffaaead021f?source=collection_archive---------4----------------------->

列出了在 React Native 中开发 carousel 的多种方法。

![](img/82dd0da0d3c5b75428aeed5b151eb7c5.png)

[Design creative](http://ihatereading.in)

# 在后台

Carousel 是每个 web 应用程序中最常用的组件之一。我想做一个旋转木马。所以我决定开发一个 carousel 作为 React 本机应用程序。

# 概观

您可以使用 [read-to-start-example](https://github.com/shreyvijayvargiya/iHateReadingLogs/tree/main/TechLogsMobile/MapsInReactNative) 资源库。一旦 expo 安装完成，您只需要包含图像和文本的样本数据来显示在 carousel 中。您可以依赖的 API 是带有以下链接的 API。

```
[https://picsum.photos/v2/list](https://picsum.photos/v2/list)
```

# 入门指南

有多种方法可以创建你自己的旋转木马—

1.  [**ScrollView**](https://reactnative.dev/docs/scrollview) —这是 React Native 的内置组件，提供垂直和水平方向的滚动。所以，要在水平方向添加一个旋转木马，可以简单地添加这个道具。
2.  [**Flatlist**](https://reactnative.dev/docs/flatlist) —这是 React Native 的另一个高性能内置组件，用于滚动内容。这也支持水平和垂直方向的滚动功能。我已经写了一篇关于如何使用 FlatList 的文章，链接在描述中。
3.  [**React Native Carousel**](https://www.npmjs.com/package/react-native-carousel)—提供 Carousel 组件 HOC 的第三方库。您只需要将这个 HOC 包装到子组件或者您想要添加到 carousel 的内容中。
4.  [**React Native Swiper flat list**](http://react-native-swiper-flatlist)**——**又一个周下载量超过 6K 的第三方库。这个库的好处是他们依赖 FlatList 为我们的 carousel 提供滚动功能，这使得它比 **ScrollView 更具性能。这个库也提供了自动播放和分页属性，这使得一切变得如此简单。**
5.  [**React Native Snap Carousel**](https://www.npmjs.com/package/react-native-snap-carousel)—这是 React Native 应用中开发 Carousel 使用最多、最广泛的 npm 包。它的周下载量超过 10 万次。他们有许多真实世界的例子，如演示、类型脚本支持和易于实现的 carousel。如果您将为任何专业用例开发一个 carousel，那么强烈推荐使用这个库。
6.  [**React Native Swiper**](https://www.npmjs.com/package/react-native-swiper)—React-Native 的 Swiper 组件。顾名思义，它为您包装的组件提供了滑动功能。使用 react native snap carousel 为 carousel 添加滑动功能使用 react native swiper 很容易实现。
7.  [**React Native Gallery Swiper**](http://react-native-gallery-swiper)—React Native 组件，通过平移手势、触摸和滑动功能实现图像库。一个高性能的库，支持大列表，大图片，手势控制，易于定制。

# 结论

如果您正在处理一个专业领域，并且想要一个快速简单的高性能转盘，那么您应该选择一个带有 react-native-swiper 的 react-native-snap-转盘。这种组合易于实施，并能提供最高效的性能。

但如果你是初学者或处于学习阶段，那么你应该尝试我建议的 7 个选项中的至少 3/4，因为这将有助于提高你的理解。

```
Until, next time. Have a good day, People.
```

[](https://medium.com/nerd-for-tech/flatlist-is-still-underrated-796130a8b8f2) [## Flatlist 仍然被低估了

### 也许你使用 Flatlist 的方式是错误的，这里有一些提示和技巧

medium.com](https://medium.com/nerd-for-tech/flatlist-is-still-underrated-796130a8b8f2) [](/stop-wasting-your-time-on-developing-that-to-do-list-application-88a4bc513e0a) [## 停止浪费你的时间为你的投资组合开发一个待办事项列表应用程序

### 时间就是金钱。不要浪费时间去开发一个待办事项应用程序，让你的投资组合脱颖而出。

javascript.plainenglish.io](/stop-wasting-your-time-on-developing-that-to-do-list-application-88a4bc513e0a) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)