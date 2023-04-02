# 反应本地—祝酒和活动指示器

> 原文：<https://javascript.plainenglish.io/react-native-toasts-and-activity-indicator-8053d5223e64?source=collection_archive---------19----------------------->

![](img/7c3d8f1e4d667caa3a0c0ebfd8cf050d.png)

Photo by [Pixzolo Photography](https://unsplash.com/@pixzolo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React Native 是基于 React 的移动开发，我们可以用它来进行移动开发。

在本文中，我们将看看如何使用它来创建一个带有 React Native 的应用程序。

# ToastAndroid

我们可以用`ToastAndroid`组件在我们的 Android 应用程序中显示一段祝酒词。

例如，我们可以写:

```
import React from 'react';
import { View, StyleSheet, ToastAndroid, Button } from "react-native";
import Constants from "expo-constants";const showToast = () => {
  ToastAndroid.show("Hello World", ToastAndroid.SHORT);
};const showToastWithGravity = () => {
  ToastAndroid.showWithGravity(
    "Hello World",
    ToastAndroid.SHORT,
    ToastAndroid.CENTER
  );
};const showToastWithGravityAndOffset = () => {
  ToastAndroid.showWithGravityAndOffset(
    "A wild toast appeared!",
    ToastAndroid.LONG,
    ToastAndroid.BOTTOM,
    25,
    50
  );
};export default function App() {
  return (
    <View style={styles.container}>
      <Button title="Toggle Toast" onPress={() => showToast()} />
      <Button
        title="Toggle Toast With Gravity"
        onPress={() => showToastWithGravity()}
      />
      <Button
        title="Toggle Toast With Gravity & Offset"
        onPress={() => showToastWithGravityAndOffset()}
      />
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: Constants.statusBarHeight,
    backgroundColor: "#ecf0f1",
    padding: 8
  },
});
```

我们调用`ToastAndroid.show`方法来显示一个简单的祝酒词。

`ToastAndroid.showWithGravity`表现出敬酒时的庄重。

`ToastAndroid.showWithGravity`显示重力和位置偏移的祝酒词。

此外，我们可以通过手动设置可见性状态来显示祝酒辞。

例如，我们可以写:

```
import React, { useEffect, useState } from 'react';
import { View, StyleSheet, ToastAndroid, Button } from "react-native";
import Constants from "expo-constants";const Toast = ({ visible, message }) => {
  if (visible) {
    ToastAndroid.showWithGravityAndOffset(
      message,
      ToastAndroid.LONG,
      ToastAndroid.BOTTOM,
      25,
      50
    );
    return null;
  }
  return null;
};export default function App() {
  const [visibleToast, setvisibleToast] = useState(false); useEffect(() => setvisibleToast(false), [visibleToast]); const handleButtonPress = () => {
    setvisibleToast(true);
  }; return (
    <View style={styles.container}>
      <Toast visible={visibleToast} message="Example" />
      <Button title="Toggle Toast" onPress={() => handleButtonPress()} />
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: Constants.statusBarHeight,
    backgroundColor: "#ecf0f1",
    padding: 8
  },
});
```

我们用`visible`道具创建了自己的`Toast`组件来控制 toast 的可见性。

同样，我们用`message`道具将消息传递到 toast 中。

当`visibleToast`状态改变时，我们首先用`useEffect`回调使其不可见，然后再使其可见。

# 活动指示器

我们可以用`ActivityIndicator`组件在我们的应用程序中添加一个活动指示器。

例如，我们可以写:

```
import React from 'react';
import { ActivityIndicator, StyleSheet, Text, View } from "react-native";
export default function App() {
  return (
    <View style={[styles.container, styles.horizontal]}>
      <ActivityIndicator />
      <ActivityIndicator size="large" />
      <ActivityIndicator size="small" color="green" />
      <ActivityIndicator size="large" color="blue" />
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center"
  },
  horizontal: {
    flexDirection: "row",
    justifyContent: "space-around",
    padding: 10
  }
});
```

我们添加了`ActivityIndicator`组件来显示它。

`size`道具控制尺寸，`color`改变颜色。

# 结论

我们可以添加一个活动指示器，用 React Native 祝酒。