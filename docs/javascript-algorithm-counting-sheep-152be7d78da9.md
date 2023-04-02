# JavaScript 算法:数羊

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-counting-sheep-152be7d78da9?source=collection_archive---------11----------------------->

## 数一排绵羊的数量

![](img/105859dcab7a42f6a80d5bc8122c0fb1.png)

Photo by [Tanner Yould](https://unsplash.com/@tyould?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`countSheeps`的函数，它接受一个数组`arrayOfSheep`作为参数。

给你一个包含布尔值的数组。该函数的目标是返回当前有多少只羊。如果值是`true`,这意味着羊出现了。

示例:

```
let array = [true,  true,  true,  false,
              true,  true,  true,  true ,
              true,  false, true,  false,
              true,  false, false, true ,
              true,  true,  true,  true ,
              false, false, true,  true ];countSheeps(array1); // output: 17
```

在上面的例子中，数组中有 17 个`true`值，所以函数将输出`17`。

即使数组值是布尔值，检查其他假值也很重要，比如`null`和`undefined`。

对于这个函数，我们将使用`filter`方法。我们首先创建一个名为`present`的常量变量。该变量将包含保存来自`arrayOfSheep`的所有`true`值的数组。

```
const present = arrayOfSheep.filter(sheep => sheep);
```

`filter`方法将帮助我们过滤掉数组输入中的所有`falsey`值。

通过只返回`sheep`，JavaScript 使用类型转换将每个值作为布尔值进行评估。任何被认为是假值的都不会包含在`present`数组中。

现在我们有了`true`值的数组，我们需要做的就是返回数组的长度。这个数字代表在场的羊的数量。

```
return present.length;
```

下面是完整的函数:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](/javascript-algorithm-array-diff-90e109b9acf4) [## JavaScript 算法:Array.diff

### 实现从一个列表中减去另一个列表的差函数

javascript.plainenglish.io](/javascript-algorithm-array-diff-90e109b9acf4) [](/javascript-algorithm-finding-the-longest-word-in-a-string-2e7458ef4cef) [## JavaScript 算法:查找字符串中最长的单词

### 创建一个函数来返回包含字符串中最长单词的数组。

javascript.plainenglish.io](/javascript-algorithm-finding-the-longest-word-in-a-string-2e7458ef4cef) [](https://levelup.gitconnected.com/javascript-algorithm-calculate-sum-of-all-numbers-in-a-jagged-array-94230951d726) [## JavaScript 算法:计算交错数组中所有数字的和

### 创建一个计算交错数组中所有数字之和的函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-calculate-sum-of-all-numbers-in-a-jagged-array-94230951d726) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)