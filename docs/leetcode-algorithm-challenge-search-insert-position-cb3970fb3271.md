# 如何解决 LeetCode 算法的挑战:搜索插入位置

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-challenge-search-insert-position-cb3970fb3271?source=collection_archive---------11----------------------->

![](img/ea2952d82539babe3cfad34023154459.png)

# LeetCode 算法挑战:搜索插入位置

# 问题

给定一个不同整数的排序数组和一个目标值，如果找到目标，则返回索引。如果没有，返回按顺序插入时的索引位置。

**实施例 1:**

**输入:** nums = [1，3，5，6]，target = 5

**产量:** 2

**实施例 2:**

**输入:** nums = [1，3，5，6]，target = 2

**输出:** 1

**实施例 3:**

**输入:** nums = [1，3，5，6]，target = 7

**输出:** 4

# 挑战

这个任务看起来很简单，乍一看，它可以通过 indexOf 方法来解决。但这种情况让它变得更加棘手——“如果找不到目标，请将索引返回到按顺序插入时的位置。”

让我们把它分解一下。

1.  将 nums 阵列的每个元素与目标进行比较
2.  如果匹配，则返回匹配元素的索引
3.  如果元素不匹配，检查下一个元素是否小于目标，如果不匹配，则返回下一个索引位置。
4.  检查是否到达数组的末尾并返回位置

# 让我们编码

对于设置，我将需要 2 个变量:

位置—数组元素的位置、索引

结果—记录最终结果

```
let pos = 0;let result = 0;
```

现在让我们检查是否需要深入我们的数组，因为如果数组的第一个元素比目标元素多，那么目标元素的索引应该是 0。所以我们检查它并返回结果 0。

```
if (nums[0]<target) { //* further calculations will be here}return result;
```

是时候构建我们的递归函数了，不知何故，我一直在使用它们。我的 find 函数将接受 3 个参数:

1.  nums —原始阵列
2.  目标—原始目标
3.  pos —数组元素的索引/位置

将 if 语句与以下步骤结合使用。首先，我们将数组的元素与目标进行比较。如果我们找到了匹配项，我们的结果应该等于当前 pos。

```
if (nums[pos]===target) { result = pos;}
```

否则，我将使用 else-如果有或条件。如果数组的下一个元素多于目标，这意味着目标应该占据下一个元素的位置，或者如果我们已经到达数组的末尾并且没有找到匹配的元素，那么目标应该在数组的末尾。因此，这两种情况都会产生相同的结果。

```
else if (nums[pos+1]> target || pos+1===nums.length) { result = pos+1;}
```

最后，如果以上条件都不起作用，我们将移动到数组的下一个元素，并使用更新的 pos 参数执行 find。

```
else { pos++; find(nums,target,pos)}
```

这是一个非常有趣的练习，但我找到了一个更快的解决方案。

```
var searchInsert = function(nums, target) { let newArray = […nums, target].sort((a, b) => {return a — b}) const position = newArray.indexOf(target) return position};
```

哇，那是我的想法。像 1，2，3 一样简单。

1.  通过向新阵列添加目标来创建新阵列
2.  对新创建的数组进行排序
3.  我之前提到了 indexOf 方法，现在我们可以使用它并返回结果。

# 密码

不知何故，我陷入了递归函数，但有时有更简单的解决方案。将来，我应该试着找到它，而不仅仅是构建一个递归函数。

请在以下社交网络上查看我，我很乐意收到您的来信！——[*LinkedIn*](https://www.linkedin.com/in/nick-solonyy/)*，* [*GitHub*](https://github.com/nicksolony) ， [*脸书*](https://www.facebook.com/nick.solony) *。*

[*更多内容尽在 plainenglish.io*](http://plainenglish.io/)