# JavaScript 算法:100 以内？

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-less-than-100-9bdff6d4d6a9?source=collection_archive---------10----------------------->

## 写一个函数，检查两个数之和是否小于 100。

![](img/765ac3855524756465dae25a7a23f6f2.png)

Photo by [Antoine Dautry](https://unsplash.com/@antoine1003?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`lessThan100`的函数，它将接受两个整数`a`和`b`作为参数。

该函数的目标是检查`a`和`b`之和是否小于 100。

示例:

```
lessThan100(22, 15) ➞ true
// 22 + 15 = 37

lessThan100(83, 34) ➞ false
// 83 + 34 = 117
```

为了编写函数，我们可以使用 if 语句来检查`a`和`b`的和是否小于 100。如果是，返回 true，否则返回 false。

```
if(a + b < 100){
    return true;
}else{
    return false;
}
```

解决这个问题的另一种方法是放弃 if 语句，只返回布尔求值。

```
return a + b < 100
```

这样做的目的是，代码将评估`<`符号左侧的语句，并将其与右侧进行比较，看看左侧的值是否小于 100。布尔语句将返回真或假。

代码到此结束。以下是其余部分:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-array-plus-array-19e17c70e9fe) [## JavaScript 算法:数组加数组

### 写一个计算两个数组之和的函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-array-plus-array-19e17c70e9fe) [](https://medium.com/javascript-in-plain-english/javascript-algorithm-power-2cbedf59f40c) [## JavaScript 算法:Power

### 我们将编写一个函数，不使用任何内置的数学函数来返回一个数的幂。

medium.com](https://medium.com/javascript-in-plain-english/javascript-algorithm-power-2cbedf59f40c) [](https://levelup.gitconnected.com/javascript-algorithm-pangrams-3e6add10f38f) [## JavaScript 算法:Pangrams

### 对于今天的算法，我们要写一个叫做 pangrams 的函数，它接受一个字符串 s 作为输入。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-pangrams-3e6add10f38f)