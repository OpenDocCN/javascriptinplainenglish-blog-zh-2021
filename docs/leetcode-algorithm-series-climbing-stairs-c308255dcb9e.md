# LeetCode 算法系列:爬楼梯

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-series-climbing-stairs-c308255dcb9e?source=collection_archive---------18----------------------->

![](img/046a092047904970ee07a9274fba76cb.png)

Photo by [Bruno Nascimento](https://unsplash.com/@bruno_nascimento?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/stairs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

你好！我带着另一个算法问题回来了。今天的问题来自 Leetcode 的顶级面试问题——轻松下*动态编程*章节。

在**爬楼梯**:

> 你正在爬楼梯。到达顶端需要`n`步。
> 
> 每次你可以爬`1`或`2`台阶。有多少种不同的方式可以让你爬上顶峰？

示例:

```
**Input:** n = 2
**Output:** 2
**Explanation:** There are two ways to climb to the top.
1\. 1 step + 1 step
2\. 2 steps**Input:** n = 3
**Output:** 3
**Explanation:** There are three ways to climb to the top.
1\. 1 step + 1 step + 1 step
2\. 1 step + 2 steps
3\. 2 steps + 1 step
```

最初，这看起来是一个相当棘手的问题，因为我必须想出一种方法来计算所有不同的爬坡可能性。我怎样才能算出在我的总数上加 1 还是加 2，直到我到达顶端？

我决定采取的第一步是制定更多的测试用例，这样我就有更多的例子可以使用。在 Leetcode 中这很容易，因为你可以测试不同的情况，它会给你预期的答案。如果你没有这个选项，那么让我们写出更多的案例。

```
input: 4
Distinct Ways:
1\. 1 + 1 + 1 + 1
2\. 1 + 1 + 2
3\. 1 + 2 + 1
4\. 2 + 1 + 1
5\. 2 + 2output --> 5input: 5
Distinct Ways:
1\. 1 + 1 + 1 + 1 + 1
2\. 1 + 1 + 1 + 2
3\. 1 + 1 + 2 + 1
4\. 1 + 2 + 1 + 1
5\. 2 + 1 + 1 + 1
6\. 1 + 2 + 2
7\. 2 + 1 + 2
8\. 2 + 1 + 1
```

因此，根据问题中提供的 2 个例子和我自己算出的 2 个例子，我得到 2 有 2 种不同的方式，3 有 3 种不同的方式，4 有 5 种不同的方式，5 有 8 种不同的方式。你开始看到一种模式出现了吗？

…

如果你说的是斐波那契数列，那你就对了！！随着我处理更多的案例，我认识到了这个模式，这帮助我更容易地解决了这个问题，因为我以前做过斐波那契数列。如果你不熟悉斐波那契数列，在这里阅读它们。本质上，它是一个序列中前两个数的和。所以我所做的就是在一个 **while** 循环中设置我的 Fibonacci 序列，并让 **while** 循环运行作为输入提供的次数。

```
var climbStairs = function(n) {
    let total = 0
    let first = 0
    let second = 1
    let i = 0

    while (i < n) {
        total = first + second
        first = second
        second = total
        i++
    }

    return total
};
```

这样做的时间复杂度是 O(n ),因为我知道我的 while 循环将根据输入(n)的值运行。在 LeetCode 上运行这个，运行时间是 **68ms** ，仅仅比提交的 **82.90%** 好。

如果你有一个不同的方法来解决这个问题，或者你是如何解决这个算法的，我很乐意听到我的代码如何改进。如果你正在与它斗争，我希望这有助于澄清它！

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