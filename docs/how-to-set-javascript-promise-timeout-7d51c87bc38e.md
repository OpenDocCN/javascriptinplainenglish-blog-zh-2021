# 如何为 JavaScript 承诺设置超时

> 原文：<https://javascript.plainenglish.io/how-to-set-javascript-promise-timeout-7d51c87bc38e?source=collection_archive---------5----------------------->

## 提示和技巧

## 只是不要永远等待承诺的实现，你需要设定自己的条件。

![](img/c3f2a002b4398dc0091d083c31aad8f6.png)

Image by [cherylholt](https://pixabay.com/users/cherylholt-209609/) on [Pixabay](https://pixabay.com)

你有没有想过为什么不能为你的 JavaScript 承诺设置一个超时？你并不孤单。

我以前也有同样的问题，实际上，我找不到**为什么**的答案。但我最终决定停止思考，开始行动。

为 JavaScript 承诺实现超时并不困难，您可以自己轻松完成。

[](https://medium.com/subscribe/@eng_ahmed.tarek) [## 订阅艾哈迈德的时事通讯？

### 订阅艾哈迈德的时事通讯📰直接获得最佳实践、教程、提示、技巧和许多其他很酷的东西…

medium.com](https://medium.com/subscribe/@eng_ahmed.tarek) 

# 这是我思考问题的方式

1.  超时本身可以使用本机的`setTimeout()`函数来实现。
2.  我可以利用本机的`Promise.race()`函数，这样我就可以在超时和最初的承诺之间开始一场比赛。
3.  这样，我可以将超时作为一个承诺来实现。
4.  剩下的部分是关于如何将小部分整合在一起，以获得预期的结果。

# 履行

## 等待

这里的**超时**部分是作为**承诺**本身实现的。这是通过将原生的`setTimeout()`函数包装成一个承诺来实现的，该承诺将总是解析为常量字符串`‘time out’`。你可以根据需要修改这个部分，你甚至可以返回一个对象。

## PromiseWithTimeout 超时

这里，新的 Promise 功能被定义为一个名为 **PromiseWithTimeout** 的新对象类型，这样它就可以像使用本地 **Promise** 对象一样使用。因此，你应该使用`let myPromise = new PromiseWithTimeout(…)`，而不是`let myPromise = new Promise(…)`。

主要思想是使用原生的`Promise.race()`函数，然后返回我们定义的**原始承诺**和**等待承诺**之间的竞争承诺。

## **使用 PromiseWithTimeout**

现在你可以开始轻松使用新的 **PromiseWithTimeout** 了。

## 从 PromiseWithTimeout 获取结果

现在，根据您决定如何解决 **wait** 承诺，您可以断言返回的结果，以检查它是超时还是最初承诺的实际结果。

# 希望这些内容对你有用。如果您想支持:

如果您还不是**中型**会员，您可以使用 [**我的推荐链接**](https://medium.com/@eng_ahmed.tarek/membership) ，这样我就可以从**中型**中获得您的一部分费用，您无需支付任何额外费用。订阅
[**我的简讯**](https://medium.com/subscribe/@eng_ahmed.tarek) 将最佳实践、教程、提示、技巧和许多其他很酷的东西直接发送到您的收件箱。

# 其他资源

这些是您可能感兴趣的其他资源。

[](/how-to-use-observables-with-vanilla-javascript-aca40a7590ff) [## 如何在普通 JavaScript 中使用 Observables

### 没有使用框架，只是纯香草 JavaScript。

javascript.plainenglish.io](/how-to-use-observables-with-vanilla-javascript-aca40a7590ff) [](/how-to-customize-webpages-ui-behavior-using-javascript-userscripts-7b6a090e0135) [## 使用 JavaScript 用户脚本定制网页用户界面/行为

### 即使你不拥有这个网页，你仍然可以附上你的 JavaScript 用户脚本。

javascript.plainenglish.io](/how-to-customize-webpages-ui-behavior-using-javascript-userscripts-7b6a090e0135) [](/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220) [## 如何在你的 Slack 频道上获得自由职业者的新项目通知

### 这是一个设置用户脚本的问题，我将为您提供。

javascript.plainenglish.io](/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220) [](https://betterprogramming.pub/twitter-auto-retweet-bot-with-node-js-and-typescript-4d6eaf24c0ab) [## 用 Node.js 和 TypeScript 构建一个 Twitter 自动转发机器人

### 了解如何创建一个 Twitter 机器人来转发任何带有特定关键字或标签的推文

better 编程. pub](https://betterprogramming.pub/twitter-auto-retweet-bot-with-node-js-and-typescript-4d6eaf24c0ab) [](https://levelup.gitconnected.com/paging-partitioning-main-equations-to-make-it-easy-44fe89d5290b) [## 分页/分区—简化这一过程的主要等式

### 最后，这是您理解分页/分区主要等式并学习如何在代码中应用它们的机会。

levelup.gitconnected.com](https://levelup.gitconnected.com/paging-partitioning-main-equations-to-make-it-easy-44fe89d5290b) 

最后，希望你觉得读这个故事和我写它一样有趣。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)