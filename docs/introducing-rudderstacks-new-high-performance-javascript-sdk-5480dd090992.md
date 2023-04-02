# 介绍 RudderStack 新的高性能 JavaScript SDK

> 原文：<https://javascript.plainenglish.io/introducing-rudderstacks-new-high-performance-javascript-sdk-5480dd090992?source=collection_archive---------10----------------------->

![](img/4f41f24828b6ec596d444b79e652e5e0.png)

大多数企业花费大量的时间和金钱来开发他们的网站，这是有充分理由的。网站是现代消费者和买家与企业互动和建立关系的方式。因此，工程团队承受着确保他们的网站始终以最佳状态运行的巨大压力。为了帮助提高页面速度和一般页面性能，我们很高兴地宣布我们的 RudderStack JavaScript SDK 的最新版本。

# 新的 RudderStack JavaScript SDK

任何公司对潜在客户的第一印象都是页面速度。在第一印象之后，网站性能指标立即成为形成客户意见的中心，包括渲染时间、互动时间、DNS 查找速度等等。在过去，工程师们面临着一个困难的选择，是优先考虑页面性能高于一切，还是在他们的网站上实现工具来帮助满足业务需求。

RudderStack 的 JavaScript SDK 的最新版本解决了这个问题，使快速性能和为各种工具收集客户数据成为可能。我们的 JavaScript SDK 利用 rudder-analytics.js 库跟踪用户事件并将其从您的网站发送到 RudderStack，而不会影响网站性能。然后，您可以进一步转换该事件数据，并将其路由到您选择的目标平台。

不要只相信我的话。让我们深入了解一下指标。我们的基准测试显示，通过各种优化，性能提高了近 3 倍。我们减少了 70%的包装尺寸和 60%的加载时间。测试还显示 Lighthouse 的性能分数提高了 10-30 分，在许多情况下减少了⅔对 JavaScript 的惩罚。

性能有所提高，但锦上添花的是，SDK 仍将这些数据实时路由到 Snowflake、亚马逊 S3、Salesforce、Slack、Google Analytics、Customer.io 等工具。有了这些数据，我们所有的核心业务职能，从销售和营销到招聘和客户支持，都能够访问他们需要的数据，以便更好地服务于我们的客户和不断增长的业务。

# 开发者体验

我们的 JavaScript SDK 使工程团队向任何目的地发送事件数据变得极其简单，而不必每次都实施新的 API。我们支持各种 JavaScript SDK APIs，包括加载、识别、分页、跟踪、别名、分组和重置。

我们还允许开发人员筛选发送事件数据的选择性目的地。通过过滤掉其余的数据，您可以将您的事件数据仅发送到几个预定的目的地。可以通过在 identify()、page()和 track()方法的 options 参数中传递 integrations 对象来实现这一点。我们支持超过 150 个目的地，从 Salesforce 和 Slack 到 Redshift 和 BigQuery。

# 方向舵栈中的语境和特征

RudderStack 为开发人员提供了根据事件类型自动捕获特定于事件和特定于用户的数据的选项。上下文和特征字典可以包含在 options 参数中，该参数包含在 identify()、page()和 track()方法中。上下文是关于特定数据的附加信息的字典，例如用户的 IP 地址。特征是包含在上下文中的可选字典，它指定用户的独特特征。这是一个非常有用的字段，用于将用户信息从之前进行的 identify()调用链接到 track()或 page()事件。

# 检测广告阻止的页面

RudderStack 的新 JavaScript SDK 还提供了一种发送页面视图的方法，该视图包含页面是否被广告屏蔽的相关标记。您可以分析这些数据，找出受广告拦截器影响的网站页面浏览量的百分比。

# 免费注册并在您的网站上安装我们的 JavaScript SDK

要将 RudderStack JavaScript SDK 与您的网站集成，您可以将代码片段的缩小版或非缩小版放在网站的部分。此外，我们有一个 NPM 模型，将方向舵堆栈直接打包到您的产品中。更多信息，您可以查看我们的[版本迁移指南](https://rudderstack.com/docs/stream-sources/rudderstack-sdk-integration-guides/rudderstack-javascript-sdk/version-migration-guide/)。

*通过* [*注册我们的免费试用*](https://app.rudderstack.com/signup?type=freetrial/) *，今天就开始使用舵栈。*

*本博客最初发布于:* [*https://rudder stack . com/blog/rudder stacks-new-high-performance-JavaScript-SDK/*](https://rudderstack.com/blog/rudderstacks-new-high-performance-javascript-sdk/)

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***