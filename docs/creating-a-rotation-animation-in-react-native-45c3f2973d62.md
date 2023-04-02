# 如何在 React Native 中创建旋转动画

> 原文：<https://javascript.plainenglish.io/creating-a-rotation-animation-in-react-native-45c3f2973d62?source=collection_archive---------1----------------------->

## 使用挂钩

> 这篇文章最初发表在我的博客@ [isaks.io](https://isaks.io/blog/2021-03-17/creating-a-rotation-animation-in-react-native/)

在本教程中，我将向您展示如何创建一个按钮，当它被按下时旋转 720 度。我们将使用 [React 本地动画](https://reactnative.dev/docs/animated)动画系统来创建旋转动画。

![](img/106bee7ae4fb75ee3685e6536f6daad0.png)

Photo by [Kinson Leung](https://unsplash.com/@filmprint?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 创建组件

首先，我们创建功能组件`ButtonWithSpin`，它有一个`TouchableOpacity`组件，里面有一些文本。

注意，文本是使用`Animated.Text`组件创建的。这是因为将要旋转的文本必须是*可动画化的*。如果您正在旋转其他东西，那么您也可以使用这些组件中的任何一个:

*   **动画。图片**
*   **动画。滚动视图**
*   **动画。查看**
*   **动画。正文**
*   **动画。平面列表**
*   **动画。章节列表**

我们还使用`useState`钩子来存储我们的`rotateAnimation`值。这是动画库中的一个*动画值*。我们使用`new Animated.Value(0)`来初始化该值。

## handleAnimation 函数

`Animated.timing()`使用[缓动功能](https://reactnative.dev/docs/easing)使一个值随时间变化。默认情况下，它使用`easeInOut`曲线，这是我们正在做的完美。我们传递我们的`rotateAnimation`值和一个配置值，其中我们将持续时间设置为 800 毫秒。动画是通过调用`start()`开始的，我们包含了一个回调函数来重置动画。

## 插入

`interpolate()`方法将输入范围映射到输出范围。将 0–1 范围转换为 0–100 范围的基本映射是:

```
value.interpolate({
  inputRange: [0, 1],
  outputRange: [0, 100]
});
```

您也可以使用`interpolate()`方法来映射字符串。由于我们希望将文本从 0 度旋转到 720 度，我们的代码将如下所示:

我们还创建了`animatedStyle`对象，它包含了一个数组`transform`和我们刚刚创建的旋转值`interpolateRotating`。

## 把所有东西放在一起

将`animtedStyle`对象添加到`Animated.Text`组件，将`width`添加到`TouchableOpacity`组件，我们就完成了！

这是最终产品的样子:

![](img/284c151a0042a300771f59261b62cc40.png)

Button spinning after click

代码是:

现在我们有了。我希望你已经发现这是有用的。这是我在 Medium 上的第一篇帖子，因此非常感谢任何反馈！