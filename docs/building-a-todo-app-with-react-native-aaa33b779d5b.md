# 使用 React Native 构建 Todo 应用程序

> 原文：<https://javascript.plainenglish.io/building-a-todo-app-with-react-native-aaa33b779d5b?source=collection_archive---------5----------------------->

## *第一款真正应用的实用指南*

![](img/917e9a2c5696d5ab7a2c78626255d91c.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/coding?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在这段时间里，很多人都想学习新的东西。也许你想学习如何变戏法，如何骑摩托车，或者如何开发应用程序。

你首先尝试的是明显的 Hello World 应用程序、简单的计数器应用程序或者只是玩玩可用的组件。但是你将如何继续？

## 动机

最好的选择是那些容易上手的应用程序，你可以随着知识的进步来构建它们。Todo 应用、dice 应用或者笔记应用都是非常好的选择。可能有数百种这样的应用程序可用，但有些将在应用程序商店上为€5 甚至€10 出售。

这些昂贵的应用程序具有你可以自己构建的功能，但是你从哪里开始呢？这正是这篇博客的目的。

## 介绍

我们将使用 [React Native](https://reactnative.dev/) 构建一个跨平台的 todo 应用。

这将为你构建真正的应用程序提供一个良好的开端。然而，我需要注意的是，我假设你对 React Native 有一些非常基础的知识。

# 设置您的项目

打开 cmd 并创建一个新的 React 本地项目。

```
npx react-native init TodoApp
```

进入新目录，运行你的应用程序，确保一切正常。我在连接到我电脑的安卓手机上运行我的项目。

```
cd TodoApp && npx react-native run-android
```

如果一切正常，您可以删除所有默认代码，直到剩下一个空的 React 页面。

# 创建组件

我们需要添加的第一件事是一个使用 [useState](https://reactjs.org/docs/hooks-state.html) 和 [FlatList](https://reactnative.dev/docs/flatlist) 的状态，它将显示虚拟数据(目前)。您可以通过查看文档来尝试自己构建它，或者查看下面的代码。

它看起来像一大块代码，但是如果你把它分成几个部分，它是相当简单的。

我们从两个来源进口。我们从 React Native 导入一些**组件**，从 React 导入 React 和 useState。

在 React 本机“app”组件中，我们声明变量以使用我们的状态。我们将初始状态设置为一个包含两个字符串的数组。

在我们的 return 语句中，我们设置了想要呈现的组件。在这种情况下，它们都是来自 React Native 的组件。

我们添加了一些文本和一些基本样式的平面列表。

接下来，我们需要添加一种在状态中添加新字符串的方法。为此，我们将在新文件 TodoInput.js 中创建一个名为 TodoInput 的组件。

## 文本输入

在这个组件中，我们想要一个状态，一个[文本输入](https://reactnative.dev/docs/textinput)和某种[按钮](https://reactnative.dev/docs/button)，当我们想要添加我们的新 todo 项目时，可以点击它。我将使用一个[可触摸不透明](https://reactnative.dev/docs/touchableopacity)来代替一个按钮，以方便造型。

这个组件只有一个文本输入和一个按钮。该按钮调用我们将在 app.js 中定义的函数，因为它将从 TodoInput 组件外部更新状态。

现在你有了一个应用程序，可以将待办事项添加到状态中，并在列表中显示它们。

## 删除待办事项

下一步是添加功能来删除我们已经完成的列表项。买完东西了吗？好了，现在我们需要删除列表项。

我们通过添加一个函数来通过索引从状态数组中移除一个项目，并将其添加到 onPress 属性中。

你的应用程序现在应该可以通过点击来添加和删除列表项。你刚刚做了一个待办事项应用。干得好！

[*这里是目前为止的代码*](https://gist.github.com/mbvissers/49e12dff007b8da818768aeb2b8ccea6) *以防你错过了什么。造型略有更新。*

那么下一步是什么？现在，我们可以添加更多的功能，如带有“x”按钮的 ListItem 组件来删除它们，单击它们会显示一条线。

## 更新的列表项

你可能见过的一个功能是，当你完成一个待办事项时，你可以将它们设置为已完成。为此，我们需要更新一些东西。

我们需要给我们的状态项一个属性“completed ”,我们需要向我们的列表项添加功能。让我们首先更新 app.js 中的状态。

接下来，我们要创建一个新的 TodoItem.js 组件，用作我们的 listItem。这一新的组成部分将包括:

*   要呈现文本的文本。
*   一个可触摸的不透明/按钮，我们可以按下它来删除一个项目。
*   props 中的函数来改变 app.js 的状态。

现在，如果你更新 app.js 中的 FlatList 来使用这个组件，你会看到它看起来很不错，但我们仍然缺少一个功能。完成 todoItem 并删除文本。

我们添加 completeTodoItem 函数，并使用它需要的道具来呈现新组件。

让我们添加一些完成状态更新时的视觉效果。应该将 TodoItem.js 中最外层的视图更新为 TouchableOpacity 或类似的组件，以便能够处理压迫事件。

我们更新后的 TodoItem.js 是这样的:

如你所见，我们添加了一个更新样式的条件，在我们的返回中，我们将视图更改为 TouchableOpacity。我们还更新了第一个文本组件的样式属性，以利用条件样式。

现在我们已经完成了我们的 Todo 应用程序！恭喜你！

[*这里是完成的代码*](https://gist.github.com/mbvissers/3067e1cd990ab3eff38b31a010c62f79) *以防你漏了一步。*

# 那么下一步是什么？

当然，你可以看到还有很多事情可以做。我有一些建议，可能会帮助你通过使用这个应用程序作为模板来继续学习。

一个很好的下一步是让它在重置之间保存它的数据。你可以使用 Realm 这样的数据库，我已经就这个话题创建了一个[博客](https://medium.com/javascript-in-plain-english/getting-started-with-realm-for-react-native-c15e72c96758)。您也可以使用 SQLite 或 AsyncStorage。

另一个很好的练习是造型。也许让它看起来像你最喜欢的 todo 应用程序，或者从 [Dribbble](https://dribbble.com/) 中获得一些灵感？

祝您成为应用程序开发人员的旅途愉快。