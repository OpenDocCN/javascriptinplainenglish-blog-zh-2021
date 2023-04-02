# 什么是二分搜索法算法？

> 原文：<https://javascript.plainenglish.io/a-word-on-binary-search-241df807761e?source=collection_archive---------29----------------------->

![](img/bb34ad9b35a263f979eb3ef68c1aef6a.png)

Binary Search — Chopping things in half over and over again

新年的第一周，我一直在研究的最相关的算法之一是二分搜索法算法。二分搜索法就是这样一种有用的算法，因为它有效地使事情更容易找到，并且不会太复杂而难以理解。从另一个角度来看，这有点像一遍又一遍地把一根木头劈成两半，直到你到达你想要的劈砍点。具体就二分搜索法而言，这一理想点将是我们的目标数字点。

# 二分搜索法到底是什么？

二分搜索法的意思是，在一组排序有序的事物中，也许是一组数字，将该组的中间值与您试图搜索的事物(目标)进行比较，以查看这两者是否匹配。如果它们是匹配的，那么你已经找到了你一直在寻找的东西，但是如果不是，那么排序后的组被切成两半，并且只观察适用于中间与目标如何比较的任何一边。例如，如果你要找的东西比中间值大，那么你应该看右边，因为那里有更大的东西。

实现这一概念的一个简单例子是:

我们在这个数组的 5 个数字列表中寻找数字 4(目标):

[1, 2, 3, 4, 5].

首先你可以看中间，看到 3 是中间的数字。3 比 4 小，3 比 4 小。因为这些数字是有序的，所以从 3 的右边寻找更大的数字 4 是有意义的。1 和 2 被淘汰现在 4 是[3，4，5]的新中间，等于我们要找的目标。

现在进行一些编码。我将一步一步地讲述我是如何使用 JavaScript 解决二分搜索法算法的，并像往常一样尽可能地简化这个过程。

# 问题是

编写一个函数，它接受一个排序的整数数组和一个目标数，并使用二分搜索法算法来确定目标数是否在数组中。如果是，那么函数应该返回目标数字的索引。如果不是，则返回-1。

# 解决方案

首先使用关键字函数，我将我们的函数称为 binarySearch 函数，并给它上面列出的输入；一个数组和一个目标数。此外，为了使用二分搜索法风格的算法，我们需要两个指针，即左指针和右指针。这些变量将代表数组中每一边的索引。左边代表第一个数字，右边代表最后一个数字。

```
function binarySearch(array, target) { let left = 0
  let right = array.length-1
```

此时，我将使用 for 循环来遍历数组中的所有数字，以应用我们的逻辑。接下来是初始化一个中间变量，该变量使用 Math.floor 赋值。Math.floor 会将我们的结果向下舍入到小于或等于括号中值的最大整数。在括号中，我们将把左指针和右指针的索引加在一起，然后除以 2 得到平均值，这个值大约在数组的中间。

```
function binarySearch(array, target) { let left = 0
  let right = array.length-1 for (let i=0; i<array.length; i++){
   let middle = Math.floor((left+right) / 2)
```

在下一阶段，我们将编写一个 if 语句，检查数组中间的数字是否与目标数字相同。如果是，那么我们已经找到了我们要找的数字，所以我们将返回该数字的索引。

```
function binarySearch(array, target) { let left = 0
  let right = array.length-1 for (let i=0; i<array.length; i++){
   let middle = Math.floor((left+right) / 2)
   if(array[middle] === target){
     return array.indexOf(target)
```

如果我们没有找到我们要寻找的目标数，那么下一步我们就必须遍历下面写的 else if 语句。这两者是相反的，因为在这一点上我们可以有两种可能性。我们寻找的目标要么比中间的数字小，要么比中间的数字大。

第一个 else if 条件声明，如果中间的数字大于目标值，则将右边的变量赋给中间的左边。当我们把现在看到的数字移到左边时，这就是“削波”开始的地方。

如前所述，第二个 else if 条件正好相反。如果目标数字高于中间的数字，那么我们需要将左边的变量从中间第一个右边的空格开始赋值。在这种情况下,“削波”应该在右边。

```
function binarySearch(array, target) {let left = 0
let right = array.length-1
for (let i=0; i<array.length; i++){
  let middle = Math.floor((left+right) / 2)
  if(array[middle] === target){
   return array.indexOf(target)
  } else if (array[middle] > target){
   right = middle-1
  } else if (array[middle] < target){
   left = middle +1
  }
```

只有一种可能性，如果我们的 if 条件都不满足。那就是我们要找的数字在我们的数组中不存在。如果是这样，根据问题陈述，我们需要返回-1 并关闭我们的函数，如下所示。

```
function binarySearch(array, target) {let left = 0
let right = array.length-1
for (let i=0; i<array.length; i++){
  let middle = Math.floor((left+right) / 2)
  if(array[middle] === target){
   return array.indexOf(target)
  } else if (array[middle] > target){
   right = middle-1
  } else if (array[middle] < target){
   left = middle +1
  }
}
 return -1
}
```

这就是我们算法的结尾。我发现理解这个算法是理解比这个更难的算法的关键之一。在学习如何对数据进行排序以获得所需结果的模式时，二分搜索法算法是需要真正掌握的最基本的概念之一，所以我鼓励其他人花时间去理解它。感谢您阅读本指南，祝您新年快乐，充满新的机遇。