# LeetCode 算法系列:最长公共前缀

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-series-longest-common-prefix-fc40ba439ed7?source=collection_archive---------9----------------------->

![](img/2711b17efa18f51517433f91256d2bc6.png)

Photo by [Luca Bravo](https://unsplash.com/@lucabravo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

下面这个问题来自 Leetcode 的*顶级面试问题——轻松*下*琴弦*章节。

在**中最大的常用前缀:**

> 写一个函数在字符串数组中寻找最长的公共前缀字符串。
> 
> 如果没有公共前缀，则返回空字符串`""`。

示例:

```
**Input:** strs = ["flower","flow","flight"]
**Output:** "fl"**Input:** strs = ["dog","racecar","car"]
**Output:** ""
**Explanation:** There is no common prefix among the input strings.
```

看一下例子，我们想要找到在单词开头的相同的字母序列。如果没有共同点，那么我们返回一个空字符串。

基本上，我认为既然所有的单词都必须有相同的前缀，我可以选择任何一个单词，然后将其他单词的字母与我选择的单词进行比较

我决定在这篇文章中以不同的方式展示我的步骤。下面是我的解决方案，我在整个函数中放置了粗体注释来解释我的过程。

```
var longestCommonPrefix = function(strs) {
    **// if array is empty, return a prefix of empty string**
    if (strs.length === 0) {return ""} **// if array has 1 word, return the whole word**
    if (strs.length === 1) {return strs[0]}

    **// set a variable prefix equal to empty string**
    let prefix = "" **// iterate through the letters of the first word**
    for (let i = 0; i < strs[0].length; i++) { **// compare those letters to same Index-ed letter of other words**
        for (let j = 1; j < strs.length; j++) { **// if the letters match, continue to next set of letters;             
        // but if the letters don't match, return prefix
        // for the inside for loop (currently an empty string)**
            if (strs[j][i] === strs[0][i]) {
                continue
            } else {
                return prefix
            }
        } **// After inside for loop completes OR Breaks because the letters 
    // no longer match, the index in the first word will mark where 
    // the longest common prefix is, so we add to our empty string**
        prefix += strs[0][i]
    }

    return prefix
};
```

因为在另一个 **for 循环中运行一个 **for 循环**，所以时间复杂度为 O(n)。R** 在 LeetCode 上运行这个，运行时间是 **79ms** ，只比提交的 **59.52%** 好。然而，似乎还有一些其他因素在起作用，因为我的代码与其他提交的代码相似，但速度更快。

我很乐意听到我的代码如何改进，特别是如果它能以比 n 更好的时间复杂度完成，或者你如何着手解决这个算法。

请关注未来更多的 LeetCode 解决方案！

LeetCode 系列:

> 1.[包含重复的](/leetcodes-series-contains-duplicate-644f3f8a3291)
> 2。[合并排序后的数组](https://kdshah6593.medium.com/leetcode-algorithm-series-merge-sorted-array-3ec101aa3cca)3
> 。[高度检查器](https://kdshah6593.medium.com/leetcode-algorithm-series-height-checker-2cb703879529)
> 4。[有效回文](https://kdshah6593.medium.com/leetcode-algorithm-series-valid-palindrome-3cd94c4b00cc)
> 5。[快乐数字](https://kdshah6593.medium.com/leetcode-algorithm-series-happy-number-1bdea90dde7)
> 6。[最长常用前缀](https://kdshah6593.medium.com/leetcode-algorithm-series-longest-common-prefix-fc40ba439ed7)
> 7。[爬楼梯](https://kdshah6593.medium.com/leetcode-algorithm-series-climbing-stairs-c308255dcb9e)
> 8。[有效括号](https://kdshah6593.medium.com/leetcode-algorithm-series-valid-parentheses-3a379f9dceb7)
> 9。[帕斯卡三角形](https://kdshah6593.medium.com/leetcode-algorithm-series-pascals-triangle-253856454598)
> 10。[最大子阵列](https://kdshah6593.medium.com/leetcode-algorithm-series-maximum-subarray-776252f61ea0)

*更多内容请看*[***plain English . io***](http://plainenglish.io)