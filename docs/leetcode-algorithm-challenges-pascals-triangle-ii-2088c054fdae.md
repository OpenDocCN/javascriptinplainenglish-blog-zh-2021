# LeetCode 算法挑战:帕斯卡的三角 II

> 原文：<https://javascript.plainenglish.io/leetcode-algorithm-challenges-pascals-triangle-ii-2088c054fdae?source=collection_archive---------7----------------------->

# 问题

给定一个整数`rowIndex`，返回**帕斯卡三角形**的`rowIndexth` ( **0 变址**)行。

在**帕斯卡三角形**中，每个数字是它正上方的两个数字之和，如图所示:

![](img/a5b14972920e57a9dde8713a276af03f.png)

**例 1:**

```
**Input:** rowIndex = 3
**Output:** [1,3,3,1]
```

**例 2:**

```
**Input:** rowIndex = 0
**Output:** [1]
```

**例三:**

```
**Input:** rowIndex = 1
**Output:** [1,1]
```

# 那应该很容易吧？

上周我解决了[帕斯卡的三角形挑战](https://leetcode.com/problems/pascals-triangle/)，下一个上榜的是帕斯卡的三角形 II。考虑到我已经有了第一个挑战的解决方案，我认为这很容易。

回顾一下，在帕斯卡三角形挑战中，我们得到了行数，我们返回了帕斯卡三角形的所有行。那个函数的返回值是一个数组，我想哇，这真的很简单。我有如下回报声明:

```
return values;
```

所以我简单地把它改成了下面的值，它会显示一个与所需行的索引相对应的行。

```
return values[rowIndex-1];
```

嗯，认为某件事很容易，没有仔细阅读，导致我犯了一个错误。在当前的挑战中，输入值不是上一个挑战中的行号，而是行索引。所以索引是 0，表示第 1 行，索引 2 表示第 3 行，以此类推。这一次我决定一步一步地检查整个函数，以确保这次我做对了。

函数声明改变了，这是一个重要的改变，因为这里使用了参数`rowIndex`。

```
var getRow = function (rowIndex) { ....}
```

下一个关键的变化是`for loop`条件，原来我用的是`numRows`，现在是`rowIndex`。

```
for (let n = 0; n < numRows; n++) {
```

对

```
for (let n = 0; n <= rowIndex; n++) {
```

有一个变化，使这个功能的工作。这是一个非常小的变化，但它确实有用。当我们到达我们的 rowIndex 时，我们的循环结束，因此`<`标志着`<=`的改变。

现在我只需要返回由`values`数组的`rowIndex`指定的元素。

```
return values[rowIndex];
```

# 密码

请在以下社交网络上查看我，我很乐意收到您的来信！——[*LinkedIn*](https://www.linkedin.com/in/nick-solonyy/)*，* [*GitHub*](https://github.com/nicksolony) ， [*脸书*](https://www.facebook.com/nick.solony) *。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)