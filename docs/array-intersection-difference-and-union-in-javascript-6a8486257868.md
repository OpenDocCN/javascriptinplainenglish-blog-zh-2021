# JavaScript 中的数组交集、差集和并集

> 原文：<https://javascript.plainenglish.io/array-intersection-difference-and-union-in-javascript-6a8486257868?source=collection_archive---------3----------------------->

![](img/1d759fa9c36d5bc139594c8483ab3bd8.png)

Photo by [Pierre Bamin](https://unsplash.com/@bamin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

北极出了点问题。圣诞老人做了一个抽样检查:他发现一些礼物在袋子里不见了。幸运的是，所有的事情都被记录下来，我们可以比较不同的列表来找出不同之处。我们可以添加丢失的包。

# 谜题:找到丢失的礼物🎁

![](img/9f65e78710c8683c1a221dfb8c151983.png)

我认为 [Dev 降临节日历问题 23🎅](https://github.com/devadvent/puzzle-23)是解决方案最短的一个:字面上 2 行代码就足以解决它；

问题是"*我如何找到一个数组中的元素而不是另一个数组中的元素？*”。

# 找出两个数组之间的差异

要回答这个问题，只需结合两种数组方法:

*   Array.prototype.filter() ，返回一个新数组，其中包含通过给定测试的所有元素
*   [array . prototype . includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)，如果数组包含指定的元素，则返回值`true`

我可以推导出这个函数:

谜题的第二部分涉及返回一个对象数组，该数组取自刚刚找到的元素所在的数组。我可以这样改变函数:

我可以通过修改传递给`filter`的测试来缩短代码。另一种计算差异的方法是说元素`x`包含在`a`中，但不包含在`b`中:

# 两个阵列之间的对称差

另一个有趣的问题是如何在 JavaScript 中计算两个数组之间的对称差。基本上我想找到属于一个数组而不是另一个数组的所有元素。

前一段时间，有两个帖子对我很有用:

[](https://medium.com/@alvaro.saburido/set-theory-for-arrays-in-es6-eb2f20a61848) [## ES6 中的数组交、差、并

### 今天，我为大家带来一些 ES6 魔术，用于常见的数组算法，有时，我们想多了，他们有一个非常简单的…

medium.com](https://medium.com/@alvaro.saburido/set-theory-for-arrays-in-es6-eb2f20a61848) [](/javascript-algorithm-find-difference-between-two-arrays-ed8df86c4924) [## JavaScript 算法:找出两个数组之间的差异

### 返回一个数组的函数，该数组的元素在第一个数组中，但不在第二个数组中。

javascript.plainenglish.io](/javascript-algorithm-find-difference-between-two-arrays-ed8df86c4924) 

我可以通过依次运行两个过滤器，然后用[array . prototype . concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)方法或 [spread 操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)连接数组来找到它们:

# 两个数组的交集

另一个常见的操作是计算两个数组的交集。换句话说，我们怎样才能得到一个新的数组，包含两个起始数组中同时存在的所有元素？

再次使用`filter`方法:

用文字说，它们都是`b`中呈现的`a`的元素。

# 两个数组的并集

最后一个操作是两个数组的并集。有两种方法来定义这个操作。我们可以简单地合并两个数组，而不考虑任何重复的值:

在某些情况下，我们希望避免重复的值。在这种情况下，最好使用 [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) :它是一个 JavaScript 对象，只收集不同的值，防止我们创建重复值。

我可以把数组转换成集合，就像这样:

将集合转换为数组的反向操作很简单:

我可以用这个函数连接两个数组，而不用重复 double 值:

好吧，也许我今天的练习有点跑题了。但对我来说，这是一个回顾数组的好机会。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2021 年 12 月 24 日*[*https://blog.stranianelli.com*](https://blog.stranianelli.com/array-intersection-difference-and-union-in-javascript/)*。*

*更多内容看* [*说白了就是*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家的写作机会和建议。*