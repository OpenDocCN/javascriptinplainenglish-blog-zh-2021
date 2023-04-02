# JavaScript 算法:列表过滤

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-list-filtering-5ad64fa2d264?source=collection_archive---------13----------------------->

## 从数组中移除所有字符串

![](img/02687645e6aad7d7f75e6796046a150e.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`filter_list`的函数，它将接受一个数组`l`作为参数。

给你一个整数和字符串的数组。该函数的目标是返回相同元素的新数组，但没有字符串。

示例:

```
filter_list([1,2,'a','b']) 
//output: [1,2]filter_list([1,'a','b',0,15]) 
// output: [1,0,15]
```

这个函数很短，所以首先我们使用`filter`方法从输入数组中过滤掉字符串。为了检查一个元素是字符串还是数字，我们使用了`typeof`操作符。我们只想保留具有`"number"`的`typeof`的元素。

接下来，我们将新数组赋给一个名为`noStr`的变量并返回它。

```
let noStr = l.filter(elem => typeof elem === "number");                         return noStr;
```

下面是完整的函数:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](/javascript-algorithm-square-n-sum-c43649711749) [## JavaScript 算法:平方和

### 如何对数组中的每个数字求平方，并返回所有数字的总和。

javascript.plainenglish.io](/javascript-algorithm-square-n-sum-c43649711749) [](/javascript-algorithm-beginner-series-2-clock-ff163cb493ba) [## JavaScript 算法:初学者系列#2 时钟

### 以毫秒为单位返回自午夜以来的时间

javascript.plainenglish.io](/javascript-algorithm-beginner-series-2-clock-ff163cb493ba) [](/javascript-algorithm-detect-pangram-9d57ca713d0d) [## JavaScript 算法:检测 Pangram

### 盘符是一个包含字母表中每个字母至少一次的句子。

javascript.plainenglish.io](/javascript-algorithm-detect-pangram-9d57ca713d0d) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)