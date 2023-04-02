# 使用 JavaScript 用户脚本定制网页用户界面/行为

> 原文：<https://javascript.plainenglish.io/how-to-customize-webpages-ui-behavior-using-javascript-userscripts-7b6a090e0135?source=collection_archive---------4----------------------->

## 提示和技巧

## 即使你不拥有这个网页，你仍然可以附上你的 JavaScript 用户脚本。

![](img/f6c5f2ee4f4f1f104634a8ff6a830061.png)

Photo by [Jim Manning](https://freeimages.com/photographer/binsurf-42051) from [FreeImages](https://freeimages.com/)

在某种程度上，我们每个人都面临过这样的情况，当他发现一些网站(如脸书、LinkedIn、谷歌等)缺少一些本可以通过一点 JavaScript 完成的东西。但是，不幸的是，我们对此无能为力，因为我们不拥有网站，我们不能改变它的代码。但是，故事就这样结束了吗？

感谢用户脚本和可以运行它们的浏览器插件/扩展，我们有了一个解决方案。

[](https://medium.com/subscribe/@eng_ahmed.tarek) [## 订阅艾哈迈德的时事通讯？

### 订阅艾哈迈德的时事通讯📰直接获得最佳实践、教程、提示、技巧和许多其他很酷的东西…

medium.com](https://medium.com/subscribe/@eng_ahmed.tarek) ![](img/5cc1fc9d0ffb22df0d3e2f9c8fba9ec7.png)

Photo by [Olga Thelavart](https://unsplash.com/@olga_o?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/note?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText), modified by [Ahmed Tarek](https://medium.com/@eng_ahmed.tarek)

## 2021–11–04

> 我创造了一个关于 [**的有趣故事，学习如何开发一个用户脚本来监控自由职业者的新项目，并将它们发布到你的休闲频道**](/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220?sk=8a003a6f0e99382a8732ff9c9d7a2025) 。我鼓励你去那里看看。

![](img/892aaa7e75a86cea0643762ecffa1ba9.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

UserScript 是一段写在文本文件中的 JavaScript，很可能有扩展名`.user.js`。在这段 JavaScript 代码中，你可以访问一个网页向最终用户展示的所有内容，所以没有任何可疑之处。您可以通过添加、移除、移动和样式化 HTML 元素来操作 UI。此外，您可以修改某些元素的行为，甚至添加新的行为。这完全取决于你的需要。

值得一提的是，UserScript 中的所有 JavaScript 代码将只在您这边的网页上执行，所以不要期望您的代码会以某种方式找到网页最初驻留的 web 服务器，并在那里注入自己。

有一些著名的在线用户脚本库，在那里你可以分享你自己的用户脚本，也可以找到其他开发者创建的其他用户脚本。

这些在线存储库包括:

*   [油腻的叉子](https://greasyfork.org/en)
*   [OpenUserJs](https://openuserjs.org/)
*   [牛逼](https://project-awesome.org/brunocvcunha/awesome-userscripts)
*   [最佳开源](https://www.findbestopensource.com/tagged/userscript)
*   [用户脚本区域](https://www.userscript.zone/?utm_source=tm.net&utm_medium=scripts)

![](img/1cfcc77ba0944ebb4d6314649a142f5c.png)

**浏览器插件/扩展**允许你设置一些配置来控制哪个用户脚本在哪个网页上运行，一旦它被加载到你的浏览器中。这些配置的一部分是在 UserScript 本身中设置的，稍后我将向您展示。

以下是最著名的插件/扩展列表:

*   [油滑猴](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/)
*   [Tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en)
*   [暴力猴子](https://chrome.google.com/webstore/detail/violentmonkey/jinjaccalgkegednnccohejagnlnfdag?hl=en)
*   [FreeStylerWs](https://freestyler.ws/)
*   [发射架](https://launchlet.dev/en/)
*   火猴

因此，根据你的浏览器类型，你可以选择适合你需要的插件。

![](img/ae5e9d94cffdf159967b7a8f1545f6f2.png)

Photo by [Emily Morter](https://unsplash.com/@emilymorter?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 用户脚本看起来像什么？

用户脚本很可能由以下内容组成。

## 用户脚本标题

在标题上，您可以设置一些配置浏览器插件/扩展的字段。

**名称**:用户脚本的名称。这在浏览器插件/扩展的仪表板中使用，以便您可以识别这个特定的用户脚本。

**名称空间**:用于避免公共在线存储库中托管的脚本之间的命名冲突。如果你称你的脚本为`foobar`,而其他人也这么做，那么就很难将他们区分开来。在上面的例子中，我将其设置为我的 LinkedIn 个人资料，因为这是我独有的。

**描述**:是浏览器插件/扩展的仪表板内出现的描述。

**匹配/包含**:用于匹配运行用户脚本的网页 URL 的模式。这可以接受正则表达式或通配符。关于什么是可接受的或者不可接受的更多信息，你需要检查你正在使用的浏览器插件/扩展。

**require** :是您设置代码成功运行所需的任何外部 JS 文件的地方。在上面的代码中，我包含了`jquery-3.3.1.min.js`,因为我在代码中使用了 jQuery。

**作者**:是用户脚本的作者。在上面的代码中是我。

**用户脚本体**

这是放置 JavaScript 代码的地方。它就在标题下面，不多也不少。

![](img/b5776995406efeaf8e011a34569acad6.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我不久前已经开发了一些用户脚本。您可以在这里查看它们[，在这里](https://greasyfork.org/en/users/6079-ahmedtarekhasan)查看[。](https://openuserjs.org/users/fidodido91/scripts)

此外，我创造了一个关于 [**的有趣故事，学习如何开发一个用户脚本来监控自由职业者的新项目，并将它们发布到你的 Slack 频道**](/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220?sk=8a003a6f0e99382a8732ff9c9d7a2025) 。我鼓励你去那里看看。

[](/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220) [## 如何在你的 Slack 频道上获得自由职业者的新项目通知

### 这是一个设置用户脚本的问题，我将为您提供。

javascript.plainenglish.io](/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220) 

最后，我鼓励你在互联网上浏览用户脚本，看看当你释放用户脚本的力量时你能做些什么。然后，你可以试着开发你自己的用户脚本并与他人分享。

# 希望这些内容对你有用。如果您想支持:

如果您还不是**中的**会员，您可以使用 [**我的推荐链接**](https://medium.com/@eng_ahmed.tarek/membership) ，这样我就可以从**中**获得您的一部分费用，您无需支付任何额外费用。订阅 [**我的简讯**](https://medium.com/subscribe/@eng_ahmed.tarek) 将最佳实践、教程、提示、技巧和许多其他有趣的东西直接发送到您的收件箱。

# 其他资源

这些是您可能感兴趣的其他资源。

[](/how-to-set-javascript-promise-timeout-7d51c87bc38e) [## 如何设置 JavaScript 承诺超时

### 只是不要永远等待承诺的实现，你需要设定自己的条件。

javascript.plainenglish.io](/how-to-set-javascript-promise-timeout-7d51c87bc38e) [](/how-to-use-observables-with-vanilla-javascript-aca40a7590ff) [## 如何在普通 JavaScript 中使用 Observables

### 没有使用框架，只是纯香草 JavaScript。

javascript.plainenglish.io](/how-to-use-observables-with-vanilla-javascript-aca40a7590ff) [](/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220) [## 如何在你的 Slack 频道上获得自由职业者的新项目通知

### 这是一个设置用户脚本的问题，我将为您提供。

javascript.plainenglish.io](/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220) [](https://betterprogramming.pub/twitter-auto-retweet-bot-with-node-js-and-typescript-4d6eaf24c0ab) [## 用 Node.js 和 TypeScript 构建一个 Twitter 自动转发机器人

### 了解如何创建一个 Twitter 机器人来转发任何带有特定关键字或标签的推文

better 编程. pub](https://betterprogramming.pub/twitter-auto-retweet-bot-with-node-js-and-typescript-4d6eaf24c0ab) [](https://levelup.gitconnected.com/paging-partitioning-main-equations-to-make-it-easy-44fe89d5290b) [## 分页/分区—简化这一过程的主要等式

### 最后，这是您理解分页/分区主要等式并学习如何在代码中应用它们的机会。

levelup.gitconnected.com](https://levelup.gitconnected.com/paging-partitioning-main-equations-to-make-it-easy-44fe89d5290b) 

希望你觉得读这个故事和我写它一样有趣。

*更多内容尽在* [***说白了***](http://plainenglish.io)