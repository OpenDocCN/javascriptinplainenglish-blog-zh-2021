# React Native —维度和 Web 视图

> 原文：<https://javascript.plainenglish.io/react-native-dimensions-and-web-views-19dd25da2f5f?source=collection_archive---------10----------------------->

![](img/bafbd96305ef54f2aea156021df56af7.png)

Photo by [Aditya Chinchure](https://unsplash.com/@adityachinchure?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React Native 是基于 React 的移动开发，我们可以用它来进行移动开发。

在本文中，我们将看看如何使用它来创建一个带有 React Native 的应用程序。

# 规模

我们可以使用`Dimensions`对象来获取窗口的尺寸。

例如，我们可以写:

```
import React, { useEffect, useState } from 'react';
import { View, StyleSheet, Text, Dimensions } from "react-native";const window = Dimensions.get("window");
const screen = Dimensions.get("screen");export default function App() {
  const [dimensions, setDimensions] = useState({ window, screen }); const onChange = ({ window, screen }) => {
    setDimensions({ window, screen });
  }; useEffect(() => {
    Dimensions.addEventListener("change", onChange);
    return () => {
      Dimensions.removeEventListener("change", onChange);
    };
  }); return (
    <View style={styles.container}>
      <Text>{`Window Dimensions: height - ${dimensions.window.height}, width - ${dimensions.window.width}`}</Text>
      <Text>{`Screen Dimensions: height - ${dimensions.screen.height}, width - ${dimensions.screen.width}`}</Text>
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center"
  }
});
```

我们通过监听`change`事件来获得窗口和屏幕的尺寸。

我们使用`Dimensions.addEventListener`为事件添加一个监听器。

我们使用带有不同参数的`Dimensions.get`方法来获得窗口和屏幕尺寸。

# 键盘回避视图

我们可以使用`KeyboardAvoidingView`组件来添加一个容器，当关键字出现时，它就会离开关键字。

例如，我们可以写:

```
import React from 'react';
import { View, KeyboardAvoidingView, TextInput, StyleSheet, Text, Platform, TouchableWithoutFeedback, Button, Keyboard } from 'react-native';export default function App() {
  return (
    <KeyboardAvoidingView
      behavior={Platform.OS == "ios" ? "padding" : "height"}
      style={styles.container}
    >
      <TouchableWithoutFeedback onPress={Keyboard.dismiss}>
        <View style={styles.inner}>
          <Text style={styles.header}>Header</Text>
          <TextInput placeholder="Username" style={styles.textInput} />
          <View style={styles.btnContainer}>
            <Button title="Submit" onPress={() => null} />
          </View>
        </View>
      </TouchableWithoutFeedback>
    </KeyboardAvoidingView>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  inner: {
    padding: 24,
    flex: 1,
    justifyContent: "space-around"
  },
  header: {
    fontSize: 36,
    marginBottom: 48
  },
  textInput: {
    height: 40,
    borderColor: "black",
    borderBottomWidth: 1,
    marginBottom: 36
  },
  btnContainer: {
    backgroundColor: "white",
    marginTop: 12
  }
});
```

我们添加了带有`onPress`支柱的`TouchableWithoutFeedback`组件的`KeyboardAvoidingView`。

我们将`Keyboard.dismiss`方法传递给它，让我们将键盘从屏幕上移除。

现在，当我们点击`TextInput`时，键盘会显示出来，视图会缩小以适应键盘。

# 链接

我们调用`Linking.openURL`方法来打开一个带有我们想要的 URL 的 web 视图。

例如，我们可以写:

```
import React from 'react';
import { View, StyleSheet, Text, Linking } from 'react-native';export default function App() {
  const handlePress = () => {
    Linking.openURL('https://google.com');
  }; return (
    <View
      style={styles.container}
    >
      <Text onPress={handlePress}>Google</Text>
    </View>
  );
}const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```

添加一段文字，当我们点击它的时候，它就会出现在谷歌上。

# 结论

我们可以用 React Native 得到窗口和屏幕的尺寸。

此外，我们可以使用`Linking.openURL`方法打开 web 视图来加载网页。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**