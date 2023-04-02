# 在 JavaScript 中实现快速排序

> 原文：<https://javascript.plainenglish.io/implementing-quicksort-in-javascript-8923a9773044?source=collection_archive---------12----------------------->

![](img/6b5588b8dffe630dcd0ac6d131afaafa.png)

Photo by [Mikael Kristenson](https://unsplash.com/@mikael_k?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

上周我报道了用 JavaScript 实现合并排序的[。本周我将介绍快速排序，这是另一种常用的排序算法。像合并排序一样，快速排序是另一种比较排序算法，它采用了一种分治和并发的方法。](https://medium.com/javascript-in-plain-english/implementing-merge-sort-in-javascript-4ea74f92bbea)

# 分步示例

对阵列执行快速排序的步骤如下:

*   从数组中挑选一个元素，称为*中枢。*
*   对数组重新排序，使小于轴心的元素排在前面，大于轴心的元素排在后面。这称为分区，因为现在阵列位于两个分区中。
*   在两个分区上递归调用 quicksort，只要分区至少包含 1 个元素(基本情况)。

有几件事需要注意。选择哪个元素作为枢纽会极大地影响性能，例如，如果选择第一个或最后一个元素作为枢纽，并对已经排序的数组运行快速排序，将导致 O(n)时间复杂度。

另一件要注意的事情是，我们将使用霍尔的分区。以开发快速排序算法的计算机科学家东尼·霍尔命名。霍尔的分区通过使用两个索引来工作，分别指向数组的开头和结尾。索引将彼此相向移动，直到左边的索引(或数组的开始)找到大于或等于主元的元素，而右边的索引(或数组的结尾)找到小于或等于主元的元素。在这一点上，这两个元素将交换。当左和右(或开始和结束)索引交叉时，算法将返回左索引的值。

既然我们已经了解了整个过程以及分区过程，让我们开始吧。

## 预期结果

按升序排序
输入:[4，2，5，1，3，6]
输出:[1，2，3，4，5，6]

## 第一步

我们需要决定我们的支点。因为我们知道第一个或最后一个元素可能导致 O(n)时间复杂度，所以通常建议选择随机索引、中间索引或中间索引。为简单起见，我们将选择中间的索引。

`array = [4, 2, 5, 1, 3, 6]
pivot = 2 // since we’re working with 0 based indexing`

现在我们需要对阵列进行分区。我们将引用 pivot 处的数组值，并将开始和结束时的值与 pivot 值进行比较，以找到我们需要交换的内容。

`startIndex = 0
endIndex = 5
pivotVal = 5
[**4**, 2, **5**, 1, 3, **6**]`

startIndex (4)处的值小于 pivot 处的值，因此我们将递增 startIndex。endIndex (6)处的值大于我们的 pivot 值，因此我们将减少 endIndex。

`startIndex = 1
endIndex = 4
pivotVal = 5
[4, **2**, **5**, 1, **3**, 6]`

现在 2 < 5, so we increment startIndex. However 3 < 5, so we won’t decrement endIndex.

【

Now that the startIndex has overlapped with pivot it isn’t less than the pivot (they are equal). So at this point we will swap the elements at startIndex and endIndex (since we had already found an element less than our pivot at the endIndex).

So our array now looks like: [4, 2, 3, 1, 5, 6]
由于我们执行了交换，我们将增加 startIndex 并减少 endIndex。

`startIndex = 3
endIndex = 3
pivotVal = 5
[4, 2, 3, **1**, **5**, 6]`

1< 5, so we will increment startIndex. Then startIndex and endIndex will have crossed and we will end our partition algorithm and return startIndex.

This is what we are left with:


## 第二步

现在我们将使用返回的 startIndex 创建两个分区。第一个是从 0 索引到返回的索引减 1，第二个是从返回的索引到原始数组的末尾。

`partition1 = [4, 2, 3, 1]
partition2 = [5, 6]`

我们将在每个分区上运行 quicksort。让我们来看一下分区 1 的过程。

`array = [4, 2, 3, 1]
pivot = 1`

`startIndex = 0
endIndex = 3
pivotVal = 2
[**4**, **2**, 3, **1**]`

4 > 2 和 1 < 2
交换 4 和 1，并分别递增和递减 startIndex 和 endIndex。

`startIndex = 1
endIndex = 2
pivotVal = 2
[1, **2**, **3**, 4]`

2 不小于 2，所以我们不会增加 startIndex，3 > 2，所以我们会减少 endIndex。

`startIndex = 1
endIndex = 1
pivotVal = 2
[1, **2**, 3, 4]`

现在 startIndex、endIndex 和 pivotVal 的值都相同了。这有点奇怪，因为它实际上会导致我们“交换”这些值，尽管实际上什么都没有改变。之后，我们递增和递减 startIndex 和 endIndex。

`startIndex = 2
endIndex = 0
pivotVal = 2
[1, 2, 3, 4]`

由于 startIndex > endIndex，我们将结束我们的分区算法，并返回值 2。

## 最终迭代

从这里开始，我们的分区 1 现在实际上被分成另外两个分区[1，2]和[3，4]。我们还将对这些元素运行快速排序，尽管它们已经按顺序排列，这将对[1]和[2]以及[3]和[4]运行快速排序，它们都将遇到只有一个元素的数组的基本情况。分割 2 也是如此，因为它是[5，6]。它会分成[5]和[6]两部分，并击中基本情况。至此，我们的数组已经排序，快速排序算法也完成了。

# 密码

首先，我们需要制定我们的划分算法。

```
function partition(arr, start, end) {
    // For random pivot use => arr[Math.floor(Math.random() * (end - start + 1) + start)]; // middle pivot
    const pivotVal = arr[Math.floor((start + end) / 2)]; while (start <= end) {
        while (arr[start] < pivotVal) {
            start++;
        }
        while (arr[end] > pivotVal) {
            end--;
        } if (start <= end) {
            // swap
            let temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp; start++;
            end--;
        }
    } return start;
} 
```

就像我们一步一步的例子一样，我们得到了元素在轴上的值。从这里开始，我们将循环遍历数组，直到`start`索引小于`end`索引。

在我们的`while`循环中，开始时有两个`while`循环。他们的目的是增加`start`索引，直到有一个元素大于我们的枢纽值，并减少我们的`end`索引，直到有一个元素小于我们的枢纽值。

此时，我们交换`start`和`end`处的元素，并分别递增和递减它们。

一旦我们脱离了第一个`while`循环，我们就返回`start`，这样我们就可以用它来找到我们的分区。

现在让我们实现快速排序算法。

```
function quickSort(arr, start = 0, end = arr.length - 1) {
    if (start < end) {
        const index = partition(arr, start, end); quickSort(arr, start, index - 1);
        quickSort(arr, index, end);
    } return arr;
}
```

我们开始我们的`quickSort`函数，接受一个数组、一个`start`值和一个`end`值。我们给它们数组的第一个和最后一个索引的默认值，这样我们就可以在一个数组上调用`quickSort`,而不需要自己手动传递这些值。

然后，只要数组有不止一个元素(只要`start < end`)我们就会运行 partition，它会返回决定我们分区分割的`index`。最后我们返回数组。

# 时间复杂度、空间复杂度和稳定性

## 时间复杂度

最坏情况下的时间复杂度是 O(n)，这发生在所选择的中枢是重复的，其中大多数或所有其他元素大于或小于中枢的时候。平均和最好的时间复杂度是 O(n log n)。在这一点上，你可能想知道为什么我们会使用快速排序而不是合并排序，因为合并排序*总是*具有线性时间复杂度。使用快速排序很少得到最坏情况下的时间复杂度。除此之外，快速排序具有更好的缓存局部性。什么是缓存局部性？

这是来自[康乃尔大学](https://www.cs.cornell.edu/courses/cs3110/2012sp/lectures/lec25-locality/lec25.html) : *的简短描述“为了应对计算机内存相对变慢的问题，计算机架构师引入了* ***高速缓存*** *，它们是位于 CPU 和主内存之间的更小、更快的内存。高速缓存跟踪处理器最近请求的存储器位置的内容。如果处理器要求这些位置中的一个，缓存将给出答案。因为高速缓存比主存小得多(几百千字节而不是几十或几百兆字节)，所以它可以比主存更快地传送请求:几十个周期而不是几百个周期*

## 空间复杂性

快速排序就地排序，这是它比合并排序更受欢迎的另一个原因。也就是说，它具有 O(log n)的空间复杂度。这与在每个分区上进行的递归调用有关。[这个堆栈溢出](https://stackoverflow.com/questions/12573330/why-does-quicksort-use-ologn-extra-space#:~:text=Quicksort%20with%20in%2Dplace%20and,O(log%20n)%20space.)问题在评论中有一些非常有见地的答案(即使是关于 java 的，这些答案仍然适用)。

## 稳定性

快速排序不是一种稳定的排序算法，这也是您可能希望使用合并排序而不是快速排序的原因。这意味着它不会保持等值元素的顺序。

# 最后

快速排序和合并排序比我们前面的例子更难理解。就个人而言，我仍然更多地关注线性时间复杂度，现在我需要理解堆栈上的递归调用如何影响空间复杂度。也就是说，很高兴终于能够实现一些更广泛使用的排序算法。我已经把这篇博客中使用的代码放在了 GitHub 仓库[这里](https://github.com/ReginaF2012/JavaScript_quickSort)。