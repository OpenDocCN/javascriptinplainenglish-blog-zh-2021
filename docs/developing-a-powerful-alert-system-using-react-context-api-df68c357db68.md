# 使用 React Context API 开发强大的警报系统

> 原文：<https://javascript.plainenglish.io/developing-a-powerful-alert-system-using-react-context-api-df68c357db68?source=collection_archive---------3----------------------->

## React 的上下文 API 的一个实际例子

![](img/d82ea21cdedbe0393d4cf3eb000fd7d3.png)

Photo by [Bastian Riccardi](https://www.pexels.com/@rcbt?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/black-and-gray-bicycle-handle-bar-with-bell-near-canal-112377/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

React 上下文 API 增强了我们的 React 应用程序。现在我们可以用 pure React 做一些事情，而不需要像 Redux 这样的其他库的帮助，这在以前是不可能的。

今天我将分享我是如何在一个大规模的应用中使用上下文的。

我们将建立一个警报系统。每当任何用户点击一个按钮或者用户需要在一个模态中看到一些信息时，我们将使用上下文来压缩一个组件内部的逻辑。

让我们开始吧…

# 概述:

主要过程将是这样的

*   我们将创建一个带有缩减器的上下文。
*   我们用那个上下文包装整个<app>组件</app>
*   然后从任何组件，我们将触发一个动作来更新上下文的值
*   警报组件将使用上下文，从而避免不必要的重新呈现。
*   每当上下文中发生任何更新时，就会触发警报组件。

# 步骤 1:让警报类型

让我们首先定义我们将在这里处理哪种类型的警报。创建一个名为`AlertTypes.ts`的文件。并将下面的代码放在那里。

# 步骤 2:警报操作

现在创建一个动作文件。我们可以创建一个包含所有动作和 reducers 的文件，但是这样更简洁。

在这个文件中，我们现在已经添加了 2 个动作。我们的`showSuccessAlert()`函数将单个参数作为消息。这是我们将向用户显示的消息。

# 第二步:警告减少器

现在我们将创建我们的 reducer 文件。我们的警报缩减器是一个简单的函数，它检查动作类型并设置我们的状态值。

AlertReducer.ts

# 步骤 4:提醒商店

现在是时候创建我们的商店了。我们将使用`useReducer`钩子做出反应。我们的状态只有一个名为`alertShower`的变量。该变量将保存报警的`type`和`message`。

# 步骤 5:包装组件

现在我们需要用这个上下文来包装我们的应用程序，因为警报可以从任何地方触发。

App.tsx

注意我们是如何包含一个名为`AlertPopup`的特殊组件的。这将是我们的警报组件。我们需要这是全球性的，因为在整个应用程序中只有一个警报组件。

# 步骤 6:警报组件

我们使用材质界面对话框作为我们的警报。可以使用任何设计库，甚至可以使用自己的设计库。

我们不需要在所有需要向用户显示信息的地方反复包含这个组件。

# 第七步:使用警告

现在我们需要测试我们为自己创造了什么。创建一个名为`AlertButton.tsx`的按钮。把这个组件放在你想放的任何地方。

该按钮将发送一个动作，该动作将更新警报上下文的值，进而触发我们的警报组件。

多棒啊。

# 引人深思的事

那么，如果您需要向这个警报模型添加一些动作，您会怎么做呢？你能做到吗？

# 结论

本文是关于使用 React 的上下文 API 构建现实生活中的应用程序的实用指南。

几乎所有的应用程序都需要一些反馈机制。希望这能有所帮助。如果你有什么不明白的，请告诉我。

祝您愉快！

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) **或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**

[](https://betterprogramming.pub/my-frustrations-with-the-context-api-in-react-26189fcd5371) [## 我对 React 中的上下文 API 感到失望

### 以及为什么我的下一个项目会选择 Redux

better 编程. pub](https://betterprogramming.pub/my-frustrations-with-the-context-api-in-react-26189fcd5371) 

*更多内容看* [***说白了. io***](http://plainenglish.io/)