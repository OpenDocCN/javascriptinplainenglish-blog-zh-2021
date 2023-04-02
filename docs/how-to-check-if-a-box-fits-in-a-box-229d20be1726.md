# 如何检查一个盒子是否适合一个盒子

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-box-fits-in-a-box-229d20be1726?source=collection_archive---------3----------------------->

![](img/469c7595e155fefef35ae17f2aeb14bd.png)

Photo by [Jackie Zhao](https://unsplash.com/@jiaweizhao?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/boxes?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

小精灵们走运了:自助餐厅的业务继续增长。可惜他们把盒子搞混了。他们努力想出如何在不浪费纸板的情况下将所有货物装箱。精灵邮政服务📯(ECS)有多种格式可供选择。今天的 [Dev 降临](https://github.com/devadvent/readme)谜题就是关于这个的。

# 难题:优化航运📦

![](img/d3c8aba1fd602a69f2a0d522719466d2.png)

今天的问题与几何有关:这是一个理解一个盒子能否装进另一个盒子的问题。仅仅测量单个角的长度是不够的，还可以旋转盒子使其适合。

解决方案很简单，不需要解释:

我一直在寻找一个通用的公式，以更优雅的方式实现这一点，但我没有找到更好的方法。而且只有 3 个维度，手动公式就够了。

然而，有一件有趣的事情。我在对象析构操作期间重命名了变量。只需在原始变量的名称后添加新变量的名称:

上面的例子不是我举的，是来自[保罗·范内尔德](https://medium.com/u/db86d4f5721e?source=post_page-----229d20be1726--------------------------------)。我是在 Medium 上发表的一篇有趣的文章中发现的:

[](/7-little-known-techniques-to-improve-your-javascript-20a9e870a5fe) [## 提高 JavaScript 的 7 个鲜为人知的技巧

### 世界上最著名的编码语言的隐藏宝石

javascript.plainenglish.io](/7-little-known-techniques-to-improve-your-javascript-20a9e870a5fe) 

好了，今天就到这里。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2021 年 12 月 5 日 https://blog.stranianelli.com*[](https://blog.stranianelli.com/how-to-check-if-a-box-fits-in-a-box/)**。**

**更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****