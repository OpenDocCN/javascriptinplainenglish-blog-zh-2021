# 如何在 React Native 中使用 FlatList 组件

> 原文：<https://javascript.plainenglish.io/how-to-use-the-flatlist-component-in-react-native-78c88972b99c?source=collection_archive---------4----------------------->

## *给大家的懒人加载列表！*

![](img/e3a1423d4fff80871da910ba3d12d0ae.png)

Photo by [Alexandru Acea](https://unsplash.com/@alexacea?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/coding?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

每个应用程序都需要列表。你的待办事项应用，你的股票应用，你的笔记应用，你的邮件应用，等等等等…

但是想象一下，如果当你打开应用程序时，邮件应用程序需要加载你所有的 2352 封未读邮件，这将需要很长时间，这取决于你手机的规格。这就是为什么我们使用叫做*延迟加载*的东西。

简而言之，惰性加载是一种通过简单地加载需要显示的内容来加载长列表的方式。像 Android RecyclerView 这样的列表更进一步改善了性能和加载时间。React Native 中的 FlatList 组件就是我们使用的 lazy loader。

我记得当我第一次使用这个组件时，我有点害怕，因为这和填充一个 ScrollView 不一样。但是在我学会使用它之后，我再也没有返回 ScrollView 查看未知长度的列表。

# 设置

我将使用一个空白的世博会项目作为我的开始。因为本文将尽可能地把重点放在 FlatList 组件上，所以我不会试图偏离太多，添加只会让它更难理解的废话。

你可以按照这里的说明[或者我写的另一篇文章中的说明](https://reactnative.dev/docs/environment-setup)来做，这篇文章的重点是让 Expo 应用程序为开发做好准备。

[](https://mbvissers.medium.com/building-your-first-react-native-app-fe4f6a1785c1) [## 构建您的第一个 React 原生应用

### 本土发展衰落的原因。

mbvissers.medium.com](https://mbvissers.medium.com/building-your-first-react-native-app-fe4f6a1785c1) 

在您准备好并拥有一个空的`App.js`文件之后，我们可以继续添加一些样本数据来迭代。

# 数据

`FlatList`使用的一个属性是`data`。这是我们首先要创建的，一些要迭代的数据。这可以是从数字数组到充满 JSON 对象的数组。我将使用一个相当简单的字符串数组。

这是目前为止基本的`App.js`。我们在一些视图中有一些文本，我们在`state`之外定义了一个数组。

我们现在可以开始创建列表了，但是让我们先检查一下如果没有`FlatList`我们会怎么做。*请注意，这并不是好的做法*，但是您可能会觉得很有趣。

同样，如果您事先不知道数据的长度，这不是一个好的做法。但是我们定义了一个`ScrollView`，在这个函数中，我们使用`map`循环遍历数据数组，并返回每个`Text`以及一个从`index`中获得的密钥。

我们的 FlatList 看起来非常相似，因为我们将使用类似于`map`的东西来呈现 FlatList 的`renderItem`属性中的每个内部组件。

然而，我们还没有定义一个键。虽然我们可以将`key`道具添加到我们渲染的`Text`组件中，但是平面列表中还有另一个名为`keyExtractor`的属性，它会自动设置关键点。

这是最后的`FlatList`组件，包含了我们现在需要的所有东西。一个漂亮的平面列表，以比我们的滚动视图更有效的方式显示所有项目。

但是下一步是什么呢？

`FlatList`组件还有一些可能有用的属性，比如`ListHeaderComponent`，您可以在其中定义一个标题，它将像项目一样滚动。因为我们当前的代码不会这样做。

这是我在每一个带`FlatList`的项目中使用的所有东西。在[官方文件](https://reactnative.dev/docs/flatlist)中有更多值得探索的地方。您已经准备好创建自己的邮件或待办事项应用程序。

# 结论

React Native 附带的`FlatList`组件是一种呈现大型数据集或数组的资源友好方式。使用`listHeaderComponent`你可以添加一个和数据列表一起滚动的标题，这样你就可以让它尽可能的像一个常规的`ScrollView`一样。

祝您的应用程序开发之旅好运，非常感谢您的阅读。祝你愉快。