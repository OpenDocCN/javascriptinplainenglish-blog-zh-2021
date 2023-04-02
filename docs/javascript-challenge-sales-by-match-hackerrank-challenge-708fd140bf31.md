# JavaScript 挑战:按匹配销售(HackerRank 挑战)

> 原文：<https://javascript.plainenglish.io/javascript-challenge-sales-by-match-hackerrank-challenge-708fd140bf31?source=collection_archive---------4----------------------->

## 了解如何解决 HackerRank 的面试准备挑战

![](img/af1f2232d2762b2f9ee591eb8f66ca0f.png)

Photo by [Vlad Sargu](https://unsplash.com/@vladsargu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这个挑战中，我们将解决 HackerRank 的销售匹配面试挑战。该挑战的难度级别为平台上标记的“简单”。

**挑战。**

有一大堆袜子必须按颜色搭配。给定一个表示每只袜子颜色的整数数组，确定有多少双颜色匹配的袜子。

**举例**

*   n=7
*   ar= [1，2，1，2，1，3，2]

有一对彩色 **1** 和一对彩色 **2** 。还剩三只袜子，每种颜色一只。对数为 **2** 。

**功能描述**

***sockMerchant*** 具有以下参数:

*   int n:袜子堆中袜子的数量
*   每只袜子的颜色

**返回**

*   int:对数

**解决问题**

在这个挑战中，我们得到了一组代表一对物品的数字。我们的解决方案应该找出一个给定数字出现的次数。如果一个数字出现在两个序列中(2 次)，我们将返回一对。如果这对出现在三个序列中，我们应该返回 1，因为只有一对。记住一对类似于两个事件。

要注意

*   给定数组的出现次数。
*   给定一对中的事件(2)返回一。

我们可以对数组中的元素进行排序，使数组按升序排列。现在我们已经对数组中的元素进行了排序。我们可以遍历数组并比较数组序列。

**写代码**

现在我们有了解决方案应该是什么样子的概述，让我们现在写同样的代码。

这个挑战的代码解决方案。

如果你想尝试挑战，请点击这里查看 [***。***](https://www.hackerrank.com/challenges/sock-merchant/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=warmup)

**结论**

谢谢你检查我的这个解决方案。希望对你有帮助。

你认为我们可以添加什么或者如何进一步重构它？

如果你觉得我的内容有用，而你不是媒体成员，你可以在这里(媒体推荐链接)获得你的媒体成员资格[，以获得对所有内容的无限制访问，并作为作者支持我们。](https://amjohnphilip.medium.com/membership)

**更读**

[](/javascript-challenge-compare-the-triplets-hackerrank-challenge-98af70c2cd5e) [## JavaScript 挑战:比较三元组(HackerRank 挑战)

### HackerRank 比较三胞胎挑战的解决方案

javascript.plainenglish.io](/javascript-challenge-compare-the-triplets-hackerrank-challenge-98af70c2cd5e) [](/how-to-configure-dependabot-in-a-nuxt-js-project-cb4d19953364) [## 如何在 Nuxt.js 项目中配置 Dependabot

### 使用 Dependabot 自动更新您的依赖项

javascript.plainenglish.io](/how-to-configure-dependabot-in-a-nuxt-js-project-cb4d19953364) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)