# 求解 LeetCode 的“给定长度的子串中元音的最大数量”

> 原文：<https://javascript.plainenglish.io/solving-leetcodes-maximum-number-of-vowels-in-a-substring-of-given-length-8ac89b663fe?source=collection_archive---------12----------------------->

![](img/7290bfdaedeab6e5373a7980ea9b8a2d.png)

Photo by [Amador Loureiro](https://unsplash.com/@amadorloureiroblanco?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本文中，我们将在 JavaScript 中求解 LeetCode 在给定长度的子串中的最大元音数。这个问题使用了滑动窗口技术。有两种类型的滑动窗口。这个问题使用的技术是一个固定的窗口长度 k。我们移动窗口来寻找窗口中的特定内容，例如窗口中的最大数量。另一种技术涉及 2 个指针(通常是字符串/数组的索引),表示窗口边上的 2 条边。起始索引在左边缘，结束索引在右边缘。在起始和结束索引范围内捕获的数组元素将用于计算结果。我们可以根据需要扩大或缩小数组的大小。在每种技术中，窗口从数组的开头开始，滑动到末尾，扫描所有元素。因此得名，推拉窗。

# 问题

给定字符串 s 和整数 k。

返回长度为 k 的 s 的任意子串中元音字母的最大数量。

英语中的元音字母是(a，e，I，o，u)。

# 例子

```
**Input:** s = "abciiidef", k = 3**Output:** 3**Explanation:** The substring "iii" contains 3 vowel letters.
```

# 解决办法

# 说明

我们第一次通过我们的 for 循环(`s[i]` = `“a”`)，我们的第二个 if 语句为真:`“a”`包含在我们的`vowels`字符串中。我们的`count`变量增加，我们的`result`变量被重新分配给`count`。`“b”`和`“c”`不是元音并且`i`仍然小于`k`，所以什么都不会发生。我们的下一个循环(`s[i]` = `“i”`)的索引为 3，等于`k` ( `k` = 3)。我们的 if 语句为真(`i >= k`)，其内部 if 语句`vowels.includes(s[i — k])`为真(`s[i — k]` = `“a”`)。我们正在右移窗口，所以`“a”`不再在窗口中，我们减少了`count`。我们下一个 if 语句为真，`“i”`是元音。我们将它添加到我们的`count`中，我们的`result`保持不变。

下一个循环是另一个索引为 4 的`“i”`，所以我们进入第一个 if 语句。这次，`s[i — k]`等于不是元音的`“b”`，所以我们不减`count`。`“i”`是一个元音，所以我们把它加到`count`上，而`result`被重新分配为 2。对于我们的下一个`“i”`(索引为 5)，我们再次遵循相同的模式，我们的`count`和`result`现在等于 3。我们现在可以返回我们的结果，而不需要完成我们的 for 循环，因为 3 是我们窗口中可能的最大元音数(`k` = 3)。

## 资源

LeetCode 问题:[https://leet code . com/problems/maximum-number-of-a-substring-of-given-length/](https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/)

[](https://zengruiwang.medium.com/sliding-window-technique-360d840d5740) [## 滑动窗口技术

### 滑动窗口技术对于解决数组或字符串中的问题是有用的，特别是它被认为是一种

zengruiwang.medium.com](https://zengruiwang.medium.com/sliding-window-technique-360d840d5740) [](https://medium.com/swlh/sliding-window-a-common-technique-for-solving-algorithmic-problems-involving-string-array-44adf35e2d5d) [## 滑动窗口——解决涉及字符串/数组的算法问题的常用技术

### 我最近在尝试解决一些涉及数组的算法问题时，偶然发现了滑动窗口技术…

medium.com](https://medium.com/swlh/sliding-window-a-common-technique-for-solving-algorithmic-problems-involving-string-array-44adf35e2d5d) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)