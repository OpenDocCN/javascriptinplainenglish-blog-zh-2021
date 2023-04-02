# 用 React 挂钩构建自动注销会话超时

> 原文：<https://javascript.plainenglish.io/building-an-auto-logout-session-timeout-with-react-using-hooks-e7804ef973ec?source=collection_archive---------0----------------------->

![](img/8d860742f8e97b36c1721b1a01d3adba.png)

Picture: [https://www.pexels.com/photo/close-up-photo-of-street-clock-near-tall-building-937512/](https://www.pexels.com/photo/close-up-photo-of-street-clock-near-tall-building-937512/)

有时，用户登录到您的应用程序，却忘记注销。让我们假设在你的应用程序中有很多关于用户的敏感信息，比如个人信息或者交易数据。这使得用户数据易受攻击。

作为一名开发人员，您需要开发一个解决方案来检测应用程序上的用户非活动状态。该解决方案旨在帮助用户在不使用应用程序时注销。

在本教程中，我们将使用 react 及其钩子来构建前端。在 Vue 或 Angular 上工作时，遵循这些步骤会让您有更好的理解。

**我们开始吧！**

在我们继续之前，请注意，本教程假设您对 react 和 react 钩子有基本的了解。如果没有，请找到可用的资源，引导你通过并回到这里。

首先，让我们从在组件文件夹中创建一个 javascript 文件开始，例如 *SessionTimeout.js*

为了加快速度，让我们导入本教程需要的所有东西。你需要安装[力矩](https://momentjs.com/)。

```
npm install moment --save
```

`useState:`接受状态项的初始值，并返回一个包含状态变量的数组，以及您调用来改变状态的函数。

`useCallback:`当你有一个子组件频繁重渲染时，这个钩子很有用。

`useEffect:`该函数在组件第一次渲染时运行，并在随后的每次重新渲染/更新时运行。

`useRef:`这个钩子允许我们强制访问一个 DOM 元素。

`Fragment:`这让您可以在不增加额外节点的情况下对孩子列表进行分组。

接下来，我们列出所有需要的状态。

`events:`这个状态有助于定义我们的事件监听器。您可以添加任意数量的侦听器。

`second:`该状态有助于定义用户注销前剩余的秒数。

接下来，让我们编写一个在组件挂载时初始化定时器的函数。

`resetTimer:`首先，我们检查用户是否经过身份验证。如果是，我们在 sessionStorage 中设置时间戳，如果没有通过身份验证，我们从存储中删除时间戳。`usecallback` 钩子用于查找用户认证的变化。

在我们的`useEffect` 钩子中，我们然后在我们的**窗口中传递函数**

接下来，让我们编写一个 setTimeout 函数来检查我们存储的**时间戳。**

我们用这个函数来初始化定时器。 **setTimeout** 方法设置一个定时器，一旦定时器在 1 分钟时到期，该定时器就执行一个功能。我们从 sessionStorage 获取存储的时间戳，然后将它发送给我们的警告函数。我们一会儿会看看**警告激活**函数。

接下来，让我们运行时间检查器功能

正如你所看到的，理想的计时器正在逐渐实现。以下是更新内容:

1.  我们在**使用效果**和**重置计时器上运行**时间检查器**。**这是因为我们希望 timeChecker 在组件挂载时和窗口上有监听事件时进行检查。
2.  我们还在 resetTimer 函数中清除 setTimeout。这将帮助我们停止任何连续的循环。

现在我们已经能够编写一个时间检查器，让我们编写一个警告用户的函数。

好吧，别害怕。我知道这是一堆代码。我会解释一切。

`warningInactive:`在使用这个函数之前，让我们先清除 setTimeout。现在，我们可以使用 **setInterval** 方法。setInterval 方法被设置为每 1 秒重复运行一次。而在这里，多亏了`momentjs`，我们可以很容易地用它来检查时差。

如果您还不了解[设置超时](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)和[设置间隔](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval)之间的区别，请点击这些链接。

我们检查**当前时间**和**存储时间之间的时间差。minPast** 为过去一分钟**和 leftSecond** 为倒计时秒。

事情到此为止:

1.  最大理想时间为 2 分钟， **popTime** (通知时间)设置为用户理想时间的 1 分钟。
2.  一旦 **minPast** 等于 **popTime，我们设置秒开始计数。**
3.  您可以更改 **maxTime** 来增加用户的理想定时器。
4.  最后，一旦 **minPast** 与 **maxTime** 相等，即一旦达到用户理想的 2 分钟，我们就清除 setInterval 和 sessionStorage。

是的，我们写了很多代码。不管怎样，我们快完成了。

最后，让我们回到我们的 resetTimer 函数，并做一些清理。

以下是我们做的几件事:

1.  我们在重置计时器上添加了一个 **clearInterval** 方法。这对于避免不必要的循环是必要的。并且当用户未被认证时也清除所有运行条件。
2.  我们还添加了组件卸载后的清理。

终于！一切就这些了。现在，我们可以通过将 **SessionTimeout.js** 添加到 **app.js** 中或者您认为需要它的地方来测试我们的代码。

为了增加趣味，您可以将`fragment`更改为通知用户警告的模态。你也可以把它应用到其他框架中。

本教程的完整代码可以在 https://github.com/sadewole/Idle-session-timer 找到。多亏了弗拉维奥·科普斯，我使用了他对钩子的定义。

请喜欢并留下任何贡献的评论。谢谢你。