# 如何在 Chrome 扩展中发送通知

> 原文：<https://javascript.plainenglish.io/how-to-send-notifications-in-chrome-extensions-7b7b3f5a0e9b?source=collection_archive---------15----------------------->

![](img/85cdc7c1065974a3a7d5d46a95728345.png)

在本教程中，我们将讨论如何在 Chrome 扩展中发送通知。我们将讨论如何发送一个通知，以及如何安排在以后发送通知。

## 先决条件

本教程假设你已经知道如何创建一个 Chrome 扩展。如果你没有，那么这里的是你可以先开始的。

## 设置权限

在您发送任何类型的通知之前，您需要首先在您的`permissions`键中添加以下内容:

```
"permissions": [
          "notifications"
          //other permissions in your extension
  ]
```

这意味着用户在安装或更新您的扩展时必须接受他们将收到通知，以便使用该扩展。

## 发送通知

要发送通知，您需要使用[通知 API](https://developer.chrome.com/docs/extensions/reference/notifications) 。特别是`chrome.notifications.create`方法，它采用以下必需选项:

```
chrome.notifications.create('NOTFICATION_ID', {
    type: 'basic',
    iconUrl: 'path',
    title: 'notification title',
    message: 'notification message',
    priority: 2
})
```

以下是这些选项的含义:

1.  **NOTIFICATION_ID:** 通知的 ID。这可能是更新通知或清除通知所必需的。
2.  **类型:**通知的类型。其值可以是“基本”、“图像”、“列表”、“进度”
3.  **iconUrl:** 应该在通知中显示的图标的路径。这应该是相对于你的扩展的根。
4.  **标题:**通知的标题。
5.  **消息:**通知中显示的消息。
6.  **优先级:**这个不是必须的，但是我推荐包含。它的值可以从-2 到 2，其中-2 是最低优先级，2 是最高优先级。此选项的默认值为 0，因此如果不包含此选项，您的通知可能会被忽略。还应注意，小于 0 的值会在没有通知中心的设备上产生错误。

还有其他一些可选选项:

**按钮:**您希望在通知中显示的按钮。这需要一个最多包含 2 个按钮的按钮数组。该数组应该是一个具有属性`title`的对象，该属性将是按钮的标题。例如:

```
buttons: [
    {
        title: 'Yes'
    },
    {
        title: 'No'
    }
]
```

**上下文消息:**该消息将以较低的字体显示。

**事件时间:**与通知相关联的时间戳。例如:

```
eventTime: Date.now()
```

**项目:**这将只在 Mac OS X 上显示。这对于`list`类型的通知可能很有用。例如:

```
items: [
    {
        title: 'Item 1',
        message: 'This is first item'
    }
]
```

**进度:**这对于`progress`类型的通知很有用。它取 0 到 100 之间的值

**requiresInteraction:** 这个只适用于 50 以后的 Chrome 版本。其值为布尔值。如果设置为 true，这意味着通知不会从屏幕上消失，直到用户通过单击它或取消它来与消息进行交互。此项的默认值为 false。

**静音:**这个只对 70 以后的 Chrome 版本有效。它的值是布尔值。如果设置为 true，那么通知将不会发出声音或振动。默认值为 false。

要向用户发送仅显示消息的基本通知:

```
chrome.notifications.create('test', {
    type: 'basic',
    iconUrl: 'images/1.png',
    title: 'Test Message',
    message: 'You are awesome!',
    priority: 2
});
```

这将在执行时发送一个通知。

## 计划通知

在许多情况下，您实际上并不想现在发送通知，或者您希望每隔一段时间发送一次通知，比如一天一次。为此，我们将使用[警报 API](https://developer.chrome.com/docs/extensions/reference/alarms/) 。

警报允许我们安排某件事在以后运行。创建提醒时，您可以指定提醒运行的时间间隔。然后，您可以收听警报，并在警报运行时执行您想要的任何代码。

为了能够使用警报，我们还需要在`manifest.json`中将其包括在我们的权限中:

```
"permissions": [
          "alarms",
          "notifications"
          //other permissions your extension require
  ],
```

要按特定时间表发送通知，工作流程如下:

1.  创建以特定时间间隔运行的警报
2.  注意听闹钟什么时候响
3.  当警报运行时，执行一些逻辑并创建一个通知

## **创建一个以特定时间间隔运行的警报**

为了创建警报，我们将使用`chrome.alarms.create`方法:

```
chrome.alarms.create('ALARM_NAME', {
    //options
});
```

你只需要指定闹钟的名字`ALARM_NAME`，以后听闹钟的时候会用到。不需要其他选项。但是，如果您在没有选项的情况下使用它，警报只会在创建时运行一次。

您可以传递的选项有:

**什么时候:**闹钟应该什么时候开始工作。如果您希望它立即启动:

```
when: Date.now()
```

**周期分钟:**这是我们指定闹钟运行的时间。它需要一个数字，即每次报警之间的分钟数。所以，如果我想让闹钟每五分钟响一次:

```
periodInMinutes: 5
```

**delay minutes:**指定`onAlarm`事件在触发前是否应该延迟一点。

这里最重要的选项是`periodInMinutes`。它指定了我们希望何时创建通知。

因此，如果我们想要创建一个提醒，让我们创建一个每天运行的通知:

```
chrome.alarm.create('testAlarm', {
	periodInMinutes: 1440
});
```

## **监听闹钟何时响起**

下一步是当警报响起时进行监听。这通常应该在清单 V2 的后台脚本中完成，或者在清单 V3 的服务工作人员中完成。

*你可以在这里* *阅读更多关于 Manifest V2 和 V3* [*的区别。*](https://blog.shahednasser.com/chrome-extension-tutorial-migrating-to-manifest-v3-from-v2)

如果你不知道什么是后台脚本，正如它的名字所说，它是一个总是在后台运行的脚本，即使你的扩展的页面或弹出窗口或你的扩展使用的任何东西没有打开或运行。这有助于我们随时收听事件、警报、消息等。

Manifest V3 中引入了服务工作器，作为后台脚本的替代。主要区别在于服务人员并不总是跑步。服务人员向警报、消息等注册事件监听器，与后台脚本相同，因此只有监听器在必要时运行，如事件发生时。

如果你的 chrome 扩展中还没有后台脚本，你需要首先在`manifest.json`中包含它:

```
"background": {
    "scripts": ["js/background.js"],
    "persistent": false
},
```

或者，如果您使用的是 Manifest V3，您需要注册一个服务人员:

```
"background": {
    	"service_worker": "js/background.js"
 },
```

然后，在脚本中，我们将使用接受回调函数的`chrome.alarms.onAlarm.addListener`来监听警报，这将是我们的监听器。这个回调函数将在我们的扩展中的警报每次运行时执行，所以我们需要确保我们只监听我们需要的警报，我们将其命名为`testAlarm`:

```
chrome.alarms.onAlarm.addListener((alarm) => {
    if (alarm.name === "testAlarm") {
        //our alarm is running, send notification
    }
});
```

我们需要检查`alarm.name === "testAlarm"`，以确保我们的通知警报正在运行。如果您的扩展中有多个警报，这也很重要，以确保您正在为正确的警报执行所需的逻辑。

因此，如果条件为真，我们可以创建通知。

## 当警报运行时，执行一些逻辑并创建一个通知

根据您的用例，您可能会执行一些逻辑，可能会向服务器或任何其他逻辑发送请求，然后运行通知。

我们要做的是，在警报运行时创建消息。这是可以做到的:

```
chrome.alarms.onAlarm.addListener((alarm) => {
    if (alarm.name === "testAlarm") {
        chrome.notifications.create('test', {
            type: 'basic',
            iconUrl: 'images/1.png',
            title: 'Test Message',
            message: 'You are awesome!',
            priority: 2
        });
    }
});
```

在这 3 个步骤之后，我们的扩展将创建一个每天运行一次的警报，并执行我们添加到`onAlarm`事件的监听器中的代码。该侦听器将创建一个通知。因此，每天都会向用户发送通知。

## 在 Firefox 上发送通知

在 Firefox 上发送通知是完全一样的，除了你只需要在所有使用`browser.*`的方法中替换`chrome.*`。你可以在这里阅读更多关于火狐和 Chrome 的区别。

## 摘要

要创建通知，您需要:

1.  将`notifications`添加到`manifest.json`的`permissions`阵中
2.  使用`chrome.notifications.create`创建并发送通知。

要安排通知按时间间隔运行，您需要:

1.  将`alarms`添加到`manifest.json`中的`permissions`数组
2.  使用`chrome.alarms.create`创建一个警报。
3.  用`chrome.alarms.onAlarm.addListener`监听警报，并在监听器中创建一个通知。

*如果您想连接并谈论更多关于本文或编程的一般内容，您可以在我的 Twitter 帐户*[*@ shahednasserr*](https://twitter.com/shahednasserr)*上找到我。本文原载于* [*我的个人博客*](https://blog.shahednasser.com/how-to-send-notifications-in-chrome-extensions/) *。*

*更多内容请看*[***plain English . io***](http://plainenglish.io)