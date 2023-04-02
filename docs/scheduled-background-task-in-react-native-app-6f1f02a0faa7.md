# 在 React 本机应用中计划后台任务

> 原文：<https://javascript.plainenglish.io/scheduled-background-task-in-react-native-app-6f1f02a0faa7?source=collection_archive---------0----------------------->

## 如何在 React 本机应用程序中调度定期后台任务

![](img/a371ef99e61d4429f7d1e31c5c2b007f.png)

Source ([link](https://www.progress.com/blogs/the-react-native-sdk-for-kinvey-is-now-available))

在本文中，我将带您了解在 React 本地应用程序中创建后台任务的过程。目标是拥有一个定期运行的调度作业，即使在应用程序关闭时也能执行一些任务。

在开始之前，我们先讨论一下后台作业的局限性:

*   任何 UI 交互都是不可能的，因此所有执行的代码都应该存在于任何 React 组件之外。
*   两个作业之间的最短持续时间为 15 分钟。
*   任务执行的确切时间是不可预测的。
*   对于 Android，当应用程序在前台时，任务不会运行。
*   对于 iOS，用户手动关闭应用程序后，后台获取将不会继续运行。
*   模拟器中不会安排后台任务。

让我们直接进入代码，看看如何建立一个基本的工作流。我们将使用[react-native-background-task](https://github.com/jamesisaac/react-native-background-task)库进行后台作业。

## 步骤 1:安装 NPM 软件包

运行以下命令来安装 NPM 软件包。

```
npm install react-native-background-task --save
```

RN≥60 时，应该会自动链接，但对于 Android，需要额外的手动步骤。在`MainApplication.java`文件的`onCreate`方法中添加下面一行。

```
import com.jamesisaac.rnbackgroundtask.BackgroundTaskPackage;@Override
public void onCreate() {
  ...
  BackgroundTaskPackage.useContext(this);
}
```

## 步骤 2:为您的后台任务实现该方法

接下来，为`task.js`创建一个单独的文件，并为你的后台任务创建一个实现逻辑的函数。如果需要在作业中使用 redux 状态，可以导入存储并获得如下所示的状态。

**注意:** store 是您的 redux-store 的实例。

## 步骤 3:定义后台任务

在`App.js`之外的`App`组件定义你的后台任务。我们使用前面定义的`backgroundSync`方法在任务内部调用。

## 步骤 4:计划后台任务

最后，让我们从 app 组件内部调度后台任务。请注意，我们没有为任务提供任何标识符(例如名称或 id ),因此我们可以用这种方法定义一个后台任务。在本例中，我们计划每 30 分钟运行一次作业。最短可以是 15 分钟。

## 奖励:检查后台任务的状态

您还可以检查您的后台任务的状态，以确保一切工作顺利。在这个方法中，您可以处理失败场景，以触发一个分析事件来收集关于失败的信息。

这里有一个完整的例子，展示了在定义了上述方法之后，App.js 可能的样子。

就这样，您现在应该已经为您的应用程序配置了一个后台作业。

我希望这篇文章对你有用。请在评论中让我知道你的想法。考虑成为中级会员[继续阅读我所有的优质文章以及 1000 多个其他故事。](https://utkarshabakshi.medium.com/membership)

你可以在这个[列表](https://utkarshabakshi.medium.com/list/react-native-development-0d5f690f6585)中找到我关于 React 原生开发的其他文章。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)