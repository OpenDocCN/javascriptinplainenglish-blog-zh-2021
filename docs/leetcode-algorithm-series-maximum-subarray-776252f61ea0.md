# LeetCode 算法系列:最大子阵列

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-series-maximum-subarray-776252f61ea0?source=collection_archive---------14----------------------->

![](img/9fd66b41f4ef2eff9d45b6935cb7160e.png)

Photo by [Joshua Sortino](https://unsplash.com/@sortino?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

今天的算法题来自 Leetcode 的顶级面试题——轻松下*动态编程*章节。

在**最大子阵列:**

> 给定一个整数数组`nums`，找到具有最大和的连续子数组(至少包含一个数),并返回其和*。*
> 
> *一个**子数组**是一个数组的**连续**部分。*

*示例:*

```
***Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]
**Output:** 6
**Explanation:** [4,-1,2,1] has the largest sum = 6.**Input:** nums = [1]
**Output:** 1**Input:** nums = [5,4,-1,7,8]
**Output:** 23*
```

*因此，强力方法是列出所有可能的连续数组，然后计算每个和，并找出最大和。所以从第一个数字开始，会有 N 个子阵列。然后移动到下一个数字，将有 N-1 个子阵列，等等。此外，我还需要得到每个子数组的总和，这太耗费时间和空间了。*

*对我来说，我相信这个算法可以通过遍历整个数组一次，以 O(N)的时间复杂度解决。在迭代时，我可以跟踪当前的和，而不是创建子数组，这样就不需要在内存中保存多个数组。每当我迭代到下一个数字时，我就把当前的总和加到它上面。如果新的和大于当前的数，那么我的子数组可以继续。如果添加下一个数字会使和减少，那么这意味着当前的数字更大，所以我希望这个数字开始我的新的子数组。这就是我如何创建和检查各种子数组的总和，而不需要实际跟踪它们。需要的额外步骤是，每当你得到一个新的和，从技术上讲，这是一个新的子阵列，你要检查，看看新的子阵列和是否大于以前的最大和。如果是，则替换该值。*

# *步骤/思考过程*

*让我们用第三个例子`*nums = [5,4,-1,7,8]*`*

*   *我将 index0 的值设置为等于一个 **max** 和 **currSum** 变量，以提供一个比较的起点。`*max = 5 currSum = 5*`*
*   *然后从 index1 开始，我使用循环的**来处理主数组中的其他数值。***
*   *我检查当前值+我的当前总和是否大于当前值。`*5 + currSum => 5 + 4 = 9 | is 9 > 4? Yes*`*

> *注意:我检查的是当前值，而不是当前总和，因为我不是从 5 和 4 开始，而是从-2 和 1 开始。总和会是-1，比我现在的总和-2 要大。然而，它小于我现在的值 1。请记住，一个数字本身仍然算作一个连续的子数组，所以我的子数组和[index1]将大于我的子数组和[index0，index1]。所以，我想用 index1 开始我的新的连续子数组。*

*   *因此，如果我的新总和大于当前值，我想把它加到 **currSum** 中。任何时候 **currSum** 发生变化，我都要检查新值是否大于我当前的 **max** sum。如果是，那么我设置一个新的最大值。*
*   *正如我在注释中提到的，如果 **currSum** 不大于当前值，那么我想用那个值开始我的新子数组(即 **currSum** )。所以我把值设为等于它。请记住，再次 **currSum** 已经更改，所以我需要检查新值是否大于我的 **max** 。如果是，那么我设置一个新的最大值。*
*   *您继续通过原始数组，直到到达末尾*

*现在让我们看看第一个例子，看看子阵列建筑是什么样子的:*

```
*nums = [-2,1,-3,4,-1,2,1,-5,4]
-----------------------
[-2]              currSum = -2 max = -2  is -2 + 1 > 1 ? NO
[1]               currSum =  1 max =  1  is 1 + -3 > -3 ? YES
[1,-3]            currSum = -2 max =  1  is -2 + 4 > 4 ? NO
[4]               currSum =  4 max =  4  is 4 + -1 > -1 ? YES
[4,-1]            currSum =  3 max =  4  is 3 + 2 > 2 ? YES
[4,-1,2]          currSum =  5 max =  5  is 5 + 1 > 1 ? YES
[4,-1,2,1]        currSum =  6 max =  6* is 6 + -5 > -5 ? YES
[4,-1,2,1,-5]     currSum =  1 max =  6  is 1 + 4 > 4 ? YES
[4,-1,2,1,-5,4]   currSum =  5 max =  6*So even though my array kept building, I had already recorded that this continuous subarray was my largest one.*
```

*以下是我完成的代码:*

```
*var maxSubArray = function(nums) {
  let max = nums[0]
  let currSum = nums[0] for (let i = 1; i < nums.length; i++) {
    let num = nums[i] if (num + currSum > num) {
      currSum += num
      if (max < currSum) {
        max = currSum
      }
    } else {
        currSum = num
        if (max < num) {
          max = num
        }
      }
  }
  return max
};*
```

*这样做的时间复杂度是 O(n ),因为我有一个循环的**。在 LeetCode 上运行这个，运行时间是 **84ms** ，比提交的 **53.10%** 要好。***

*如果你有一个不同的方法来解决这个问题，或者你是如何解决这个算法的，我很乐意听到我的代码如何改进。如果你正在与它斗争，我希望这有助于澄清它！*

*请关注未来更多的 LeetCode 解决方案！*

*LeetCode 系列:*

> *1.[包含重复的](/leetcodes-series-contains-duplicate-644f3f8a3291)
> 2。[合并排序后的数组](https://kdshah6593.medium.com/leetcode-algorithm-series-merge-sorted-array-3ec101aa3cca)3
> 。[高度检查器](https://kdshah6593.medium.com/leetcode-algorithm-series-height-checker-2cb703879529)
> 4。[有效回文](https://kdshah6593.medium.com/leetcode-algorithm-series-valid-palindrome-3cd94c4b00cc)
> 5。[快乐数字](https://kdshah6593.medium.com/leetcode-algorithm-series-happy-number-1bdea90dde7)
> 6。[最长常用前缀](https://kdshah6593.medium.com/leetcode-algorithm-series-longest-common-prefix-fc40ba439ed7)
> 7。[爬楼梯](https://kdshah6593.medium.com/leetcode-algorithm-series-climbing-stairs-c308255dcb9e)
> 8。[有效括号](https://kdshah6593.medium.com/leetcode-algorithm-series-valid-parentheses-3a379f9dceb7)
> 9。[帕斯卡三角形](https://kdshah6593.medium.com/leetcode-algorithm-series-pascals-triangle-253856454598)
> 10。[最大子阵列](https://kdshah6593.medium.com/leetcode-algorithm-series-maximum-subarray-776252f61ea0)*

**更多内容请看*[***plain English . io***](http://plainenglish.io)*