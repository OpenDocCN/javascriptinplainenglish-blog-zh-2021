# 如何在 React Native 中进行标签导航

> 原文：<https://javascript.plainenglish.io/how-to-make-tab-navigation-in-react-native-a1850155781f?source=collection_archive---------10----------------------->

## *堆栈导航很酷，但是标签导航更酷。*

![](img/64de235a2e84cf3f3c87a822f352732e.png)

Photo by [Kari Shea](https://unsplash.com/@karishea?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/iphone?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 动机

创建应用程序是一个很好的方式来度过现在世界各地的封锁期。你甚至可以利用广告或 IAPs 赚点外快。但是首先你需要学习一些基础知识。

其中一个基础就是导航。有两种主要的导航方式。

*   堆栈导航
*   标签导航

还有混合导航或那些不遵循任何规则的导航，但现在这并不重要。

堆栈导航是线性的。你点击一个按钮，进入下一个屏幕。下一个。接下来…如果你想回去，你需要回去三次才能回家。

选项卡导航在底部有“选项卡”。通常伴有图标或文本。你可以在 Apple Music 应用程序、Instagram 和更多地方看到这一点。

所以让我们开始吧。

# 安装和设置

我不会使用 Expo 来创建我的 React 应用程序，但是你仍然可以使用它，反正代码都是一样的。我将假设所有的 Android / iOS SDK 都已安装。

让我们通过在控制台/终端中运行一些命令，在我们选择的 IDE 中创建一个新的应用程序。

```
npx react-native init reactNativeNav
```

这将创建我们的裸应用程序文件。让我们也安装[反应导航](https://reactnavigation.org/docs/getting-started/)和底部标签包。*确保您在正确的文件夹中。*

```
npm install @react-navigation/nativenpm install @react-navigation/bottom-tabsnpm install react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context [@react](http://twitter.com/react)-native-community/masked-view
```

让我们通过在您的仿真器/设备上运行它来测试它是否能运行。

```
npx react-native run-android
```

首次运行可能需要一段时间(2-10 分钟),具体取决于您的系统。

# 创建页面

接下来，让我们创建一些基本页面。

首先我们清空`App.js`。

接下来，我们创建一个`/pages/`目录，我们将在其中创建三个页面:

*   `Home.js`
*   `NotHome.js`
*   `List.js`

这些名称只是占位符，可以是任何名称。现在，我所有的页面都将采用相同的格式:

如果您将`PageName`更新为页面的实际名称，您可以看到您当前正在查看的页面。我的所有三个页面都有相同的代码和更新的文本字符串。

如果你重新加载你的应用程序，你将看不到任何东西。因为我们需要在我们的`App.js`中添加选项卡导航。

让我们在`App.js`中添加选项卡导航的导入。

```
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
```

接下来，我们需要添加选项卡导航对象。

```
const Tab = createBottomTabNavigator();
```

让我们更新`App.js`中的 JSX 代码，以包含到选项卡的路由。

我们完整的`App.js`文件现在看起来像这样:

如果您运行这段代码，您将在屏幕底部看到一些简单的选项卡，如果您单击这些选项卡，屏幕将切换到下一个选项卡。

# 核标准情报中心

恭喜您，您已经在应用中添加了选项卡！但是如果没有任何图标，它们看起来会很无聊，所以让我们添加一些图标。

React 导航的文档使用矢量图标，但是由于本教程将会更加简洁，所以我将使用文本字符串作为图标，比如‘H’、‘L’和‘N’。

我们需要使用`screenOptions`属性将这些信息添加到我们的 Navigator 对象中。我们将我们的`<Tab.Navigator>`开始标记更新为:

我们添加了`screenOptions`，在其中我们为每条路线设置了图标。你可以使用任何你喜欢的组件！我们只是碰巧使用了`Text`组件。

我们还添加了`tabBarOptions`来设置图标和标签栏文本的活跃和不活跃的颜色。如您所料，这些也可以是十六进制值。

在本教程的最后，我们的完整的`App.js`看起来像这样。

干得好！

我们的选项卡导航现在已经完成。

# 下一步是什么？

现在你可以通过跟随[文档](https://reactnavigation.org/docs/tab-based-navigation)来尝试组合堆栈和标签导航。您可以尝试不同的道具来根据自己的喜好设计 tabbar。

我希望你学到了新的东西，祝你今天过得愉快。