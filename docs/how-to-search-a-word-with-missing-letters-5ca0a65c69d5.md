# 如何搜索缺少字母的单词

> 原文：<https://javascript.plainenglish.io/how-to-search-a-word-with-missing-letters-5ca0a65c69d5?source=collection_archive---------8----------------------->

![](img/22f562fb1b6aa171ffa3b90652c7d447.png)

Photo by [Hannes Wolf](https://unsplash.com/@hannes_wolf?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@hannes_wolf?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

出了点问题，精灵们制造了一点混乱。一些礼物被扔进了雪里，名字标签也被毁了。幸运的是，名字的大部分字母都是可见的。圣诞老人确信整个名字可以从碎片开始重建。

# 谜题:匹配礼物名称🎁

![](img/5a11cf46dd89079c6a7a98a2faadeaef.png)

今天的问题是 [Dev 降临节日历的第 7 期🎅](https://github.com/devadvent/puzzle-7)很快。但是它要求你使用**正则表达式**。我仍然在努力处理 JavaScript 的这一方面——我发现即使像这样简单的问题也很难。

我从解决方案开始:

第一步是尝试正则表达式的各种组合，看看哪一种最适合这个问题。为此，我使用 [regex101](https://regex101.com/) 并进行一些手动测试。确定正确的规则后，我创建正则表达式。

有两种方法。我目前使用的是这样的:

它通常是最佳解决方案，因为它是最高效的。但是，它假设您总是使用相同的规则。今天的情况并非如此。我需要为每个要检查的名字创建不同的正则表达式。因此，我使用:

当然，这段代码只有在我想搜索单词`hello`时才有效。

首先，我用`.`字符替换`#`字符。为什么？因为正则表达式中的句点表示任何单个字符。这样我可以将`h#ello`转换成字符串`h.ello`。那我下一步就用`h.ello`了。

下一步根据数据的来源进行更改。在我们的例子中，每个名字都是一个单词。因此，我可以假设比较发生在完整的字符串之间。所以我添加了两个命令:

*   `^`表示模式在字符串的开头
*   `$`表示模式的最后一个字符之后没有任何内容。

这样我确保`patt.`只返回`patty`和`patti`而不是`patterson`。

找到要使用的正则表达式后，剩下的工作就是使用它。问题是，我不会用[regexp . prototype . test()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test)。`test()`总是从找到的最后一个索引重新开始搜索。这会产生 bug:如果没有代码测试，我会很难发现这个问题。

因此我决定使用[string . prototype . search()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/search):这个方法总是从位置 0 开始搜索，这正是我所需要的。

就这样

如果你对[很好奇🎅开发降临节日历](https://github.com/devadvent/readme)然后您可以点击以下链接:

[](https://betterprogramming.pub/which-is-the-best-method-to-find-an-item-in-an-array-of-arrays-in-javascript-5f51589d2086) [## 在 JavaScript 中，在数组的数组中查找项目的最佳方法是什么？

### 比较三种方法

better 编程. pub](https://betterprogramming.pub/which-is-the-best-method-to-find-an-item-in-an-array-of-arrays-in-javascript-5f51589d2086) [](/how-to-get-unique-values-from-a-list-in-javascript-301675602985) [## 如何在 JavaScript 中从列表中获取唯一值

### 最后，小精灵们把他们的商业野心放在一边，回到他们的工作上:帮助圣诞老人给…

javascript.plainenglish.io](/how-to-get-unique-values-from-a-list-in-javascript-301675602985) [](https://el3um4s.medium.com/how-to-find-the-sum-of-an-array-of-objects-in-javascript-24965d883bd0) [## 如何在 JavaScript 中找到一个对象数组的和

### 小精灵们准备了很多礼物，包了很多糖果。但是只有好孩子才会收到礼物。其他人会…

el3um4s.medium.com](https://el3um4s.medium.com/how-to-find-the-sum-of-an-array-of-objects-in-javascript-24965d883bd0) 

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2021 年 12 月 8 日 https://blog.stranianelli.com*[](https://blog.stranianelli.com/how-to-search-a-word-with-missing-letters/)**。**

**更多内容请看**[***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。******