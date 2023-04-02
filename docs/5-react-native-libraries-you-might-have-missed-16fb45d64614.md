# 5 个您可能错过的反应原生库

> 原文：<https://javascript.plainenglish.io/5-react-native-libraries-you-might-have-missed-16fb45d64614?source=collection_archive---------3----------------------->

![](img/63d08673aee9448ee396c1011a842383.png)

Photo by [CHUTTERSNAP](https://unsplash.com/@chuttersnap?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为 reactor Native 开发者，我认为我们都熟悉 reactor-Native 社区中的那些基本库，以及其他一些开创性的库，如 React Navigation 和 Reanimated。

事实上，也有较小的贡献者那里和他们的工作值得一提。我想分享我发现的 5 个非凡的库，希望它们能对你的项目有用。

# 1.gor hom/底层

这是迄今为止我尝试过的最好的底稿库。它将[重新激活表单](https://github.com/osdnk/react-native-reanimated-bottom-sheet)中的无缝动画和手势以及[反应原生滚动表单](https://github.com/rgommezz/react-native-scroll-bottom-sheet)中的可滚动功能组合到一个类似原生的性能库中。

底部表是通过门户安装的，该门户引用了在 web 开发中创建覆盖内容的通用实践。该概念类似于 React Portals。

它还可以与 React Navigation 集成，后者模仿 iOS 本机模式堆栈行为。这种设置只是用一张底纸包裹一个堆栈导航器。不需要自定义导航器。这在实现模式堆栈时提供了更多的创造性自由。

![](img/acd02547934fbbdd414e695ad5120127.png)

Demo video from the documentation

不利的一面是恼人的键盘避免视图问题。它有一些不完善的黑客攻击，所有者希望在需要 Reanimated v2 的 v3 中解决这个问题。如果你不打算在你的资产负债表中包含任何输入字段，那你无异于在公园里散步。

[](https://github.com/gorhom/react-native-bottom-sheet) [## gor hom/reaction-native-bottom-sheet

### 具有完全可配置选项的高性能交互式底稿🚀 🌟模式演示视图，底稿…

github.com](https://github.com/gorhom/react-native-bottom-sheet) 

# 2.反应-本地-通知程序

这个库让我想起了 Instagram 的应用内通知。我喜欢整洁的设计，更不用说与手势处理程序的集成了。它也是完全可定制的。

还有一种队列模式，您可以排列多个通知并通过它们进行转换。

您实际上可以模仿本机推送通知。每个人都应该觉得用户体验熟悉而直观。

[](https://github.com/seniv/react-native-notifier) [## seniv/reaction-native-通知程序

### 快速而简单的应用内通知反应原生这个库使用反应原生手势处理程序，一个完美的库…

github.com](https://github.com/seniv/react-native-notifier) 

# 3.反应-原生-呈现-html

这个库让我想起了爱奥尼亚。基本思想是将 HTML 标记映射到它们相应的 React Native 组件。您甚至可以使用自定义标记和类添加样式。

我认为最大的潜力是将其与后端服务相结合，您可以将 HTML 模板提供给 React Native 应用程序进行呈现。这对于动态内容(如促销或免责声明文档)特别有用。

[](https://github.com/meliorence/react-native-render-html) [## 梅利奥伦 ce/reaction-native-render-html

### iOS/Android 纯 javascript 反应-原生组件，呈现您的 HTML 到 100%原生视图…

github.com](https://github.com/meliorence/react-native-render-html) 

# 4.反应-自然-触觉-反馈

这个库增加了一点用户反馈体验。像声音或振动这样的小互动往往会让我们感觉与应用程序“联系在一起”。这个想法在游戏世界中被广泛使用。不仅仅是游戏的音效，还有控制器上的震动。

iOS 在其生态系统中无缝实现了触觉功能，例如当你使用应用支付或确认应用下载时。尝试在您的用户旅程中添加此功能，让您的应用充满活力。

[](https://github.com/junina-de/react-native-haptic-feedback) [## 朱妮娜-德/反应-自然-触觉-反馈

### 目前，Android 的实现是一个小的振动模式，类似于 iOS 触觉系统的“感觉”…

github.com](https://github.com/junina-de/react-native-haptic-feedback) 

# 5.react-原生-解析-文本

创建到某个页面的内联链接，不像我们可以在 HTML 中添加内联`a`标签，需要 React Native 做大量的工作。在文本中嵌套组件是不可能的。当你的 app 使用内化的时候，问题就更加明显了。根据语言的不同，句子可以有不同的结构。不能以同样的方式将组件和文本连接在一起。

这个图书馆将是你的救星。您可以使用正则表达式或预定义的模式来选择单个文本。然后，您可以向它们添加样式和处理程序。例如，您可以选择 URL 并添加一个处理程序来打开浏览器。

[](https://github.com/taskrabbit/react-native-parsed-text) [## task rabbit/react-native-parsed-text

### 这个库允许您解析文本，并使用正则表达式或预定义的模式提取部分内容。目前有 3 个…

github.com](https://github.com/taskrabbit/react-native-parsed-text) 

# 结论

React 原生库的实现相对令人难以置信，因为你通常必须处理来自两个平台的 JavaScript 和原生代码。真心感谢这些库的所有贡献者。我希望它们能帮助您将应用体验提升到一个新的水平。