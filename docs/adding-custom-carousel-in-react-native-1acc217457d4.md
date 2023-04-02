# 如何在 React Native 中添加自定义轮播

> 原文：<https://javascript.plainenglish.io/adding-custom-carousel-in-react-native-1acc217457d4?source=collection_archive---------18----------------------->

在 React Native 中创建自定义轮播的 3 个步骤

![](img/bc2116bbac7f8b35bbe29a133c5797cf.png)

Photo by [Tyler Lastovich](https://unsplash.com/@lastly?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 在后台

故事开始于我为我的一个客户在一个 react-native 项目中创建一个 carousel。我已经创建了一个关于如何在 react-native 中创建 carousel 的故事，但是在今天的故事中，我们将开发自定义的 carousel 组件。

[](/developing-carousel-in-react-native-fffaaead021f) [## 在 React Native 中开发轮播

### 列出了在 React Native 中开发 carousel 的多种方法。

javascript.plainenglish.io](/developing-carousel-in-react-native-fffaaead021f) 

## 入门指南

我们将使用的库是 react-native-swipe-gesture 来添加手势，如左右滑动功能。我正在使用一个 [**现成的例子**](https://github.com/shreyvijayvargiya/iHateReadingLogs/tree/main/TechLogsMobile/React%20Native%20Paper%20Boilerplate) ，你也可以使用。

```
yarn add react-native-gesture-handler
```

一旦 repos 被克隆，包被安装，我们需要为我们的欢迎屏幕转盘的数据。考虑到我们的项目是一个与食品相关的项目，你可以选择你想要的数据和你想要的任何数据。

## 创建自定义轮播组件

在根目录中，创建一个单独的文件夹名称作为组件。这个组件文件夹由可重用的代码组成，或者让我们称之为应用程序的有机体。

```
import React from 'react';
import { View, Text} from 'react-native';const Welcome = () => {
  return (
    <View>
      <Text>Welcome Screen</Text>
    </View>
  );
};export default Welcome;
```

## 刷卡逻辑

最终产品将有 3 个像传送带布局对齐的图像。用户可以左右滑动，并可以查看活动图像或幻灯片。以下是相同的逻辑—

*   前三个图像将从对象数组中呈现
*   添加左右滑动手势以更改当前幻灯片
*   我们将显示活动指示器和非活动指示器

```
const stages = [
 { id: 0,
   src: require("../assets/vegetables.jpeg")
 },
 {
   id: 1,
   src: require("../assets/vegetables.jpeg")
 },
 {
   id: 2,
   src: require("../assets/breakfast.jpeg")
 }
];
```

这将是图像数据，使用这些数据，我们将只渲染活动图像。

```
const [ active, setActive ] = useState({
 id: 0,
 src: stages[0].src
});
```

使用阶段数据，我们正在设置转盘的活动图像。

## 添加推送手势

下一部分是添加滑动手势。如果用户向左滑动，我们将从活动幻灯片向后滑动，如果用户向右滑动，我们必须从活动幻灯片向前移动一张幻灯片。

在下面添加滑动逻辑

我还添加了返回上一张幻灯片的逻辑，即从第一张幻灯片向右滑动，反之亦然。

## 渲染指示器

这也很简单，一旦我们获得了活动状态，我们只需向用户显示活动指示器。

## 最终产品

这是产品的最终外观。

## 结论

这就是今天的故事，你真的需要 3 个步骤，安装软件包，编写逻辑和执行接口中的组件来开发定制的转盘。

代码可从以下链接获得。

```
[**click to read the code repository**](https://github.com/shreyvijayvargiya/iHateReadingLogs/tree/main/TechLogsMobile/React%20Native%20Custom%20Carousel) 
```

直到，下一次，有一个美好的一天，人们。

```
For more such stories visit our website - 💻 [**iHateReading**](/www.ihatereading.in)
```

## 更多阅读

[](https://medium.com/geekculture/3-steps-to-use-react-native-elements-in-react-native-70012baf76e0) [## 在 React Native 中使用 React Native 元素的 3 个步骤

### 测试 React Native 的另一个 UI 库😁，3 个简单的步骤，准备好基本 MVP

medium.com](https://medium.com/geekculture/3-steps-to-use-react-native-elements-in-react-native-70012baf76e0) [](/4-steps-for-navigations-in-react-native-c0e6304a2d09) [## 通过 4 个简单的步骤对本地导航做出反应

### 在 React 本机应用程序中添加导航

javascript.plainenglish.io](/4-steps-for-navigations-in-react-native-c0e6304a2d09) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)