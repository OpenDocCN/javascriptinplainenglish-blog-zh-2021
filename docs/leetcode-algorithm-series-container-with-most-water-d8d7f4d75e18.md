# LeetCode 算法系列:盛水最多的容器

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-series-container-with-most-water-d8d7f4d75e18?source=collection_archive---------13----------------------->

![](img/27dc9f13823b3157125042221cce18d1.png)

Photo by [Irvan Smith](https://unsplash.com/@mr_vero?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/coder?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

如果你一直在关注这个系列，我只想对你的阅读表示感谢，希望你会发现它很有帮助！

今天的问题可以在 LeetCode 上找到——中等难度。

在**盛水最多的容器中:**

> 给定`n`个非负整数`a1, a2, ..., an`，其中每个代表坐标`(i, ai)`上的一个点。`n`画垂直线，使线`i`的两个端点在`(i, ai)`和`(i, 0)`。找出两条线，它们和 x 轴一起形成一个容器，这样容器中的水最多。
> 
> **注意**不要倾斜容器。

示例:

![](img/154cfef410ef22b1435647fc8814e636.png)

```
**Input:** height = [1,8,6,2,5,4,8,3,7]
**Output:** 49
**Explanation:** The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

看一下这个例子，我们可以看到在 **Height** 数组中，每个值都是容器的高度，每个值的索引都用来计算宽度。例子中需要注意的另一点是，即使一边的高度大于另一边，你也只取较小一边的高度。最后，我们要确保我们最大限度地扩大面积。在上面的例子中，你可能会问，等等，为什么高度为 8 的两个点不是最大的？如果我们看那两个点，(1，8) & (6，8)，高度是 8，宽度是 5，也就是说面积是 40。将其与(1，8) & (8，7)进行比较，其中高度为 7，宽度为 7，面积为 49。

所以我们必须想办法找到最大的高度和宽度。此外，我们可能希望比较面积，因此我们至少需要跟踪找到的最大面积。为了解决这个问题，我采用了两点法。通过这样做，每个指针都是我的容器的一面。我可以抓住那个区域，看看它是否比我之前的最大面积大。因为我已经开始在最宽的宽度，我将不得不检查较小宽度的集装箱。因为我知道我的宽度会变小，所以我想确保我总是保持最大的高度，以最大化我找到最大区域的机会。所以在比较了高度之后，无论我的两个高度哪个更低，我都会向上或向下移动一个指数。

所有这些逻辑我决定放在一个 **while 循环中。**我使用 while 循环代替循环的**,因为循环**的**只朝一个方向，使用 2 指针设置会影响两个数字。然而，我只想一次改变 1 个索引，因此一个 **while 循环**为我提供了灵活性。**

我的完整代码:

```
var maxArea = function(height) {
  let max = 0
  let w1 = 0
  let w2 = height.length-1

  while (w1 !== w2) {        
    let h = Math.min(height[w1], height[w2])
    let width = w2-w1

    if (h * width > max) {
        max = h * width
    }

    if (height[w1] < height[w2]) {
        w1++
    } else {
        w2--
    }
  }

  return max
};
```

这样做的时间复杂度是 O(n ),因为我有一个 while 循环，最多运行 N 次。在 LeetCode 上运行这个，运行时间是 **80ms** ，比提交的 **94.90%** 要好。

如果你有一个不同的方法来解决这个问题，或者你是如何解决这个算法的，我很乐意听到我的代码如何改进。如果你正在与它斗争，我希望这有助于澄清它！

请关注未来更多的 LeetCode 解决方案！

LeetCode 系列:

> 1.[包含重复的](/leetcodes-series-contains-duplicate-644f3f8a3291)
> 2。[合并排序后的数组](https://kdshah6593.medium.com/leetcode-algorithm-series-merge-sorted-array-3ec101aa3cca)
> 3。[高度检查器](https://kdshah6593.medium.com/leetcode-algorithm-series-height-checker-2cb703879529)
> 4。[有效回文](https://kdshah6593.medium.com/leetcode-algorithm-series-valid-palindrome-3cd94c4b00cc)
> 5。[快乐数字](https://kdshah6593.medium.com/leetcode-algorithm-series-happy-number-1bdea90dde7)
> 6。[最长常用前缀](https://kdshah6593.medium.com/leetcode-algorithm-series-longest-common-prefix-fc40ba439ed7)7
> 。[爬楼梯](https://kdshah6593.medium.com/leetcode-algorithm-series-climbing-stairs-c308255dcb9e)
> 8。[有效括号](https://kdshah6593.medium.com/leetcode-algorithm-series-valid-parentheses-3a379f9dceb7)
> 9。[帕斯卡三角形](https://kdshah6593.medium.com/leetcode-algorithm-series-pascals-triangle-253856454598)
> 10。[最大子阵列](https://kdshah6593.medium.com/leetcode-algorithm-series-maximum-subarray-776252f61ea0)11
> 。盛水最多的容器

*更多内容请看*[***plain English . io***](http://plainenglish.io)