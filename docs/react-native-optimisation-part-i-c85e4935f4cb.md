# React 本机优化:指南

> 原文：<https://javascript.plainenglish.io/react-native-optimisation-part-i-c85e4935f4cb?source=collection_archive---------10----------------------->

![](img/4cd71d48d2f376a51b515bfbd5447199.png)

Photo by [Tudor Baciu](https://unsplash.com/@baciutudor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

根据 [Akamai 的报告](https://www.akamai.com/us/en/multimedia/documents/report/akamai-state-of-online-retail-performance-2017-holiday.pdf)，移动加载时间延迟一秒钟**就可以将转换率降低 20%**

这是第一部分，我们将讨论反应式优化的几个主题，下一部分我们将讨论如何使用本机端、CI、OTA 等来改进优化和部署。

# **不正确的状态更新导致额外的渲染周期/或设备太慢**

React Native 负责为您呈现应用程序。您的工作是定义您需要的所有组件，并用这些更小的构建块组成最终的界面。在这种方法中，您无法控制应用程序渲染生命周期。

![](img/0498e66f5c8ff4559420533717cd5d6c.png)

大多数性能问题是由于错误或不必要的全局或局部状态更新造成的。它对性能、UI 闪烁和 FPS 下降有负面影响。

1.  **错误使用了使用状态挂钩**

```
const [data,setData] = useState(processData());
```

我看到了这种类型的代码片段，开发人员不是传递一些 init 数据，而是传递处理一些数据的方法，这可能需要一毫秒或一秒，这取决于复杂性。这不是一个好主意，这会使你的屏幕延迟打开。

最好使用生命周期“useEffect”。

2.**慢速设备的问题**

上面的代码在大多数情况下运行良好，但是当由于 RN 异步的性质而打字太快时，它在慢速设备中产生了问题，因为这是一个双向操作 React 处理信息并通过调用 setState 相应地更新它的状态。接下来，典型的受控组件将其 JavaScript 值与本机组件值同步。

这种方法不错，但如果设备资源有限，并且由于内存不足，它开始闪烁，就不好了。同步问题的解决方案之一是从 TextInput 中完全删除 value prop。因此，数据只会单向流动，从本机流向 JavaScript 端。

然而，正如 [@nparashuram](https://twitter.com/nparashuram) 在他的 YouTube 视频(这是了解 React 原生性能的一个很好的资源)中所指出的，[在某些情况下，仅仅这种解决方法是不够的](https://www.youtube.com/watch?v=83ffAY-CmL4&t=1483s)。RN 团队也在研究这个问题。

# **对某些布局使用专用组件**

在原始组件之上，用一组为特定目的而设计和优化的高阶组件来反应原生船只。

![](img/f28e2a8279eb84e969caeb3977020b44.png)

不知道它们或者不在所有地方使用它们可能会影响应用程序的性能，特别是当您用真实的生产数据填充状态时

一些开发人员使用滚动视图，然后基于数组大小使用映射视图，但这不是一个好主意，如果我们有一些专用组件，那么我们为什么要尝试这样做。

当我们有很多不同大小的数据时，有时甚至一个平面列表也很慢，在这种情况下，我们需要返回固定高度(参见下面的代码片段)。

# **选择外部库之前要小心**

问题是大多数开发人员在挑选库时没有检查里面有什么！只为一个方法，选择整个大的库。

开发人员会发现很难从支持相同用例的多个库中进行选择。如何使用正确的 JavaScript 库帮助您提高应用程序的速度和性能。当选择一个用于下一个项目时，他们通常会研究告诉他们库是否健康和维护良好的指标，例如 Github stars、发行数量、贡献者和 PRs。

这是不正确的，因为移动开发的基础是不同的，我们需要寻找资产的大小、位置、库的大小和支持特性的数量、设备支持等。

```
import moment from ‘moment’
const date = moment(“12-25-1995”, “MM-DD-YYYY”);
```

我在许多项目中看到这种类型的任务开发使用的时刻，完全是 67kb 大小的文件。

我们可以使用 day.js(只有 2Kb ),它要小得多，并且只提供我们需要的功能

```
import dayjs from ‘dayjs’
const date = dayjs(“12-25-1995”, “MM-DD-YYYY”);
```

如果没有其他选择，最好的经验是检查是否可以导入库的一小部分。

**好处是“您的应用加载速度更快，这一点至关重要”**

# **永远记得使用移动平台专用的库**

问题是你使用的网络库没有为移动优化。未优化的库会导致电池耗尽，并降低应用程序的速度。操作系统可能会限制您的应用程序功能。

让我们以 Firebase 为例，它提供了适用于 web、android 和 Ios 的 SDK。您可以运行它的 web 版本，不会有什么大问题:

```
import database from ‘firebase/database’;
database()
 .ref(‘/users/123’)
 .on(‘value’, snapshot => {
 console.log(‘User data: ‘, snapshot.val());
 });
```

上面的例子很好地说明了这一点，它不能给你和手机一样的性能。

在这个特定的例子中，最好使用专用的 Firebase 库，它在专用的本地 SDK 上提供一个薄层，并提供与任何其他本地应用程序相同的性能和稳定性。

感谢阅读 react-native 优化的第一部分，我在一些实际项目中看到了所有这些要点大多数开发人员由于任何原因都会犯这种类型的错误，但这会导致性能或闪烁问题。

在下一部分，包括

1.  用脚蹼调试。
2.  使用 herms 进行 android 优化。
3.  优化 android 的梯度设置。
4.  OTA 和 CI/CD。

[](https://github.com/prabhat1707) [## prabhat1707 -概述

### 霍尼韦尔的 SDE 2 | Android | React Native | tensor flow Block 或 Report 从 ncapdevi/FragNav An Android 分叉…

github.com](https://github.com/prabhat1707) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)