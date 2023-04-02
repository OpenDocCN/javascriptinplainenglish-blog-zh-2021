# 如何在 React 本地应用中处理网络连接

> 原文：<https://javascript.plainenglish.io/network-connection-in-your-react-native-app-4b12f0c212ea?source=collection_archive---------2----------------------->

![](img/39e64e73edaaf6d5cc4ad8e738a896bd.png)

您的应用程序可能需要不时检测用户的互联网连接。如果用户离线或没有像样的互联网连接，您可以在不同的路径上操作。在实践中，如果您的程序广播远程视频并需要强大的互联网连接，就会出现这种情况。如果用户无法访问互联网或可靠的连接，您可以专注于无缝地通知他们视频不能进行流式传输。这比抛出一个错误并让用户困惑要好。

react-native 社区报告中提供的[React Native Network Info](https://github.com/react-native-netinfo/react-native-netinfo)API 为我们提供了有关网络连接类型和质量的信息。

注意:React Native 预装的 NetInfo API 已被弃用。React Native 的官方文档建议我们使用 React Native Network Info API，我们将在这篇博客文章中介绍它。

让我们进入细节。

# 关键特征

React 本地网络信息 API 可用于了解用户应用的互联网连接。以下是该 API 的一些主要特性:

*   安卓、iOS、macOS、Windows 都支持。
*   获取有关网络连接当前状态的信息。
*   找出你现在的网络连接类型(wifi、蜂窝、蓝牙等。)
*   确定当前的蜂窝连接世代(3g、4g 等)。)
*   能够在超时的情况下执行网络可达性测试。

# 装置

设置和使用库很简单。

使用 yarn 将包添加到项目中。

```
yarn add @react-native-community/netinfo
```

如果您使用的是 React Native >= 0.60，就不需要费心手动链接库。

如果你在 iOS 上链接 CocoaPods，一定要使用下面的命令。

```
$ npx pod-install
```

在 Android 上修改 *android/build.gradle* 配置。

```
buildscript {
  ext {
    buildToolsVersion = "28.0.3"
    minSdkVersion = 16
    compileSdkVersion = 28
    targetSdkVersion = 28
    # Only using Android Support libraries
    supportLibVersion = "28.0.0"
    # If using Android X
    # Remove 'supportLibVersion' property and add specific versions for AndroidX libraries as 
    shown below
    # androidXCore = "1.0.2" 
    // Add other AndroidX dependencies
  }
```

关于安装的更多细节，请参考官方[文档](https://github.com/react-native-community/react-native-netinfo)。

# 使用

好了，现在你已经安装了 React Native Network Info 包，你已经准备好计算应用的互联网连接数据了。让我们来看看如何使用这个库。

首先，如下所示，从包中导入 NetInfo API:

```
import NetInfo from '@react-native-community/netinfo'
```

# useNetInfo 挂钩

在函数组件中使用 useNetInfo 挂钩是不使用事件处理程序获取网络信息的最简单方法。这是我们正在使用的网络信息库的一部分。

useNetInfo 钩子返回 NetInfoState 类型，在下面的例子中描述了网络的当前状态。

```
import {useNetInfo} from "@react-native-community/netinfo";

const MyComponent = () => {
  // returns a hook with the NetInfoState type.
  const netInfo = useNetInfo();
  return (
    <View>
      <Text>Type: {netInfo.type}</Text>
      <Text>Is Connected? {netInfo.isConnected.toString()}</Text>
    </View>
  );
};
```

# NetInfoState API

useNetInfo 钩子返回当前的网络状态给我们。让我们看看 NetInfoState API 支持的属性。

*   *type —* 返回当前连接(蜂窝、wifi、蓝牙等)的 NetInfoStateType。)
*   *isConnected —* 布尔值，表示是否有活动的网络连接(蜂窝、wifi、蓝牙等。)
*   *isInternetReachable —* 一个布尔值，确定是否可以使用当前连接访问互联网。
*   *isWifiEnabled* (仅限 Android 一个布尔值，指示 wifi 是否已启用。
*   *详细信息—* 根据网络连接的类型，这可以为我们提供有关连接的更多信息。连接的成本可以由多种因素决定。在这里，您可以了解更多有关 wifi 和蜂窝网络的信息。

通常，我们只需要知道互联网连接的类型，用户是否连接，以及在构建移动应用程序时他们的互联网是否可达。在某些情况下，您可能需要关于用户连接的更多信息，您可以使用这个库获得这些信息。让我们在上一个例子的基础上，从 netinfo 钩子中获取更多的信息。

```
import {useNetInfo} from "@react-native-community/netinfo";

const MyComponent = () => {
  // returns a hook with the NetInfoState type.
  const netInfo = useNetInfo();
  return (
    <View>
      <Text>Type: {netInfo.type}</Text>
      <Text>Is Connected? {netInfo.isConnected.toString()}</Text>
      <Text>Is Connection Expensive ? 
      {netInfo.isConnectionExpensive.toString()}</Text>
      { netInfo.type == "wifi" && 
        <>
        <Text>SSID: {netInfo.details.ssid}</Text>
        <Text>BSSID: {netInfo.details.bssid}</Text>
        </>
      }
    </View>
  );
};
```

# addEventListener()

如果从类组件获取 NetInfo，您需要添加事件侦听器来订阅用户网络连接的更新。useNetInfo 挂钩可用于获取功能组件中的当前网络连接。钩子留意幕后的信息。

让我们看一个例子，看看我们如何在组件中使用事件侦听器来获取网络连接信息。

```
let unsubscribe = null
componentDidMount() {
  // Subscribe
  unsubscribe = NetInfo.addEventListener(state => {
  console.log("Connection type", state.type);
  console.log("Is connected?", state.isConnected);
 });
}

componentWillUnmount() {
  // Unsubscribe
  if (unsubscribe != null) unsubscribe()
}
```

我们正在订阅前面代码片段中 componentDidMount()生命周期方法的任何更改。订阅后，听众将获得最新的网络信息。当连接状态发生变化时，将使用 NetInfoState 类型的参数调用回调。

# 获取()

fetch()方法可以用于只获取一次网络连接信息，而不必订阅组件中的任何更新。它返回一个带有 NetInfoState 类型的承诺作为结果。

```
NetInfo.fetch().then(state => {
  console.log("Connection type", state.type);
  console.log("Is connected?", state.isConnected);
});
```

# 配置()

您还可以使用 API 通过一组设置选项来设置库。您可以通过提供想要更改的值来调整默认值。如果你要使用这个函数，确保你的应用一启动就调用它。

如何使用 configure 方法的示例如下所示。

```
NetInfo.configure({
  reachabilityUrl: 'https://clients3.google.com/generate_204',
  reachabilityTest: async (response) => response.status === 204,
  reachabilityLongTimeout: 60 * 1000, // 60s
  reachabilityShortTimeout: 5 * 1000, // 5s
  reachabilityRequestTimeout: 15 * 1000, // 15s
});
```

# 结论

就这样了，伙计们。如果你想建立离线应用或依赖于网络连接数据的应用，请查看 [React Native Net Info](https://github.com/react-native-netinfo/react-native-netinfo) 。

如果你正在寻找一门课程，让你开始学习 React Native 并教授基础知识，请查看下面链接的 Mosh 课程。

[***终极反应原生课程—代码同 Mosh***](https://bit.ly/2UhGhS6)

我希望你喜欢这篇文章。更多文章再见。如果你喜欢这篇文章，别忘了分享给你的网络。

*更多内容请看*[***plain English . io***](http://plainenglish.io)