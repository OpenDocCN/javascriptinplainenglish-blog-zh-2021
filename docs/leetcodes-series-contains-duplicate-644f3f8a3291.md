# LeetCode 算法系列:包含重复项

> 原文：<https://javascript.plainenglish.io/leetcodes-series-contains-duplicate-644f3f8a3291?source=collection_archive---------12----------------------->

![](img/0357a1c415bc44b74e8648ce780375f7.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你好，你好！我一边继续找工作，一边在 Leetcode 上练习我的算法题。所以，我想我会在博客上写一些我解决的 Leetcode 问题。

作为一名 Bootcamp 毕业生，我在算法方面没有得到太多的实践，所以在识别模式、优化我的代码以更快(看看你，Big-O)、学习如何分解问题，以及有时实现简洁的数学技巧来解决这些算法问题方面，这是一次非常有趣但有时令人沮丧的反复试验。我一直在用 JavaScript 练习它们。

由于我对算法问题相对较新，所以我从他们收集的最容易的面试问题开始。所以在**中包含了重复的:**

给定一个整数数组`nums`，如果任何值在数组中出现**至少两次**，则返回`true`，如果每个元素都不同，则返回`false`。

示例:

```
**Input:** nums = [1,2,3,1]
**Output:** true**Input:** nums = [1,2,3,4]
**Output:** false**Input:** nums = [1,1,1,3,3,4,3,2,4,2]
**Output:** true
```

简单来说，如果数组中的任何数字在数组中出现不止一次，我需要返回`true`。现在，我肯定需要找出一种方法来比较一个数字和其他数字。此外，我很可能需要遍历数组，这样我就可以访问每个数字，然后将其与其他数字进行比较。

首先，我认为我可以遍历数组，在每个实例中，我遍历剩余整数的另一个循环，并比较它们看是否有相等的(===)。然而，根据我对 Big-O 的初步理解，这将产生 O(n)的不利时间复杂度。

然后，我想我可以创建一个对象，并计算一个数字在数组中出现了多少次。通过这样做，我可以检查是否有任何数字的计数大于 1。如果是这样，那么我会返回`true`，否则我会返回`false`。

```
var containsDuplicate = function(nums) {
    hash = {}
    let i = 0
    while (i < nums.length) {
        if (hash[nums[i]]) {
            hash[nums[i]] += 1
        } else {
            hash[nums[i]] = 1
        }
        i++
    }
    values = Object.values(hash) for (let j = 0; j < values.length; j++){
        if (values[j] > 1) {
            return true
        }
    }
    return false
};
```

这很有效！解决了！时间复杂度是 O(2n)，比我最初的计划要快。然而，我想知道我能不能彻底解决这个问题，稍微改进一下我的 Big-O 运行时？

我意识到，当我遍历数组时，我已经创建了一个对象，当我发现任何一个数字出现不止一次时，我可以返回`true`。因此，我可以同时做这件事，而不是遍历整个数组，然后检查是否重复。当我迭代数组时，如果它不存在于我的对象中，那么我会添加它。如果它确实存在于对象中，那么我可以返回`true`并结束。最后，如果我在整个循环中没有碰到 return `true`语句，那么我将返回`false`。

```
var containsDuplicate = function(nums) {
    hash = {}
    for (let i = 0; i < nums.length; i++) {
        if (hash[nums[i]]) {
            return true
        } else {
            hash[nums[i]] = 1
        }
    }
    return false
};
```

现在，看起来好多了！并且它运行的时间复杂度相当低。我想仍然有更好更快的方法来解决这个问题，所以如果我的代码可以改进，请给我留下评论，或者教我一种新的方法来解决这个问题(我很乐意！).

如果你在解决这个问题上有任何困难，我希望这能帮助你，并在未来寻找更多的 Leetcode 解决方案！

Leetcode 系列:

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

*更多内容请看*[*plain English . io*](http://plainenglish.io/)