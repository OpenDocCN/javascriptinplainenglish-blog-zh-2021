# LeetCode 算法系列:合并排序数组

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-series-merge-sorted-array-3ec101aa3cca?source=collection_archive---------7----------------------->

![](img/8d9ea4913a07ed8252d92af3500cdf8b.png)

Photo by [Tianyi Ma](https://unsplash.com/@tma?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

又见面了！我带着另一个算法问题和解决方案回来了。我写的第一个问题是检查数组是否包含重复项。你可以在这里查看:[包含重复](/leetcodes-series-contains-duplicate-644f3f8a3291)。只是提醒一下，我正在使用 JavaScript 解决代码。

这个问题也来源于 Leetcode 轻松收集的顶级面试问题。所以在**合并排序后的数组:**

> 给你两个整数数组`nums1`和`nums2`，按**非降序排序**，两个整数`m`和`n`，分别代表`nums1`和`nums2`中元素的个数。
> 
> **将** `nums1`和`nums2`合并成一个按**非降序排序的数组**。
> 
> 最终排序后的数组不应该被函数返回，而是被*存储在数组* `nums1`里面。为了适应这种情况，`nums1`的长度为`m + n`，其中第一个`m`元素表示应该合并的元素，最后一个`n`元素被设置为`0`并应该被忽略。`nums2`的长度为`n`。

示例:

```
**Input:** nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
**Output:** [1,2,2,3,5,6]
**Explanation:** The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
```

本质上，我有两个数组，已经从最小到最大排序。我需要通过替换第一个数组中的最后几个零，将`*nums2*`合并到我的`*nums1*`数组中。给我的是 **m** 和 **n** ，它们是每个数组中的位数。这实际上是非常重要的，因为您可能会遇到这样的测试案例，在该案例中，您需要保留数组开头的零！这可能会改变您合并阵列的方式。

将这个问题分解成几个步骤:

1.  我需要将两个数组组合在一起，用`*nums2*` 数组中的数字替换`*nums1*` 数组中的零。
2.  合并后，我需要对`*nums1*` 数组进行排序。

# 合并数组

最初，我认为如果遍历`*nums1*` 数组，我可以用`*nums2*` 数组中相应的值来替换零

```
const len = m + n
for (let i = 0; i < len; i++) {
  if (nums1[i] === 0) {
    nums1[i] = nums2[i-n]
  }
}
```

然而，还记得我在上面提到的我需要保留带有零的测试用例吗？上面的代码会产生包含`*undefined*` 值的`*nums1*` 数组。

所以我改变了合并数组的方式。由于我被赋予了 m 和 n 的值，我实际上可以用它们来删除我在 T21`*nums1*`中不需要的零。使用 **splice()** 方法，该方法接受一个从哪个索引开始拼接的参数，我**破坏性地**改变了我的`*nums1*` 数组。然后我用一个循环的**将我的`*nums2*` 值推送到我的`*nums1*` 数组中。**

```
// nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
const len = m + n
nums1.splice(len-n)for (let i = 0; i < n; i++) {
  nums1.push(nums2[i])
}
// nums1 = [1,2,3,2,5,6]
```

现在我已经成功地将我的数组合并到`nums1`*中，我需要将它们按非降序排序。*

# *对数组排序*

*是的，你总是可以使用 JavaScript 自带的 **sort()方法**，但是算法的要点是不用它就能解决问题。另外，排序的时间复杂度是 O(n log(n))。然而，我们可以在 O(n)时间复杂度内解决这个问题，这样更快。*

*那么我该如何对它们进行排序呢？我知道我需要遍历数组，然后比较两个数字。我最初的设计:*

```
*for (let j = 1; j < len; j++) {
  if (nums1[j-1] && nums1[j] < nums1[j-1]) {
    let tmp = nums1[j-1]
    nums1[j-1] = nums1[j]
    nums1[j] = tmp
    j = j-2
  }
}*
```

*这里，我遍历数组——注意，我从索引 1 开始，而不是从 0 开始——并检查数字是否小于它前面的数字。如果是，那我就改变他们的价值观。我使用一个临时变量，所以在改变它们的时候不会丢失值。现在，请注意我还没有提到的两件事。*

```
*1\. nums1[j-1]
2\. j = j-2*
```

*从第 2 点开始，我实现它来改变我在循环中的位置，否则 **j** 每次只会增加 1。如果我没有它，就会发生这样的事情:*

```
*[1,3,2,1,4,5]
// run my code
// result
[1,3,1,2,4,5]*
```

*没整理好！因为我再也没有检查那个数字是大于还是小于上一个数字。所以你可能会问，为什么不直接做 j=j-1 呢？这就是我想要的，但是由于循环，它会自动增加 1，所以我用-2 来抵消增加的值。*

*现在，第一点，为什么会在那里？想象一下当你做了一个转换后 j = 0。当程序检查 j-1 时，它不存在，因为我已经在数组的零索引处了。如果在它之前没有可以比较的东西，我可以直接移动到数组中的下一个元素。然而，我需要多走一步，因为我仍然会遇到一个错误。你能猜到吗？在 JavaScript 中，0 的真值是多少？是假的！因此，如果`nums1[j-1]` = 0，我的 if 语句将为假，它将进入下一次迭代，这是一个问题，如果`nums1[j]`等于负数，因为然后我需要他们切换。*

*因此，如果`nums1[j-1]` = 0，改变我的代码，它看起来像这样:*

```
*for (let j = 1; j < len; j++) {
  if (nums1[j-1] || nums1[j-1] === 0) {
    if (nums1[j] < nums1[j-1]) {
      let tmp = nums1[j-1]
      nums1[j-1] = nums1[j]
      nums1[j] = tmp
      j = j-2
    }
  }
}*
```

*现在，我们开始工作了！完整的代码如下所示:*

```
*var merge = function(nums1, m, nums2, n) {
  const len = m + n
  nums1.splice(len-n) for (let i = 0; i < n; i++) {
    nums1.push(nums2[i])
  }

  for (let j = 1; j < len; j++) {
    if (nums1[j-1] || nums1[j-1] === 0) {
      if (nums1[j] < nums1[j-1]) {
        let tmp = nums1[j-1]
        nums1[j-1] = nums1[j]
        nums1[j] = tmp
        j = j-2
      }
    }
  }
  return nums1
};*
```

*这很有效！解决了！时间复杂度是 O(n ),因为我对循环运行 2 个**,但是它们没有嵌套，所以技术上是 O(2n ),但是我们只需要考虑主导项。当我在 Leetcode 上运行这个时，运行时间是 **64ms** ，这比提交的 **99.74%** 要好(是的，我超级抽)。***

*我很想知道我的代码是否可以进一步改进，或者你是如何解决这个算法的！*

*如果你在解决这个问题上有任何困难，我希望这能帮助你，并在未来寻找更多的 Leetcode 解决方案！*

*Leetcode 系列:*

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

**更多内容请看*[*plain English . io*](http://plainenglish.io/)*