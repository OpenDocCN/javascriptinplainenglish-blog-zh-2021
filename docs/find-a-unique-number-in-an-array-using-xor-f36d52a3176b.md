# 使用 XOR 查找数组中的唯一数字

> 原文：<https://javascript.plainenglish.io/find-a-unique-number-in-an-array-using-xor-f36d52a3176b?source=collection_archive---------5----------------------->

## 在由重复数字组成的数组中查找唯一数字的有效且最佳的方法。

![](img/2209a0918c326605527cf88c00e912e0.png)

Photo by [Ricardo Gomez Angel](https://unsplash.com/@rgaleria?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你的基础知识不是那么清楚，为编程中的特定问题寻找解决方案确实是一项繁重的任务。解决问题的头脑是大多数人寻求的。实现解决问题的头脑需要编程的一致性。

在本文中，我们将借助**逻辑运算符**在数组中找到一个唯一的数字。我们将使用**异或**来找出数组中的奇数。

## 问题陈述

如果给你一个数组 **a[]={1，2，3，4，5，4，3，2，1}** ，然后找出唯一的数字。请注意，所有的数字都重复两次，并且在给定的数组中唯一的数字只能出现一次。

这里我们将使用 XOR 的有趣特性。一个数与其自身的异或运算会抵消该数，或者精确地给出 0。因此，如果我们对数组中的每个元素进行异或运算，那么重复的元素将被抵消，剩下的就是唯一的数字

```
**a[]={1,2,3,4,5,4,3,2,1}**we are given an array which contains duplicates in it. Find the unique number which is present only oncecode-//let n be the size of array afunction(array a[]){int xorsum=0; //variable to calculate xor and store unique numberfor(int i=0;i<n;i++)
    {
     xorsum=xorsum^a[i];
     }return xorsum;}result--> 5 
Hence, a unique number is found in the array.
Time complexity--> O(n)
```

我们有效地使用了逻辑运算符来寻找唯一的数字。编程需要在进入高级概念之前深入理解基础知识。它将极大地帮助你轻松解决现实生活中的问题。

我希望这篇文章是有帮助和信息的。坚持编程，坚持练习。祝你的编程之旅好运！

[](https://aniketz.medium.com/membership) [## 通过我的推荐链接加入 Medium-Aniket

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

aniketz.medium.com](https://aniketz.medium.com/membership) [](/3-books-every-programmer-should-read-97ac12422cfb) [## 每个程序员都应该读的 3 本书

### 帮助我理解编程基础的书籍。

javascript.plainenglish.io](/3-books-every-programmer-should-read-97ac12422cfb) [](/how-to-calculate-the-length-of-a-string-without-using-an-inbuilt-function-51c8835945b7) [## 如何不用内置函数计算字符串的长度

### 程序员用两种有效方法求字符串长度的基本指南。

javascript.plainenglish.io](/how-to-calculate-the-length-of-a-string-without-using-an-inbuilt-function-51c8835945b7) [](/what-is-blockchain-and-why-all-programmers-should-know-about-it-897d73c24a75) [## 什么是区块链，为什么所有程序员都应该了解它

### 一篇关于区块链的信息性文章。

javascript.plainenglish.io](/what-is-blockchain-and-why-all-programmers-should-know-about-it-897d73c24a75) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)