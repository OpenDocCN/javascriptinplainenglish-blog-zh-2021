# JavaScript 挑战:数谷(HackerRank 面试准备)

> 原文：<https://javascript.plainenglish.io/javascript-challenge-counting-valleys-hackerrank-interview-prep-77678218e9c2?source=collection_archive---------6----------------------->

## 了解如何解决计数谷面试准备挑战

![](img/775182ebb08b9272f46e83d0fd5d2e49.png)

Photo by [Michal Vrba](https://unsplash.com/@mis_hik?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本解决方案中，我们将解决 counting valleys HackerRank 挑战。这个挑战在平台上被标记为容易。让我们看看这个挑战以及如何解决它。

## **挑战**

一个狂热的徒步旅行者对他们的徒步旅行做了细致的记录。在最后一次精确走几步的徒步旅行中，每一步都记录了是上坡、 **U** 还是下坡、 **D** 步。徒步旅行总是在海平面开始和结束，每一步上升或下降代表 1 个单位的高度变化。我们定义了以下术语:

*   一座山是一系列高于海平面的连续台阶，从海平面上升一个台阶开始，到海平面下降一个台阶结束。
*   山谷是海平面以下一系列连续的台阶，从海平面以下的台阶开始，到海平面以上的台阶结束。

给定徒步旅行中上下台阶的顺序，找到并打印出走过的山谷数。

**例子**

步骤= **8** ，路径=**【DDUUUUDD】**

徒步旅行者首先进入一个深达两个单位的山谷。然后他们爬出来，爬上一座两个单位高的山。最后，徒步旅行者回到海平面，结束徒步旅行。

**功能描述**

在下面的编辑器中完成**计数山谷**功能。

**计数山谷**有以下参数:

*   int 步数:徒步旅行的步数
*   字符串路径:描述路径的字符串

**退货**

*   int:穿越的山谷数

## **解决问题**

根据上面的挑战，我们要找出一个徒步旅行者在整个徒步旅行经历中走过的山谷的数量。

我们得到了他的步骤的表示。d 代表向下运动，而 U 代表向上运动。为了找到山谷数，徒步旅行者必须先低于海平面，然后再高于海平面。

举个例子，如果徒步旅行者走了 DU 步，这意味着他走下山谷，然后爬回来。这也意味着他超越了一个山谷。简单地说，如果他下去，然后再上来，那么就覆盖了一个山谷。

现在我们如何实现这一点呢？

我们可以遍历提供的路径，在向上移动的情况下增加高度，在向下移动的情况下减少高度。

同样，如果高度是负值，这意味着我们是

## **编写代码**

有了如何应对这一挑战的想法，现在让我们写一些代码。

你可以在这里查看挑战[](https://www.hackerrank.com/challenges/counting-valleys/problem)

***结论***

*感谢您查看此解决方案。希望对你有帮助。*

*你认为我们可以添加什么或者如何进一步重构它？*

*如果你觉得我的内容有用，而你不是媒体会员，你可以在这里[获得你的媒体会员资格](https://amjohnphilip.medium.com/membership)(媒体推荐链接)以无限制地访问所有内容并支持我们作为作者。*

***更多阅读量***

*[](/javascript-challenge-sales-by-match-hackerrank-challenge-708fd140bf31) [## JavaScript 挑战:按匹配销售(HackerRank 挑战)

### 了解如何解决 HackerRank 的面试准备挑战

javascript.plainenglish.io](/javascript-challenge-sales-by-match-hackerrank-challenge-708fd140bf31) [](/harsh-truths-no-one-tells-you-about-programming-1fa6c7a40c2c) [## 没人告诉你关于编程的残酷事实

### 当你进入科技和编程领域时可能会遇到的事情。

javascript.plainenglish.io](/harsh-truths-no-one-tells-you-about-programming-1fa6c7a40c2c) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*