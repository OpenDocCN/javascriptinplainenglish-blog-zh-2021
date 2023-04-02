# JavaScript 挑战:找到数组中缺少的数字

> 原文：<https://javascript.plainenglish.io/javascript-challenge-find-the-missing-number-in-an-array-67689a10a74e?source=collection_archive---------5----------------------->

## 在给定的按 1 排序的自然数数组中查找缺失数字的 JavaScript 挑战

![](img/07333222bd46280212642a1fbb248858.png)

Photo by [Jexo](https://unsplash.com/@jexo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这个挑战中，我们的任务是在给定的数组中找到一个缺失的数字。所以，你得到了一个数组，你所知道的只是原始数组的长度和数组的值减去我们想要找到的缺失值。

我们得到了一个连续数字的数组，这个数组应该按顺序递增 1。因此，我们的数组应该是如下所示的形式。

```
[1, 2, 3,5, 6,7,8,9]
```

数组的总长度是九。

挑战外卖

*   数组。
*   数组操作/遍历。
*   简单的数学知识。

从上面给出的数组中，我们可以通过编程找到缺失的数字[4]。

## **挑战解决方案。**

首先，我们需要创建一个函数来确保接受所提供的数组，并对其进行操作以找到缺失的数字。

之后，我们需要找到在给定数组中出现的自然数的和。

我们可以这样做。

这样，我们就有了数组中值的预测和的值。

找出给定数组中这些值的和。

接下来，我们需要找到给定数组中值的总和。我们可以利用 for 循环来遍历数组，并将给定数组中的值相加。

现在，我们既有给定数组中值的和，也有给定数组中出现的自然数的和。

现在我们可以做的是将这两个值相减，以找到给定自然数数组中缺失的相应自然数。

最终解决

## 结论

感谢您阅读这篇文章。此外，如果你觉得我的内容有用，而你不是媒体会员，你可以在这里(媒体推荐链接)获得你的媒体会员资格[，无限制地访问所有内容，并支持我们作为作家。](https://amjohnphilip.medium.com/membership)

## 更多阅读

[](/3-tips-i-use-to-maximize-move-beyond-tutorials-b1b2f59322c0) [## 我用来最大化和超越教程的 3 个技巧

### 我如何充分利用编程教程？

javascript.plainenglish.io](/3-tips-i-use-to-maximize-move-beyond-tutorials-b1b2f59322c0) [](/how-to-level-up-your-skills-as-a-self-taught-programmer-c77fc284f2fd) [## 作为一名自学成才的程序员，如何提升自己的技能

### 作为一个自学成才的程序员，用这些技巧和窍门搞定它。

javascript.plainenglish.io](/how-to-level-up-your-skills-as-a-self-taught-programmer-c77fc284f2fd) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)