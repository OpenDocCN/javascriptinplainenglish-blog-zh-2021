# JavaScript 算法:数组的等边

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-equal-sides-of-an-array-e4e06055bf4a?source=collection_archive---------0----------------------->

## 返回一个数组索引，其中数组左边索引的和等于右边索引的和

![](img/7f697735d44a3e776069a5316259f7d8.png)

Photo by [Antoine Dautry](https://unsplash.com/@antoine1003?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`findEvenIndex`的函数，它接受一个数组`arr`作为参数。

给你一个整数数组。该函数的目的是获取数组并返回索引，其中索引左边的整数之和等于索引右边的整数之和。如果没有这样的东西或者数组是空的，返回`-1`。

示例:

```
[1,2,3,4,3,2,1] // output: 3
[1,100,50,-51,1,1] // output: 1
```

如果我们看第一个例子，第四个数字(指数 3)是指数左边的总和等于指数右边的总和。

索引 3 左侧:`1 + 2 + 3 = 6`

索引 3 的右侧:`3 + 2 + 1 = 6`

如果你看第二个例子。这是一回事:

在索引 1 的左侧:`1`

在索引 1 的右侧:`50 + -51 + 1 + 1 = 1`

首先，我们要创建一些变量。

```
let left = 0;  
let right = 0;  
const reducer = (accumulator, currentValue) => accumulator + currentValue;
```

变量`left`将保存数组中索引`i`左边所有数字的总和。

变量`right`将保存数组中索引`i`右边所有数字的总和。

`reducer`变量是我们在使用`reduce`方法得到一个数组中所有数字的和时要用到的缩减函数。

首先，我们创建一个 if 语句来检查数组是否为空。如果是，返回`-1`。

```
if(arr.length == 0){    
    return -1;  
}
```

接下来，我们将使用 for 循环遍历数组。

```
for (let i = 0; i < arr.length; i++) {
    if (i == 0) {
        right = arr.slice(1).reduce(reducer, 0);
        if (right === i) {
            return i;
        }
    } else {
        left = arr.slice(0, i).reduce(reducer, 0);
        right = arr.slice(i + 1).reduce(reducer, 0);
        if (left == right) {
            return i;
        }
    }
}
```

在第一个 if 语句中，当我们从第一个索引`0`开始时，我们使用`slice()`方法提取第一个数字右边的每个数字。使用`reduce()`方法和我们的`reducer`函数，我们将所有数字相加，并将总和赋给`right`变量。我们检查总和是否等于数组中的第一个值。如果索引左侧没有任何内容，则索引右侧的所有数字都必须等于第一个数组整数。如果是，返回`i`或`0`。

```
if (i == 0) {
    right = arr.slice(1).reduce(reducer, 0);
    if (right === i) {
        return i;
    }
}
```

对于其他索引位置，当我们进入数组时，我们使用`slice()`方法提取当前索引左边的所有数字。我们获取该数组，并对其应用`reduce()`方法，以获得数组中所有数字的总和。我们对索引右边的所有值做同样的事情。

我们使用 if 语句比较`left`和`right`的和值，如果值相同，我们返回索引。

```
else {
    left = arr.slice(0, i).reduce(reducer, 0);
    right = arr.slice(i + 1).reduce(reducer, 0);
    if (left == right) {
        return i;
    }
}
```

如果函数设法到达循环的末尾却没有找到索引，我们默认返回`-1`。这意味着不存在这样一个指数，它的两边和相等。

```
return -1;
```

下面是完整的函数:

如果您觉得这个算法有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-categorize-new-member-8cb175a469) [## JavaScript 算法:对新成员进行分类

### 创建一个函数，根据数组中的数据对门球俱乐部的新成员进行分类

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-categorize-new-member-8cb175a469) [](/javascript-algorithm-find-difference-between-two-arrays-ed8df86c4924) [## JavaScript 算法:找出两个数组之间的差异

### 返回一个数组的函数，该数组的元素在第一个数组中，但不在第二个数组中。

javascript.plainenglish.io](/javascript-algorithm-find-difference-between-two-arrays-ed8df86c4924) [](https://endubueze00.medium.com/javascript-algorithm-fizzbuzz-42129ee418e6) [## JavaScript 算法:FizzBuzz

### 你常用的编程算法。

endubueze00.medium.com](https://endubueze00.medium.com/javascript-algorithm-fizzbuzz-42129ee418e6)