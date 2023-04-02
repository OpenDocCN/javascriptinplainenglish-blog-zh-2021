# JavaScript 算法:找出两个数组之间的差异

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-find-difference-between-two-arrays-ed8df86c4924?source=collection_archive---------7----------------------->

## 返回一个数组的函数，该数组的元素在第一个数组中，但不在第二个数组中。

![](img/d02b7f705c2d38bf8b73a289c8075216.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`mergeLeft`的函数，它将接受两个数组`arr1`和`arr2`作为参数。

该函数的目标是返回一个新数组，其中包含存在于`arr1`中但不存在于`arr2`中的元素。

示例:

```
let arr1 = [1, 2, 3, 10, 5, 3, 14];
let arr2 = [-1, 4, 5, 6, 14];
mergeLeft(arr1, arr2);//output: [1,2,3,10,3]
```

唯一被排除的数字是 5 和 14，因为这些数字在`arr1`和`arr2`中都有。

我们要做的第一件事是在`arr1`上使用`filter()`方法。我们将使用它来创建一个新的数组，其中包含只存在于`arr1`中的元素。

如果`arr1`中的特定元素存在于`arr2`中，则`includes()`方法将返回`true`。我们不希望这样，所以我们用 NOT 操作符`!`否定该语句，这样我们可以得到相反的结果。

```
let arrDiff1 = arr1.filter(function(e){      
    return !(arr2.includes(e));    
});
```

我们返回数组:

```
return arrDiff1;
```

下面是完整的函数:

如果你觉得这个算法有帮助，看看我的其他 JavaScript 算法解决方案:

[](https://levelup.gitconnected.com/javascript-algorithm-array-differences-dc0f012b307a) [## JavaScript 算法:数组差异

### 将两个数组之间的差异放到另一个数组中。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-array-differences-dc0f012b307a) [](https://medium.com/javascript-in-plain-english/javascript-algorithm-merge-two-arrays-e88e002e1554) [## JavaScript 算法:合并两个数组

### 用 JavaScript 编写合并两个数组的两种方法

medium.com](https://medium.com/javascript-in-plain-english/javascript-algorithm-merge-two-arrays-e88e002e1554) [](https://medium.com/swlh/javascript-algorithm-sorted-union-9e316654561f) [## JavaScript 算法:排序联合

### 我们编写一个函数，它将返回从两个或更多其他数组中获取的唯一值的数组。

medium.com](https://medium.com/swlh/javascript-algorithm-sorted-union-9e316654561f)