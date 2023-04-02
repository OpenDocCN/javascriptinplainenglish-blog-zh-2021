# 如何在 JavaScript 中找到一个对象数组的和

> 原文：<https://javascript.plainenglish.io/how-to-find-the-sum-of-an-array-of-objects-in-javascript-24965d883bd0?source=collection_archive---------15----------------------->

![](img/070324a84316a13d65fe1880f6d24671.png)

Photo by [Park Troopers](https://unsplash.com/@parktroopers?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/child-playing?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

小精灵们准备了很多礼物，包了很多糖果。但是只有好孩子才会收到礼物。其他人会得到煤。圣诞老人会决定。他把每个孩子做的所有动作都记录在一个旧笔记本上。然而，今年他寻求帮助来加快速度。

# 难题:列一个清单，检查两次📜

![](img/b7ad191d9ac88a1a4a87556bacdff248.png)

[开发降临节日历中的问题 6🎅](https://github.com/devadvent/puzzle-6)是关于数组以及如何根据计算值对其进行过滤。这不是一个小问题。我觉得这是很常见的情况。简而言之，它是关于将一组值减少到一个数字。

# 数组中所有元素的和

好吧，也许举个例子更好。这是一张儿童卡:

每个孩子都有一个匹配的行动列表，有些好，有些不好。每个动作对应一个值。每个动作值的总和用于计算分数:

在这种情况下，分数为正。因此，这个孩子应该得到奖励:

只要是单个元素，一切都很简单。但是如果我们有成百上千的孩子要带礼物呢？嗯，圣诞老人当然不能一直用手做所有的事情。幸运的是，有一个适合我们的方法， [Array.prototype.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

`reduce()`遍历数组的所有元素，并对每个元素执行一些操作。每个操作的结果都被添加到前一个结果中。这样我就可以计算出所有效应的总和。

# 过滤数组

问题的另一部分是第一部分的直接后果。在找到一种方法来确定一个孩子是否应该得到这份礼物后，我们可以创建两个列表。

在最初，我们只把孩子们带来的礼物交给:

相反，在第二种情况下，我们把其他人:

在这两种情况下，我都使用了 [Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) 方法从列表中只获取所需的孩子。

# 将 JSON 导入 JavaScript

最后一点。首先要做的是将孩子的列表导入程序。该列表采用`json`格式，因此需要特殊处理。有各种方法可以做到这一点。一个需要使用 [Node.js fs(文件系统)api](https://nodejs.org/api/fs.html) :

然而，这是一种繁琐的方式来做一件简单的事情。

第二种方法需要 Node.js 的一些[实验函数。为了激活它们，我必须通过添加`-experimental-json-modules`来修改`package.json`文件:](https://nodejs.medium.com/announcing-a-new-experimental-modules-1be8d2d6c2ff)

然后在`naughtyOrNice.js`文件中，我将该文件作为 JavaScript 对象导入:

它很好用，也很优雅。

以后大概就不用用`--experimental-json-modules`了。第三阶段有一个有趣的提议，[tc39/proposal-json-modules](https://github.com/tc39/proposal-json-modules)，可以让你用 JavaScript 导入 JSON 模块。在这种情况下，语法如下:

好了，今天就到这里。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮件列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2021 年 12 月 7 日 https://blog.stranianelli.com**T21*[。](https://blog.stranianelli.com/how-to-find-the-sum-of-an-array-of-objects-in-javascript/)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***