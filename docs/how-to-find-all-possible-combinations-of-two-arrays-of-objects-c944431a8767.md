# 如何找到两个对象数组的所有可能组合？

> 原文：<https://javascript.plainenglish.io/how-to-find-all-possible-combinations-of-two-arrays-of-objects-c944431a8767?source=collection_archive---------13----------------------->

![](img/97ca42653d77dedafb557a33e0235d21.png)

2021 年 [Dev 降临日日历的第二天](https://github.com/devadvent/readme)又有一个新难题要解决。圣诞老人的精灵们设法找到了在森林里迷路的驯鹿鲁道夫。回到村子里，他们需要用一杯热饮来暖身。但是精灵咖啡店的菜单让人摸不着头脑。也许我们需要帮助精灵酒保重写菜单。

# 谜题:精灵咖啡店🥤

![](img/4d7895e30f4eb01739bdfd072b58f193.png)

今天的问题是关于连接两个对象数组。这也关系到它们的排序。今天的谜题也很简单，但我必须加深我的一些知识。我还没来得及测试各种解决方案，所以不排除有更聪明的办法。但是不要再说了，让我们从拼图开始。

# 对对象数组排序:按字母顺序

我立即着手解决分类问题。为什么？因为我怀疑排序两个小数组比排序一个大得多的数组更快。所以我开始按字母顺序排列饮料清单。

在开始之前，我推荐阅读一篇来自 [JavaScript 教程的帖子:数组元素排序](https://www.javascripttutorial.net/javascript-array-sort/)。当然还有 [Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 方法的文档。

第一步是根据“name”属性直接对饮料列表进行排序。所以我根据字母表检查一个人的名字是否在另一个人的名字之前。

可能出现的第一个问题是关于大写字母和小写字母的区别。如果我们人类不难理解 JavaScript 存在一些问题的话。因此，将所有名称转换为大写(或小写)字母很方便。

好吧，但是这样我会改变菜单本身。在那之后，将很难得到名字写正确的菜单。为了解决这个问题，我没有直接修改数组，而是复制了一些变量的名称:

还有一个问题:`sort()`方法直接修改了原数组的顺序。就我个人而言，我更喜欢保持一切不变。我听从拉蒙·巴尔萨扎的建议:使用 T2。这样我得到了一个新的数组，而没有改变原来的数组:

# 对对象数组排序:数字顺序

在你整理好你的饮料后，是时候开始品尝不同的定制口味了。我本能地想到使用类似的函数，用`price`属性替换`name`属性:

然而，有一个特殊的情况是从这个成分列表中遗漏的:没有额外味道的饮料。

我认为处理这种情况的最快方法是将价格`0`的“风味:未定义”添加到列表中。我用 [unshift()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) 方法将它添加到排序列表的开头

# 在菜单上混合饮料和口味

现在我有了两个排序后的数组(`sortedDrinks`和`sortedFlavors`)，我可以开始组合配料和口味了。我可以使用两个嵌套的 for 循环。或者使用 [map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 方法:

但是有一个问题:结果是一个数组包含几个数组，每种饮料一个。这个难题需要一个这样的数组:

我可以使用`flat()`或[array . prototype . flat map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap)方法:

嗯，圣诞老人的小精灵可以满足了。通过这个解决方案，他们最终可以从一个方便的菜单中点他们想要的东西。现在该是我喝一杯热腾腾的凉茶的时候了。

那些对迷失在森林里的驯鹿鲁道夫的故事感兴趣的人，可以阅读我在 Dev 降临节日历上的第一篇帖子:

[](https://betterprogramming.pub/which-is-the-best-method-to-find-an-item-in-an-array-of-arrays-in-javascript-5f51589d2086) [## 在 JavaScript 中，在数组的数组中查找项目的最佳方法是什么？

### 比较三种方法

better 编程. pub](https://betterprogramming.pub/which-is-the-best-method-to-find-an-item-in-an-array-of-arrays-in-javascript-5f51589d2086) 

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2021 年 12 月 3 日*[*https://blog.stranianelli.com*](https://blog.stranianelli.com/how-to-find-all-possible-combinations-of-two-arrays-of-objects/)*。*

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****