# LeetCode 算法系列:高度检查器

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-series-height-checker-2cb703879529?source=collection_archive---------10----------------------->

![](img/fb1534e03bad34ccc98946bf2eb2c898.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

你好！欢迎回到另一个算法问题。这个问题实际上是建立在我之前写的算法的经验之上的。你可以在这里查看:[合并排序数组](/leetcode-algorithm-series-merge-sorted-array-3ec101aa3cca)。

这个问题来自于 LeetCode 的《数据结构导论:数组 101》。因此在**高度检查器中:**

> 一所学校正试图给所有学生拍一张年度照片。学生们被要求站成一排，按照身高的降序排列。让这个顺序由整数数组`expected`表示，其中`expected[i]`是排队的`ith`学生的预期高度。
> 
> 给你一个整数数组`heights`，表示学生所在的**当前订单**。每个`heights[i]`是队列中`ith`学生的身高(**0-索引**)。
> 
> 返回*中的* ***编号索引*** *其中* `heights[i] != expected[i]`。

示例:

```
**Input:** heights = [1,1,4,2,1,3]
**Output:** 3
**Explanation:** 
heights:  [1,1,4,2,1,3]
expected: [1,1,1,2,3,4]
Indices 2, 4, and 5 do not match.
```

分解这个问题，我们有一个没有排序的高度数组。如果我们有一个高度的排序数组，我们希望将该数组与原始数组进行比较，看看有多少索引不匹配，并返回相应的数量。

所以对我来说，这分为两个主要步骤。

1.  我需要创建一个新的高度排序数组
2.  我会遍历数组，将每个值相互比较，以计算差异。

# 第一步。创建一个排序数组

为了创建一个排序的数组，我需要依靠我用来解决我之前的算法问题的技巧。

```
let count = 0;
let expected = [...heights]for (let i = 1; i < expected.length; i++) {
        if (expected[i-1] && expected[i] < expected[i-1]) {
            let tmp = expected[i-1]
            expected[i-1] = expected[i]
            expected[i] = tmp
            i -= 2
        }
    }
```

我设置了一个计数，它将是我返回的值，也是我将在步骤 2 中处理的内容。然后，我创建了一个名为**预期为**的新数组，这样我就可以保持原来的数组不变。注意**展开操作器**的使用。您还可以使用 **slice()方法**来创建数组的副本。

> 为什么不直接设置期望等于高度数组？

JavaScript 中的数组在技术上是对象，而变量是对象的引用，而不是对象本身。因此，如果我只是设置**预期**等于**高度**数组，两个变量都引用同一个对象*。这意味着我对其中一个变量所做的任何改变都会影响到另一个变量。*

# 第二步。比较数组并计数

现在我们有了一个排序后的数组，我们需要做的就是将两个数组相互比较。因为我们现在长度是相同的，我们可以用数组长度创建一个 for 循环，或者你可以在代码的前面创建一个变量来保存数组的长度。

```
for (let j = 0; j < heights.length; j++) {
        if (heights[j] !== expected[j]) {
            count += 1
        }
    }

    return count
```

这里，只需记住我们希望知道数组中当前索引**处的元素与数组间的**不匹配的时间。然后我们只需在每次为真时将 count 变量加 1(你也可以使用 **++** 快捷键)。

这就是它的全部内容，非常简单明了！这是处理数组、循环和排序的好习惯。这样做的时间复杂度将是 O(n ),因为我正在为循环运行 2 个**。**在 LeetCode 上运行这个，运行时间是 72 **ms** ，比提交的 **91.30%** 要好。

一如既往，我很想知道我的代码是否可以进一步改进，或者你是如何解决这个算法的！

请关注未来更多的 LeetCode 解决方案！

LeetCode 系列:

> 1.[包含重复的](/leetcodes-series-contains-duplicate-644f3f8a3291)
> 2。[合并排序后的数组](https://kdshah6593.medium.com/leetcode-algorithm-series-merge-sorted-array-3ec101aa3cca)
> 3。[高度检查器](https://kdshah6593.medium.com/leetcode-algorithm-series-height-checker-2cb703879529)
> 4。[有效回文](https://kdshah6593.medium.com/leetcode-algorithm-series-valid-palindrome-3cd94c4b00cc)
> 5。[快乐数字](https://kdshah6593.medium.com/leetcode-algorithm-series-happy-number-1bdea90dde7)
> 6。[最长常用前缀](https://kdshah6593.medium.com/leetcode-algorithm-series-longest-common-prefix-fc40ba439ed7)
> 7。[爬楼梯](https://kdshah6593.medium.com/leetcode-algorithm-series-climbing-stairs-c308255dcb9e)8。[有效括号](https://kdshah6593.medium.com/leetcode-algorithm-series-valid-parentheses-3a379f9dceb7)9。[帕斯卡三角形](https://kdshah6593.medium.com/leetcode-algorithm-series-pascals-triangle-253856454598)
> 10。[最大子阵列](https://kdshah6593.medium.com/leetcode-algorithm-series-maximum-subarray-776252f61ea0)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)