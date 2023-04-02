# 在 JavaScript 中求解 LeetCode 的最后一石重量

> 原文：<https://javascript.plainenglish.io/solving-leetcodes-last-stone-weight-in-javascript-d4b834321004?source=collection_archive---------9----------------------->

![](img/8175ead643fb70dbbd3a34d7435d1b51.png)

Photo by [Sean Stratton](https://unsplash.com/@seanstratton?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

问题的链接是这里的和参考资料部分的[。](https://leetcode.com/problems/last-stone-weight/)

# 问题

我们收集了一些石头，每块石头的重量都是正整数。

每一回合，我们选择两块最重的石头，然后一起打碎。假设石头的重量为 x 和 y，其中 x < = y。这种粉碎的结果是:

*   如果 x == y，两块石头全毁；
*   如果 x！= y，重量 x 的石头全毁，重量 y 的石头有了新的重量 y-x。

最后最多剩下 1 石。返回这块石头的重量(如果没有剩余的石头，返回 0。)

# 示例:

```
**Input:** [2,7,4,1,8,1]**Output:** 1**Explanation:**We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,we combine 1 and 1 to get 0 so the array converts to [1] then that’s the value of last stone.
```

我们知道我们想要比较两个最重的石头，并将它们从数组中移除。

如果它们不相等，我们要减去差值，并将差值插入到数组中。我们不关心数组的顺序，因为我们总是比较两个最大的，所以我们可以把差推到最后。如果它们相等，我们就把它们从数组中移除。

我们一直这样做，直到数组的长度为 1 或 0。如果剩下一块石头，返回石头的重量。如果没有剩余的石头，返回 0。

# 解决办法

# 说明

让我们确切地解释我正在做什么。我用递归解决了这个问题。我在这里和参考资料部分有我关于递归的文章[的链接。简而言之，递归函数是一个调用自身的函数，直到该函数达到其基本情况。基本情况是我们不再需要调用函数的结束条件。我们的基本情况是数组的长度为 1 或 0。](https://medium.com/analytics-vidhya/recursion-the-nesting-doll-of-programming-404ae61708a0)

第一次调用这个函数时，我们的数组没有变化[2，7，4，1，8，1]。我们的基本情况不满意，所以我们继续前进。我们首先抓住最重的石头。

```
let heavy1 = Math.max(...stones) // 8
```

我们想从数组中移除这块石头，我们可以通过使用`splice()`方法来完成，该方法要求提供索引和要移除的元素数量。我用`indexOf()`抓取了`heavy1`的索引。

```
stones.splice(stones.indexOf(heavy1), 1) // stones = [2,7,4,1,1]
```

由于我们已经移除了最重的，我们可以再次做同样的事情来抓取并移除第二重的。

```
let heavy2 = Math.max(...stones) // 7stones.splice(stones.indexOf(heavy2), 1) // stones = [2,4,1,1]
```

我们检查`heavy1`是否大于`heavy2`。8 比 7 重，所以我们减去并推出差值。

```
if (heavy1 > heavy2) {    
  let newStone = heavy1 - heavy2 // 1
  stones.push(newStone)          // stones = [2,4,1,1,1]
}
```

我们再次调用我们的函数，但是使用我们的新数组[2，4，1，1，1]。我们一直这样做，直到我们的一个基本情况为真。在这个例子中，我们返回最后一块石头，它的权重为 1。

# 资源

*链接我的递归文章:*[https://medium . com/analytics-vid hya/recursion-the-nesting-doll-of-programming-404 AE 61708 A0](https://medium.com/analytics-vidhya/recursion-the-nesting-doll-of-programming-404ae61708a0)

*又一篇递归文章:*[https://medium . com/free-code-camp/how-recursion-works-explained-with-flow trade-and-a-video-de 61 f 40 CB 7 f 9](https://medium.com/free-code-camp/how-recursion-works-explained-with-flowcharts-and-a-video-de61f40cb7f9)

*LeetCode 问题:*[https://leetcode.com/problems/last-stone-weight/](https://leetcode.com/problems/last-stone-weight/)