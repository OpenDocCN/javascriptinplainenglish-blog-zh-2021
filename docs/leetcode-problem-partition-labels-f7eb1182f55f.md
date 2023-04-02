# Leetcode 问题:分区标签

> 原文：<https://javascript.plainenglish.io/leetcode-problem-partition-labels-f7eb1182f55f?source=collection_archive---------7----------------------->

## 双指针 JavaScript 解决方案演练

![](img/16d47657d00aea12f053c618a98f35b7.png)

我对自己的算法解决技巧越来越有信心。以至于我已经升级到中等难度的 Leetcode 问题。耶！我能毫不费力地解决我看到的每一个问题吗？绝对不会。我现在所处的阶段是，对于给定的问题，我通常可以提出一个可行的强力解决方案。然而，在寻找最优答案时，我通常会寻找一些提示。不过没关系！只要我在继续下一步之前花时间充分理解解决方案，我就会学到一两个新技巧，并可以将它们应用到下一个问题中。

下面就是这样一个问题:

# 分区标签问题

给出一串小写英文字母`S`。我们希望将这个字符串分割成尽可能多的部分，以便每个字母最多出现在一个部分中，并返回一个表示这些部分大小的整数列表。

## **注:**

*   `S`将具有在`[1, 500]`范围内的长度。
*   `S`将只包含小写英文字母(`'a'`到`'z'`)。

## 示例:

```
**Input:** S = "ababcbacadefegdehijhklij"
**Output:** [9,7,8]
**Explanation:** The partition is "ababcbaca", "defegde", "hijhklij".
```

# 算法

为了解决这个问题，我们将使用两点解决方案。请参见以下步骤:

## **步骤**:

1.  首先，我们为字符串中每个唯一字符的最后一个索引创建一个 hashmap。这是通过遍历字符串并存储每个字母出现的索引来实现的。如果一个字母重复出现，哈希将使用更大的索引进行更新，并且只保存最后出现的字母。
2.  接下来是两个指针部分。首先，我们将初始化我们的分区数组(这就是我们将要返回的内容)，并且初始化指向字符串开头的两个指针(将 end 和 start 设置为 0)。
3.  然后我们遍历字符串，设置结束指针。结束指针是我们所在的索引和我们所在字符的最后一个索引之间的较大值(使用 hashmap！).
4.  接下来，我们比较结束指针的位置和我们在字符串上迭代的位置。如果当前索引与结束索引不同，我们就必须继续移动，什么也不做。
5.  但是，如果 end 和 current 索引相同，那么我们一定是在一个分区的末尾。基本上，这个字符不会再出现，所以你应该在字符串中做一个剪切，以确保我们得到最大数量的分区。
6.  要进行切割，请将段的长度推入分区数组。然后，在最后一个分区结束后，我们将开始指针更新为 1。
7.  循环结束后，我们简单地返回分区数组。

# 解决方案代码

```
var partitionLabels = function(S) { let lastIndex = {} for (let i = 0; i < S.length; i++){
    lastIndex[S[i]]= i
  } let partitions = []
  let start = 0
  let end = 0 for (let i = 0; i < S.length; i++) {
    end = Math.max(end, lastIndex[S[i]])
    if (i === end) {
      partitions.push(i — start + 1)
      start = i + 1
    }
  } return partitions
}
```

# 时空复杂性

在完成时空复杂性分析之前，永远不要离开一个问题。它可以帮助触发一个信号到一个可能存在更优化方法的强力解决方案。

对于上面的解决方案代码:

**空间复杂度:O(n)** 这与我们存储每个字符的最后一个索引的步骤有关。理论上，您可以让每个字符都是唯一的，从而产生该哈希所需的 O(n)个空间。

**时间复杂度:O(n)** 循环遍历数组两次。一次是创建最后一个索引的散列，另一次是创建分区。这导致最坏情况下的时间复杂度为 2*O(n)。但是我们不关心系数，所以我们在开始时去掉了 2。

# **更多(中)问题**

在完成一个算法后，特别是一个我需要一些额外帮助的算法，我喜欢解决另一个类似的问题。寻找解决方案没有错，但是为了确保你正在学习，试着将这些技能应用到一个新的问题上。

这里有一个相关的 Leetcode 提示的问题: [**合并间隔时间**](https://leetcode.com/problems/merge-intervals/) 。试试吧！

# 参考

*   [分区标签-leet code](https://leetcode.com/problems/partition-labels/)
*   [Leetcode #763 分区标签](https://algorithmexplorer.medium.com/leetcode-763-partition-labels-33350a163019)
*   [leet code-分区标签](https://dev.to/mzakzook/leetcode-partition-labels-3dma)