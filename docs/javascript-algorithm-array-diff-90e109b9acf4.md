# JavaScript 算法:Array.diff

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-array-diff-90e109b9acf4?source=collection_archive---------8----------------------->

## 实现从一个列表中减去另一个列表的差函数

![](img/06a319eaede2d0d4eaaf2b6557d4fa93.png)

Photo by [Crissy Jarvis](https://unsplash.com/@crissyjarvis?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`arrayDiff`的函数，它将接受两个数组`a`和`b`作为参数。

给你两个数组。该函数的目标是移除数组`b`中存在的数组`a`中的所有值。该函数应该在删除所有公共值后返回数组。

以下是一些例子:

```
arrayDiff([], [4,5]) //output: []
arrayDiff([3,4], [3]) // output: [4]
arrayDiff([1,8,2], []) // output: [1, 8, 2]
```

在第一个例子中，`a`中没有值在`b`中。默认情况下，该数组为空，因此该函数将返回一个空数组。

在第二个例子中，在`b`中只找到了来自`a`的`3`，因此数字被删除，函数返回`[4]`。

在最后一个例子中，`a`中的所有值在`b`中都找不到，因此函数返回`[1,8,2]`。

首先，我们将创建一个名为`arr1`的变量，它将包含所有出现在`a`中但不在`b`中的值。这是函数将返回的数组。我们给它分配一个空数组。

```
let arr1 = [];
```

如果你看看上面的第一个和第三个例子，我们注意到如果`b`为空，函数将原样返回`a`数组。当`a`数组为空时也会发生这种情况。

因此，我们将编写一个 if 语句来检查`a`或`b`的数组长度是否为零。如果是，则原样返回`a`。

```
if(b.length === 0 || a.length === 0){    
    return a;  
}
```

除了 if 语句，我们还将添加一个`else`语句。在 else 块中，我们将使用`filter()`方法遍历`a`数组，并过滤掉所有存在的值`b`。

我们将结果数组赋给`arr1`并返回它。

```
arr1 = a.filter(num => !(b.includes(num)));
```

下面是完整的 if 语句:

```
if(b.length === 0 || a.length === 0){    
    return a;  
}else{    
    arr1 = a.filter(num => !(b.includes(num)));
    return arr1; 
}
```

下面是完整的函数:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](/javascript-algorithm-finding-the-longest-word-in-a-string-2e7458ef4cef) [## JavaScript 算法:查找字符串中最长的单词

### 创建一个函数来返回包含字符串中最长单词的数组。

javascript.plainenglish.io](/javascript-algorithm-finding-the-longest-word-in-a-string-2e7458ef4cef) [](https://levelup.gitconnected.com/javascript-algorithm-calculate-sum-of-all-numbers-in-a-jagged-array-94230951d726) [## JavaScript 算法:计算交错数组中所有数字的和

### 创建一个计算交错数组中所有数字之和的函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-calculate-sum-of-all-numbers-in-a-jagged-array-94230951d726) [](/javascript-algorithm-distance-between-points-7fe0026857e3) [## JavaScript 算法:两点之间的距离

### 创建一个函数来计算由 x 和 y 坐标定义的两点之间的距离。

javascript.plainenglish.io](/javascript-algorithm-distance-between-points-7fe0026857e3)