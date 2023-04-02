# 了解如何开发一个 JavaScript 用户脚本来监控自由职业者的项目并发布到 Slack

> 原文：<https://javascript.plainenglish.io/how-to-get-freelancers-new-projects-notifications-on-your-slack-channel-69c9c74d3220?source=collection_archive---------13----------------------->

## 提示和技巧

## 使用依赖注入(DI)和控制反转(IoC)

![](img/0f0e98f008a5288be0fe3ce66cc79cad.png)

Image by [Ahmed Tarek](https://medium.com/@eng_ahmed.tarek)

这个故事是关于学习如何开发一个**用户脚本**来监视**Freelancer.com**项目通知，并将它们发送到你的 **Slack** 频道。您可以设置您感兴趣的技能，脚本将只向您发送与这些技能相关的项目通知。

如果你不熟悉术语**用户脚本**，或者不知道如何设置一个用户脚本来工作，可以查看我的故事 [**如何使用 JavaScript 用户脚本**](https://medium.com/@eng_ahmed.tarek/how-to-customize-webpages-ui-behavior-using-javascript-userscripts-7b6a090e0135) 定制网页 UI/行为。

[](/how-to-customize-webpages-ui-behavior-using-javascript-userscripts-7b6a090e0135) [## 使用 JavaScript 用户脚本定制网页用户界面/行为

### 即使你不拥有这个网页，你仍然可以附上你的 JavaScript 用户脚本。

javascript.plainenglish.io](/how-to-customize-webpages-ui-behavior-using-javascript-userscripts-7b6a090e0135) [](https://medium.com/subscribe/@eng_ahmed.tarek) [## 订阅艾哈迈德的时事通讯？

### 订阅艾哈迈德的时事通讯📰直接获得最佳实践、教程、提示、技巧和许多其他很酷的东西…

medium.com](https://medium.com/subscribe/@eng_ahmed.tarek) ![](img/fe384505793a3e34b0d1f55ce9db5872.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

以下是一些你需要牢记的重要注意事项:

1.  将`EUR`更改为您自己的**首选货币**。
2.  改[《c#编程》，”。NET”、“ASP。NET "，… ]到你的技能阵列。请注意，您应该输入 Freelancer.com 定义的技能。
3.  将`lk6f7fd0–277z-12ec-8894–41n9e18q3291`改为自己的【freecurrencyapi.net】****API Key**。**
4.  **把`xoxb-378377152752–2574471671501-pghLJ7MGiZ9KUKI8YzJQdRN2`换成自己的 **Slack Bot Key** 。**
5.  **将`G8XCG0FK5`更改为您自己的**松弛通道 Id** 。**
6.  **将`Freelancer Notifications Catcher`改成你喜欢的 **Slack bot 用户名**。**
7.  **您将需要保持**Freelancer.com 仪表板页面**打开，以便用户脚本可以继续运行。**

## **重要提示:**

**由于 Slack API 的**问题，您可能会在浏览器控制台上看到 **CORS** 错误，导致无法将项目发布到 Slack。****

**要解决这个问题，您需要关闭 web 浏览器上的 CORS 保护。为了对 Chrome 进行这样的操作，您可以创建一个到**Chrome.exe**的快捷方式，并通过添加以下参数来修改**目标****

> **—disable-we b-security-User-Data-dir = " C:\ Users \ { your username } \ AppData \ Local \ Google \ Chrome \ User Data \ "**

**![](img/ebd80fe557655cd41368225316f9b99c.png)**

**Image by [Ahmed Tarek](https://medium.com/@eng_ahmed.tarek)**

**![](img/892aaa7e75a86cea0643762ecffa1ba9.png)**

**Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)**

# **编码时间**

**在下一节中，我们将把整个代码分成更小的部分，并解释每一部分。这不仅是关于编写最终能够工作的代码，也是关于一些最佳实践和设计决策。**

**这将帮助你理解代码，并可能学习新的技能。因此，系好安全带，准备上路吧。**

**![](img/07c95f5084a90358f26fb913dc1311e4.png)**

**Image by [StartupStockPhotos](https://pixabay.com/users/startupstockphotos-690514/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=849812) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=849812)**

# **用户脚本实现**

## **页眉**

**这里需要注意的重要事项是:**

1.  **用户脚本被设置为仅在[http://www.freelancer.com/dashboard](http://www.freelancer.com/dashboard)页面上有效。这是为了不要在任何自由职业者页面打开的时候给你的空闲频道发送垃圾信息。**
2.  **用户脚本需要加载`jquery-3.3.1.min.js`库。**

## **自由职业者项目**

**这里需要注意的重要事项是:**

1.  **是定义包含自由职业者项目所有信息的对象的类。**
2.  **它还实现了`isEqual`功能，能够比较两个实例，并决定它们是否完全相同。**
3.  **这是一个最佳实践，因为现在所有关于`FreelancerProject`内部属性的逻辑和知识都被封装并隔离在`FreelancerProject`内部。**
4.  **因此，每当出现与如何比较两个项目相关的变更时，我们只有一个地方需要变更。**

## **货币转换器**

**这里需要注意的重要事项是:**

1.  **`CurrencyConverter`是一种货币兑换服务。**
2.  **它基于 freecurrencyapi.net[](http://freecurrencyapi.net)**提供的转换器 API。****
3.  ****你需要去那里，创建一个免费账户，并获得你的 API 密匙来使用它。****
4.  ****API 将一种货币作为输入，然后返回该特定货币与数组中所有其他货币之间的兑换率。****
5.  ****`CurrencyConverter`缓存从 API 返回的每种输入货币的结果。每当缓存中存在货币及其相应的兑换率时，`CurrencyConverter`将返回缓存的值，否则，将执行一个新的 API 调用，然后将响应保存到缓存中。****
6.  ****默认情况下，缓存每 12 小时失效一次，除非在调用`new CurrencyConverter(apiKey, cachingSpanInMilliseconds)`时通过为参数`cachingSpanInMilliseconds`传递另一个值来覆盖它。****
7.  ****缓存保存在页面内存中，这意味着如果您刷新自由职业者仪表板页面，缓存将被清除。****

## ****懒鬼****

****这里需要注意的重要事项是:****

1.  ****`Slacker`是一个封装了 **Slack** API 的服务。****
2.  ****你需要创建你自己的免费 **Slack** 账户，创建你自己的**频道**，定义一个应用程序并获得你的 API 令牌。您可以使用 Slack 在线文档找到所有信息和步骤。****
3.  ****然后，您应该有一个 **Slack Bot 密钥**和一个**通道 Id** 。****
4.  ****`Slacker`有一个`slackIt`函数，它接受一个`freelancerProject`对象作为参数，然后执行适当的 Slack API 调用，将消息发送到您的通道。****
5.  ****关于如何使用**Slack API**的任何细节可以在 [Slack API 页面](https://api.slack.com/)上找到。****

## ****拳击手****

****这里需要注意的重要事项是:****

1.  ****`Scrapper`该服务负责从 HTML 通知卡中删除/检索关于自由职业者项目的信息。****
2.  ****`Scrapper`依赖于`CurrencyConverter`,因为如果需要的话，它会用它将项目预算转换成您喜欢的货币。****
3.  ****然而，`CurrencyConverter`是通过其构造函数注入到`Scrapper`中的，而不是使用全局实例。****
4.  ****这里使用 JavaScript 承诺超时技术来避免永远等待承诺的实现。如果你对这个话题感兴趣，可以在我的故事 [**如何设置 JavaScript 承诺超时**](/how-to-set-javascript-promise-timeout-7d51c87bc38e) 上了解更多。****

****[](/how-to-set-javascript-promise-timeout-7d51c87bc38e) [## 如何设置 JavaScript 承诺超时

### 只是不要永远等待承诺的实现，你需要设定自己的条件。

javascript.plainenglish.io](/how-to-set-javascript-promise-timeout-7d51c87bc38e)**** 

## ****排队管理程序****

****这里需要注意的重要事项是:****

1.  ****当一个项目信息被废弃并准备发布到你的松弛渠道时，这并不是直接发生的。首先，项目信息被放入一个队列中，然后另一个服务负责从队列中出列并发送到您的 Slack 通道。****
2.  ****这是一个最佳实践，因为它将模块报废项目信息与发布到闲置渠道的其他模块信息分离开来。****
3.  ****这最大限度地降低了单点故障的可能性。****
4.  ****`QueueManager`该服务负责从队列中出列并发布到您的 Slack 通道。****
5.  ****`QueueManager`依赖于`Slacker`,因为它使用它将项目信息发布到您的 Slack 频道。****
6.  ****然而，`Slacker`是通过其构造函数注入到`QueueManager`中的，而不是使用全局实例。****

## ****自由职业者项目评估员****

****这里需要注意的重要事项是:****

1.  ****`FreelancerProjectEvaluator`该服务负责评估你是否对某个自由职业者项目感兴趣。****
2.  ****评估是基于您填写并传递给`FreelancerProjectEvaluator`构造函数的技能数组来完成的。****
3.  ****数组中的技能应该完全按照 Freelancer.com 的定义来填充。****

## ****自由职业者通知观察者****

****这里需要注意的重要事项是:****

1.  ****`FreelancerNotificationsWatcher`该服务是负责监测任何项目通知的自由职业者仪表板页面。****
2.  ****`FreelancerNotificationsWatcher`依赖于`Scrapper`、`FreelancerProjectEvaluator`和`QueueManager`。****
3.  ****`Scrapper`用于从 HTML 通知中删除项目信息。****
4.  ****`FreelancerProjectEvaluator`用于评估是否应该通知您新项目。****
5.  ****`QueueManager`用于根据需要对新项目信息进行排队。****
6.  ****依赖项通过其构造函数注入到`FreelancerNotificationsWatcher`中，而不是使用全局实例。****

## ****公用事业****

****这里需要注意的重要事项是:****

1.  ****`replaceRecurively`是本地`String`类的扩展，支持以递归方式用一个字符串替换另一个字符串。****
2.  ****`trimStart`是本地`String`类的扩展，支持以递归方式从前端移除字符串。****
3.  ****`removeCurrencySymbolsPrefix`是本机`String`类的扩展，用于从前端移除货币符号。****
4.  ****`getWordsFromString`是一个将字符串拆分成单词的函数。****
5.  ****`wait`是等待一定时间后解析`Promise`的功能。****

## ****初始化****

****这里需要注意的重要事项是:****

1.  ****`const preferredCurrency = “EUR”;`将首选货币设置为“欧元”。根据你自己的喜好改变它。****
2.  ****设置你感兴趣的自由职业者技能。根据你自己的喜好改变它。****
3.  ****`const currencyConverter = new CurrencyConverter(“lk6f7fd0–277z-12ec-8894–41n9e18q3291”, 43200000);`初始化`CurrencyConverter`的实例，并将缓存间隔设置为 12 小时(432，000，00 毫秒)。您需要将 API 密钥更改为您从[**freecurrencyapi.net**](http://freecurrencyapi.net)获得的密钥。****
4.  ****`const slacker = new Slacker(“xoxb-378377152752–2574471671501-pghLJ7MGiZ9KUKI8YzJQdRN2”, “G8XCG0FK5”, “Freelancer Notifications Catcher”, preferredCurrency);`初始化`slacker`的一个实例。您需要将 Slack Bot 密钥和频道 Id 更改为您从 **Slack** 中获得的密钥和频道 Id。****
5.  ****`const queueManager = new QueueManager(slacker, 5000);`初始化`QueueManager`的实例，并将观察间隔设置为 5 秒(5000 毫秒)。****
6.  ****`const scrapper = new Scrapper(currencyConverter, preferredCurrency);`初始化`Scrapper`的一个实例。****
7.  ****`const freelancerProjectEvaluator = new FreelancerProjectEvaluator(freelancerSkillsToWatch);`初始化`FreelancerProjectEvaluator`的一个实例。****
8.  ****`const freelancerNotificationsWatcher = new FreelancerNotificationsWatcher(scrapper, freelancerProjectEvaluator, queueManager, 2000);`初始化`FreelancerNotificationsWatcher`的实例，并将观察间隔设置为 2 秒(2000 毫秒)。****

## ****运行用户脚本****

****这是我们触发`FreelancerNotificationsWatcher`和`QueueManager`开始工作的地方。****

# ****希望这些内容对你有用。如果您想支持:****

****如果您还不是**中介**的会员，您可以使用 [**我的推荐链接**](https://medium.com/@eng_ahmed.tarek/membership) ，这样我可以从**中介**那里获得您的一部分费用，您无需支付任何额外费用。订阅 [**我的简讯**](https://medium.com/subscribe/@eng_ahmed.tarek) 将最佳实践、教程、提示、技巧和许多其他很酷的东西直接发送到您的收件箱。****

# ****其他资源****

****这些是您可能感兴趣的其他资源。****

****[](/how-to-set-javascript-promise-timeout-7d51c87bc38e) [## 如何设置 JavaScript 承诺超时

### 只是不要永远等待承诺的实现，你需要设定自己的条件。

javascript.plainenglish.io](/how-to-set-javascript-promise-timeout-7d51c87bc38e) [](/how-to-use-observables-with-vanilla-javascript-aca40a7590ff) [## 如何在普通 JavaScript 中使用 Observables

### 没有使用框架，只是纯香草 JavaScript。

javascript.plainenglish.io](/how-to-use-observables-with-vanilla-javascript-aca40a7590ff) [](/how-to-customize-webpages-ui-behavior-using-javascript-userscripts-7b6a090e0135) [## 使用 JavaScript 用户脚本定制网页用户界面/行为

### 即使你不拥有这个网页，你仍然可以附上你的 JavaScript 用户脚本。

javascript.plainenglish.io](/how-to-customize-webpages-ui-behavior-using-javascript-userscripts-7b6a090e0135) [](https://betterprogramming.pub/twitter-auto-retweet-bot-with-node-js-and-typescript-4d6eaf24c0ab) [## 用 Node.js 和 TypeScript 构建一个 Twitter 自动转发机器人

### 了解如何创建一个 Twitter 机器人来转发任何带有特定关键字或标签的推文

better 编程. pub](https://betterprogramming.pub/twitter-auto-retweet-bot-with-node-js-and-typescript-4d6eaf24c0ab) [](https://levelup.gitconnected.com/paging-partitioning-main-equations-to-make-it-easy-44fe89d5290b) [## 分页/分区—简化这一过程的主要等式

### 最后，这是您理解分页/分区主要等式并学习如何在代码中应用它们的机会。

levelup.gitconnected.com](https://levelup.gitconnected.com/paging-partitioning-main-equations-to-make-it-easy-44fe89d5290b) 

最后，希望你觉得读这个故事和我写它一样有趣。

*更多内容看*[***plain English . io***](http://plainenglish.io/)****