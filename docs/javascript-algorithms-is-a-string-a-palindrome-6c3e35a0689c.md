# JavaScript 算法:字符串是回文吗？

> 原文：<https://javascript.plainenglish.io/javascript-algorithms-is-a-string-a-palindrome-6c3e35a0689c?source=collection_archive---------22----------------------->

## 日常 JavaScript 技巧、窍门和最佳实践

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我为日常前端开发创建了一些技巧。

![](img/8c7cb6270a4443876692221f49281169.png)

Photo by [engin akyurt](https://unsplash.com/@enginakyurt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这里，我将带来一篇新文章，介绍一些基于属性值对数组进行排序的方法。这些技巧可以成为你 2021 年 JavaScript 编码面试中的一块小石头。

> 我知道小石头没什么区别，但如果我们有成千上万的石头，就有区别了。为此我明天会带来新的石头。敬请期待

> *让我们开始今天的话题*

给定一个字符串`s`，判断它是否是回文，只考虑字母数字字符，忽略大小写。

**例 1:**

```
**Input:** s = "A man, a plan, a canal: Panama"
**Output:** true
**Explanation:** "amanaplanacanalpanama" is a palindrome.
```

**例二:**

```
**Input:** s = "race a car"
**Output:** false
**Explanation:** "raceacar" is not a palindrome.
```

## 1.我们可以使用 while 循环遍历整个字符串，比较两者是否匹配？如果不匹配，它将发送 false。

## 2.我们也可以使用数组的反转函数进行迭代，这样看起来会更干净。

# 你可以在这里查看我以前的文章:

*更多内容请看*[***plain English . io***](http://plainenglish.io/)