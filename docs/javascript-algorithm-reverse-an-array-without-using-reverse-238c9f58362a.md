# JavaScript 算法:不使用 Reverse()反转数组

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-reverse-an-array-without-using-reverse-238c9f58362a?source=collection_archive---------11----------------------->

## 编写一个函数，不使用内置的 JavaScript reverse 方法来反转一个小数组。

![](img/2dc37e6477b9de89f1324586f972c487.png)

Photo by [Guillaume TECHER](https://unsplash.com/@guillaume_t?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

今天我们要写一个名为`reverseArray`的函数，它接受一个数组`arr`作为参数。

给我们一个数组，这个函数的目标是反转这个数组。已经有一个名为`reverse()`的 JavaScript 数组方法可以为你反转一个数组，但是我们不打算使用它。

下面是我们想要实现的目标的一个示例:

```
let arr = ["a", "d", 4, "t", "h", 5, "e", "f", 3];
reverseArray(arr);// output: [3, "f", "e", 5, "h", "t", 4, "d", "a"]
```

让我们开始编写这个函数。

首先，我们创建一个空数组，并将其赋给一个名为`newArr`的变量。这是与`arr`相反的变量。这个回报我们也会还的。

```
let newArr = [];
```

接下来，我们使用 for 循环，但是循环将从数组中的最后一个元素开始向后迭代到第一个元素。该函数会在每次迭代时将每个字符添加到`newArr`数组中。

```
for(let i = arr.length - 1; i >= 0; i--){
    newArr.push(arr[i]);
}
```

我们现在可以返回反转后的数组。

```
return newArr;
```

下面是该函数的其余部分:

虽然`reverse()`方法很有用，但是学习如何在不使用内置方法的情况下使用一些东西也无妨。这个函数特别有用，可以帮助您学习如何使用 for 循环来向后遍历数组。许多循环例子从开始循环，但从结尾循环的不多。

如果你觉得这个算法有帮助，看看我的其他 JavaScript 算法解决方案:

[](https://levelup.gitconnected.com/javascript-algorithm-using-objects-for-lookups-d28f34a59504) [## JavaScript 算法:使用对象进行查找

### 我们将把一个 switch 语句转换成一个 JavaScript 对象，并根据给定的…

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-using-objects-for-lookups-d28f34a59504) [](https://medium.com/javascript-in-plain-english/javascript-algorithm-return-positive-numbers-faacd7537b32) [## JavaScript 算法:返回正数

### 一个函数，它将返回在另一个数组中找到的正数数组。

medium.com](https://medium.com/javascript-in-plain-english/javascript-algorithm-return-positive-numbers-faacd7537b32) [](https://medium.com/swlh/javascript-algorithm-sorted-union-9e316654561f) [## JavaScript 算法:排序联合

### 我们编写一个函数，它将返回从两个或更多其他数组中获取的唯一值的数组。

medium.com](https://medium.com/swlh/javascript-algorithm-sorted-union-9e316654561f)