# JavaScript 算法:将数字加到一个数上，直到我们得到一位数的结果

> 原文：<https://javascript.plainenglish.io/javascript-algos-add-digits-to-a-number-until-we-get-a-single-digit-result-ee4835f85fea?source=collection_archive---------6----------------------->

## 日常 JavaScript 技巧、窍门和最佳实践

![](img/4e9e0d3bab680593317497d9e5dcbf3e.png)

Photo by [Girl with red hat](https://unsplash.com/@girlwithredhat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我为日常前端开发创建了一些技巧。

在这里，我将带来一篇新文章，介绍一些基于属性值对数组进行排序的方法。这些技巧可以成为你 2021 年 JavaScript 编码面试中的一块小石头。

*我知道小石头没什么区别，但如果我们有成千上万的石头，就有区别了..为此，我明天会带来新的石头。敬请期待*

开始今天的话题吧。

*“****给定一个整数*** `***num***` ***，重复将它的所有位数相加，直到结果只有一位数，并返回。”***

**示例:**

```
**Input:** num = 38
**Output:** 2
**Explanation:** The process is
38 --> 3 + 8 --> 11
11 --> 1 + 1 --> 2 
Since 2 has only one digit, return it.
```

在这个问题中，我们被要求达到给定数字的一位数。

## 1.让我们先尝试一个简单的解决方案

我们将使用`toString()`方法将所有数字转换为字符串数组，并遍历 for 循环，将数字相加，直到剩下一位数。

```
let addDigit = function(num) {   while (num.toString().length >= 2) {     let str = num.toString();     let currentSum = 0;      for (const digit of str) {       currentSum += Number(digit);     }      num = currentSum;   }    return num; }; console.log(addDigit(235)); //1
```

## 2.使用 reduce

我们可以用 reduce 函数代替 for 循环来达到同样的效果。

```
const addDigits = num => {   if (num.toString().length == 1) return num;   let New = num     .toString()     .split("")     .reduce((accumulate, current) => accumulate + Number(current), 0);   return addDigits(New); };  console.log(addDigits(23)); //5
```

**你可以在这里查看我以前的文章:**

*更多内容请看*[***plain English . io***](http://plainenglish.io/)