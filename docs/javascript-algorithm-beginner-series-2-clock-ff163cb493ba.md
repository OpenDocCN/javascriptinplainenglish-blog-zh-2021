# JavaScript 算法:初学者系列#2 时钟

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-beginner-series-2-clock-ff163cb493ba?source=collection_archive---------4----------------------->

## 以毫秒为单位返回自午夜以来的时间

![](img/269b4b0c914b87629771036cb7027011.png)

Photo by [Djim Loic](https://unsplash.com/@loic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`past`的函数，它将接受三个整数`h, m, s`作为一个整数。

有一个时钟以小时`h`、分钟`m`和秒钟`s`显示时间。小时、分钟和秒显示自午夜以来的时间。该函数的目标是返回以毫秒为单位的时间。

示例:

```
past(1,1,1) // output: 3661000
```

在上面的例子中，时钟显示从午夜开始已经过了 1 小时 1 分 1 秒。

要将时间从秒转换为毫秒，请乘以:

秒 x 1000

要将时间从分钟转换为毫秒，请乘以:

分钟* 60000

要将时间从小时转换为毫秒，请乘以:

小时* 3600000

一旦你做了计算，把所有的毫秒加在一起，总数将是`3661000`。

为了开始编写这个函数，我们用上面写的等式将秒、分和小时转换为毫秒，并将它们赋给以下变量:

```
let secondsToMillisec = s * 1000;
let minutesToMillisec = m * 60000;
let hoursToMillisec = h * 3600000;
```

`secondsToMillisec`变量将秒转换为毫秒。

`minutesToMillisec`变量将分钟转换成毫秒。

`hoursToMillisec`变量将小时转换为毫秒。

最后，我们将每个变量的总数相加，并返回结果:

```
return secondsToMillisec + minutesToMillisec + hoursToMillisec;
```

下面是完整的函数:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-find-the-parity-outlier-666e350883ec) [## JavaScript 算法:寻找奇偶异常值

### 找出奇数(或偶数)

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-find-the-parity-outlier-666e350883ec) [](/javascript-algorithm-detect-pangram-9d57ca713d0d) [## JavaScript 算法:检测 Pangram

### 盘符是一个包含字母表中每个字母至少一次的句子。

javascript.plainenglish.io](/javascript-algorithm-detect-pangram-9d57ca713d0d) [](/javascript-algorithm-find-the-perimeter-of-a-rectangle-96ecb7ab0ea2) [## JavaScript 算法:求矩形的周长

### 创建一个寻找矩形周长的函数。

javascript.plainenglish.io](/javascript-algorithm-find-the-perimeter-of-a-rectangle-96ecb7ab0ea2) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)