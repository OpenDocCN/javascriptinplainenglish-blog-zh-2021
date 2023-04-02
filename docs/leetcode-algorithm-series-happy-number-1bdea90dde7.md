# LeetCode 算法系列:快乐数字

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-series-happy-number-1bdea90dde7?source=collection_archive---------19----------------------->

![](img/d8e459d631b7b3ee50193af98319c632.png)

Photo by [Nick Hillier](https://unsplash.com/@nhillier?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/numbers?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

这个问题来自于 Leetcode 的*哈希表*探索卡*实际应用—哈希集*章节下。

在**快乐数字**中:

> 写一个算法，判断一个数字`n`是否快乐。
> 
> 一个**喜数**是由以下过程定义的数:
> -从任意正整数开始，用其位数的平方和代替该数。
> -重复该过程，直到数字等于 1(它将停留在该位置)，否则**在不包括 1 的周期**中无限循环。
> -该过程**以 1** 结束的那些数字是快乐的。
> 
> 返回`true` *如果* `n` *是喜数，返回* `false` *如果不是*。

示例:

```
**Input:** n = 19
**Output:** true
**Explanation:**
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```

看一下这个例子，我有一个数字，为了确定它是否快乐，我想计算这个数字平方的和，看看这个和是否等于 1。

当我开始做这个问题时，首先我必须弄清楚如何得到这个总数。既然给了我一个数字，我需要一种方法把它分解成数字。对于 JavaScript，我需要先把它变成一个字符串。在拆分返回一个数组的字符串化数字之后，我可以遍历该数组，并使用 [**将它们改回数字。地图()方法**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) 。

之后，我需要一笔款子，JavaScript 有一个方便的 [**。reduce()方法**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 可以迭代一个数组，返回 1 个聚合结果。在 reduce 方法中，我可以改变它正在迭代的当前元素，这样我就可以得到总数的平方，而不是数字。

最后，在这种情况下，将初始值设置为 0 很重要，否则 reduce 会将数组中的第一个元素作为初始值，然后它会从下一个元素开始迭代。这是一个问题，因为数组中的第一个数字永远不会被平方。

```
const a = n.toString().split("");
const b = a.map(x => parseInt(x))
const sum = b.reduce((total, x) => total + x**2, 0)
```

现在我有了一种方法来得到数字的平方和，我需要弄清楚如何重复这个过程，直到得到 1。首先，我想到了使用 while 循环，然而，只有当我已经知道这是一个令人高兴的数字时，它才会起作用。如果这不是一个令人愉快的数字，循环将无限运行。这让我们不得不使用递归。

***免责声明*** *:我是递归方面的新手，可能解释不太完美。*

基本上，使用递归，我们在函数内部调用函数并返回值。每个递归函数都需要一个基本情况，否则函数将停止运行，否则我们会再次陷入无限循环的情况。

先简单说一下，一个不快乐的数字是什么样的？

```
**Input:** n = 2
**Output:** false
**Explanation:**
0^2 + 2^2 = 04
0^2 + 4^2 = 16
1^2 + 6^2 = 37
3^2 + 7^2 = 58
5^2 + 8^2 = 89
8^2 + 9^2 = 145
1^2 + 4^2 + 5^2 = 42
4^2 + 2^2 = 20
2^2 + 0^2 = 04
```

你注意到什么了吗？第一行和最后一行是一样的！我又得到了一笔 4，我知道如果我继续用 4 的话会是什么样。所以一个不快乐的数字会无限延续下去。那么我该如何应对呢？

我决定我需要一种方法来跟踪我遇到的数字，如果我得到一个已经是我以前见过的数字的总和，我会知道我在一个不快乐的数字的循环中，我只是返回 false。

将这种跟踪+递归的方法放在一起:

```
var isHappy = function(n, hash = {}) {
    if (n !== 1) {
        if (hash[n]) {
            return false
        }
        hash[n] = 1
        const a = n.toString().split("");
        const b = a.map(x => parseInt(x))
        const sum = b.reduce((total, x) => total + x**2, 0)
        return isHappy(sum, hash)
    }
    return true
};
```

我的函数接受一个数字和一个对象。这个对象是我用来记录我看到的数字的，数字参数是我要传递的新的和。

分解我的代码:

1.  首先检查传入的数字是否等于 1。如果是，则立即返回 true。如果没有，那么我们跳转到 If 语句块
2.  如果这个数不等于 1，我们就检查我以前是否遇到过这个数。如果有，则立即返回 false。
3.  如果我没有遇到那个数字，我把它添加到我的对象中，然后使用我之前开发的代码得到我的下一个数字，数字平方的和，我生成我的新数字
4.  由于当前数字不等于 1，也不是我以前遇到过的数字，所以仍然有可能原来的数字是正确的，所以我将新数字传递给我的函数和更新后的对象(这里称为 hash)。
5.  类似于一个循环，我们再次从代码的顶部开始往下读，直到我们遇到数字等于 1 的基本情况(或者在某个时刻，我们将遇到相同的数字并退出，因为我们返回 false)

在 LeetCode 上运行这个，运行时间是**68 毫秒**，比提交的 **98.79%** 要好。

我很想知道我的代码如何改进，或者你是如何解决这个算法的。请关注未来更多的 LeetCode 解决方案！

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
> 10。[最大副拉](https://kdshah6593.medium.com/leetcode-algorithm-series-maximum-subarray-776252f61ea0)

*更多内容请看*[***plain English . io***](http://plainenglish.io)