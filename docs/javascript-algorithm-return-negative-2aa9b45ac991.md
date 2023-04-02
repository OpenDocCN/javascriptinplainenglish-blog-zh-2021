# JavaScript 算法:返回负数

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-return-negative-2aa9b45ac991?source=collection_archive---------7----------------------->

## 创建一个返回所有负数的函数

![](img/77388caa214a4fd14d3baa30abc26954.png)

Photo by [Gage Walker](https://unsplash.com/@gagewalkerr?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`makeNegative`的函数，它将接受一个整数`num`作为参数。

该函数的目标是使`num`为负。如果输入的整数已经是负数或零，则按原样返回数字。

示例:

```
makeNegative(1); *// return -1*
makeNegative(-5); *// return -5*
makeNegative(0); *// return 0*
makeNegative(0.12); *// return -0.12*
```

我们要做的第一件事是编写一个 if 语句，检查`num`是否是一个小于或等于零的值。把零变成负数是没有意义的，如果一个数已经是负数了。如果这个陈述是真实的，我们应该让它保持原样并将其返回。

```
if(num <= 0){
    return num;
}
```

如果`num`不满足第一个条件，我们编写一个 else 语句，将正值转换为负值。我们返回那个值。

```
return -Math.abs(num);
```

以下是剩余的代码:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-calculate-sum-of-all-numbers-in-a-jagged-array-94230951d726) [## JavaScript 算法:计算交错数组中所有数字的和

### 创建一个计算交错数组中所有数字之和的函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-calculate-sum-of-all-numbers-in-a-jagged-array-94230951d726) [](/javascript-algorithm-array-diff-90e109b9acf4) [## JavaScript 算法:Array.diff

### 实现从一个列表中减去另一个列表的差函数

javascript.plainenglish.io](/javascript-algorithm-array-diff-90e109b9acf4) [](/javascript-algorithm-finding-the-longest-word-in-a-string-2e7458ef4cef) [## JavaScript 算法:查找字符串中最长的单词

### 创建一个函数来返回包含字符串中最长单词的数组。

javascript.plainenglish.io](/javascript-algorithm-finding-the-longest-word-in-a-string-2e7458ef4cef) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)