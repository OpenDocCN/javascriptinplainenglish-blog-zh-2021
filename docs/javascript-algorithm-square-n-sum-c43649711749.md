# JavaScript 算法:平方和

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-square-n-sum-c43649711749?source=collection_archive---------9----------------------->

## 如何对数组中的每个数字求平方，并返回所有数字的总和。

![](img/96a8097ba666e3c509db930486bea581.png)

Photo by [Patrick Tomasso](https://unsplash.com/@impatrickt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`squareSum`的函数，它接受一个整数数组 `numbers`，一个参数。

给你一个正数和/或负数的数组。该函数的目标是对数组中的每个数字求平方，并将平方的结果相加。该函数返回该总和。

示例:

```
squareSum([0, 3, 4, 5]) //output: 50
```

如果我们把每个数字的平方相加，

```
0^2 + 3^2 + 4^2 + 5^2 = 0 + 9 + 16 + 25 = 50
```

我们总共有 50 个。

我们开始吧。

首先，我们创建一个名为`square`的变量。这个变量将保存我们平方后数组中数字的总和。

接下来，我们使用`reduce`函数将数组缩减到一位数。在 reducer 函数中，我们将所有数字平方并相加。

```
let square = numbers.reduce((acc, curVal) => {
    return acc + curVal ** 2;
}, 0);
```

这会给我们想要的总数。我们现在返回`square`。

```
return square;
```

下面是完整的函数:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](/javascript-algorithm-beginner-series-2-clock-ff163cb493ba) [## JavaScript 算法:初学者系列#2 时钟

### 以毫秒为单位返回自午夜以来的时间

javascript.plainenglish.io](/javascript-algorithm-beginner-series-2-clock-ff163cb493ba) [](https://levelup.gitconnected.com/javascript-algorithm-power-calculator-372c5f2d41eb) [## JavaScript 算法:功率计算器

### 使用给定的电压和电流计算电量的功能。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-power-calculator-372c5f2d41eb) [](https://levelup.gitconnected.com/javascript-algorithm-convert-minutes-into-seconds-4d4a0d750b6c) [## JavaScript 算法:将分钟转换成秒钟

### 这是一个关于如何将分钟转换成秒钟的简单函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-convert-minutes-into-seconds-4d4a0d750b6c) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)