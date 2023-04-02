# 如何用无头 Chrome 和木偶师抓取 twitter 数据

> 原文：<https://javascript.plainenglish.io/how-to-scrape-twitter-data-with-depth-first-recursion-afbd437472b5?source=collection_archive---------10----------------------->

## 实时模拟用户的动作

# 用例

给定一个新闻推文 URL，我想收集每个回复、回复的回复、回复的回复的回复等的以下数据点。

```
**base_url
parent_url
comment_url
username
body
sentiment
likes_count
retweets_count
replies_count
published_datetime**
```

数据被发送到一个任意的函数 **post({…})** ，在那里它可以被保存到一个数据库或者被公开为一个服务**。**

# 分析

推文有能力作为对许多(通常是 5+)父母的回复出现，当他们只是一个父母的直系后代时。Twitter 将通过随机列出二级或三级后代来显示对话的预览，但不会没有直接后代的先前上下文。通过使用来自基本 tweet 的深度优先遍历，我们能够通过丢弃距离大于 1 级的关系来将图刮成树。每次访问一个节点时，它被存储在 visitedUrls[]中，如果该节点在未来的迭代中再次出现，它将被简单地丢弃。

## 递归

基本情况是如果 tweet 没有回复(如果从 **getSubTweetsUrls(page)** 返回的数组是 **[])。基本情况将决定你是增加还是减少一层递归。无论递归进行到多深，您都希望在方法签名中传递某些参数，例如 **base_url** 、 **parent_url** 、 **comment_url** 和 Puppeteer browser 对象(page)。**

## 提取数据

除了字段 **base_url** 、 **parent_url** 和 **comment_url** 被递归函数用来导航注释层次结构之外，其余的数据点必须从 DOM 中提取。Puppeteer 的 **$$eval** 函数提供了对页面 DOM 的访问，在这里您可以巧妙利用选择器查询来查找相关数据。有许多不同的方法可以从 DOM 中提取数据，从映射元素之间的关系到在 HTML 字符串上进行正则表达式查找。

## 履行

运行下面的脚本，查看它智能地遍历给定新闻 tweet 的评论层次结构，同时按顺序打印所需的数据点。请注意，为启动该过程而提供的基本 tweet 不会被查询数据或发布。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)