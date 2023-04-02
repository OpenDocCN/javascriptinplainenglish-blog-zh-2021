# 本地反应—警报和动画

> 原文：<https://javascript.plainenglish.io/react-native-alert-and-animations-63945b3dcb09?source=collection_archive---------9----------------------->

![](img/3699d9da13a5576a366324a605e60357.png)

Photo by [Syed Ahmad](https://unsplash.com/@syedabsarahmad?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React Native 是基于 React 的移动开发，我们可以用它来进行移动开发。

在本文中，我们将看看如何使用它来创建一个带有 React Native 的应用程序。

# 警报

我们可以用`Alert.alert`方法添加警告。

例如，我们可以写:

```
import React from 'react';
import { View, StyleSheet, Button, Alert } from "react-native";const createTwoButtonAlert = () =>
  Alert.alert(
    "Alert Title",
    "My Alert Msg",
    [
      {
        text: "Cancel",
        onPress: () => console.log("Cancel Pressed"),
        style: "cancel"
      },
      { text: "OK", onPress: () => console.log("OK Pressed") }
    ],
    { cancelable: false }
  );const createThreeButtonAlert = () =>
  Alert.alert(
    "Alert Title",
    "My Alert Msg",
    [
      {
        text: "Ask me later",
        onPress: () => console.log("Ask me later pressed")
      },
      {
        text: "Cancel",
        onPress: () => console.log("Cancel Pressed"),
        style: "cancel"
      },
      { text: "OK", onPress: () => console.log("OK Pressed") }
    ],
    { cancelable: false }
  );export default function App() {
  return (
    <View style={styles.container}>
      <Button title="2-Button Alert" onPress={createTwoButtonAlert} />
      <Button title="3-Button Alert" onPress={createThreeButtonAlert} />
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center"
  },
});
```

我们用警报标题、警报消息和一组对象调用`Alert.alert`方法来呈现按钮。

`text`属性有按钮文本。

`onPress`是我们按下按钮时运行的功能。

`style`有按钮的样式名。

`cancelable`设置是否可以取消按钮按下。

# 愉快的

`Animated`库让我们可以流畅、轻松地构建动画。

例如，我们可以写:

```
import React, { useRef } from 'react';
import { Animated, Text, View, StyleSheet, Button } from "react-native";export default function App() {
  const fadeAnim = useRef(new Animated.Value(0)).current;
  const fadeIn = () => {
    Animated.timing(fadeAnim, {
      toValue: 1,
      duration: 5000
    }).start();
  }; const fadeOut = () => {
    Animated.timing(fadeAnim, {
      toValue: 0,
      duration: 5000
    }).start();
  }; return (
    <View style={styles.container}>
      <Animated.View
        style={[
          styles.fadingContainer,
          {
            opacity: fadeAnim
          }
        ]}
      >
        <Text style={styles.fadingText}>Fading View!</Text>
      </Animated.View>
      <View style={styles.buttonRow}>
        <Button title="Fade In" onPress={fadeIn} />
        <Button title="Fade Out" onPress={fadeOut} />
      </View>
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  fadingContainer: {
    paddingVertical: 8,
    paddingHorizontal: 16,
    backgroundColor: "lightblue"
  },
  fadingText: {
    fontSize: 28,
    textAlign: "center",
    margin: 10
  },
  buttonRow: {
    flexDirection: "row",
    marginVertical: 16
  }
});
```

我们调用`Animate.timing`方法来显示我们的动画。

第一个参数是我们想要显示的动画的 ref。

然后我们使用`fadeAnim`对象作为`Animated.View`组件中`opacity`属性的值。

无论`Animated.View`里面是什么都是动画。

其他显示动画的方法包括`Animated.decay`创建一个以初始速度开始并逐渐减速至停止的动画。

`Animated.spring`为我们提供了 spring 物理模型动画。

他们采用与`Animation.timing`相同的论点。

我们还可以创作动画。

`Animated.delay`延迟播放动画。

`Animated.parallel`同时启动多个动画。

`Animated.sequence`按顺序启动动画。

`Animated.stagger`按顺序启动动画，并与连续延迟并行。

# 组合动画值

我们可以用以下方法组合两个动画值:

*   `Animated.add()`
*   `Animated.subtract()`
*   `Animated.divide()`
*   `Animated.modulo()`
*   `Animated.multiply()`

我们可以通过编写以下内容来创作动画:

```
import React, { useRef } from 'react';
import { Animated, Text, View, StyleSheet, Button } from "react-native";export default function App() {
  const fadeAnim = useRef(new Animated.Value(0)).current;
  const fadeIn = () => {
    Animated.sequence([
      Animated.delay(3000),
      Animated.timing(fadeAnim, {
        toValue: 1,
        duration: 5000,
        useNativeDriver: true
      })
    ]).start()
  }; const fadeOut = () => {
    Animated.timing(fadeAnim, {
      toValue: 0,
      duration: 5000,
      useNativeDriver: true
    }).start();
  }; return (
    <View style={styles.container}>
      <Animated.View
        style={[
          styles.fadingContainer,
          {
            opacity: fadeAnim
          }
        ]}
      >
        <Text style={styles.fadingText}>Fading View!</Text>
      </Animated.View>
      <View style={styles.buttonRow}>
        <Button title="Fade In" onPress={fadeIn} />
        <Button title="Fade Out" onPress={fadeOut} />
      </View>
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center"
  },
  fadingContainer: {
    paddingVertical: 8,
    paddingHorizontal: 16,
    backgroundColor: "lightblue"
  },
  fadingText: {
    fontSize: 28,
    textAlign: "center",
    margin: 10
  },
  buttonRow: {
    flexDirection: "row",
    marginVertical: 16
  }
});
```

在`fadeIn`函数中，我们用 3000 毫秒调用了`Animated.sequence`方法。

然后我们调用`Animated.timing`来运行我们的淡入动画。

# 结论

我们可以用 React Native 显示警报和动画。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**