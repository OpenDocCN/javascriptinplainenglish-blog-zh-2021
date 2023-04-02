# JavaScript 挑战:比较三元组(HackerRank 挑战)

> 原文：<https://javascript.plainenglish.io/javascript-challenge-compare-the-triplets-hackerrank-challenge-98af70c2cd5e?source=collection_archive---------8----------------------->

## HackerRank 比较三胞胎挑战的解决方案

![](img/dd6af8df21cd537b89f088dfa73db20e.png)

Photo by [GR Stocks](https://unsplash.com/@grstocks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这个挑战中，我们将解决名为“比较三胞胎”的黑客挑战。这个挑战在平台上有一个简单的难度级别。

## **挑战。**

Alice 和 Bob 各给 HackerRank 出了一个难题。评审员对这两个挑战进行评分，按照从 *1* 到 *100* 的等级给三个类别打分:*问题清晰度*、*创意*和*难度*。

爱丽丝挑战的评分是三元组 *a = (a[0]，a[1]，a[2])* ，鲍勃挑战的评分是三元组 *b = (b[0]，b[1]，b[2])* 。

任务是通过比较 *a[0]* 与 *b[0]* 、 *a[1]* 与 *b[1]* 、 *a[2]* 与 *b[2]* 找到他们的*比较点。*

*   如果 *a【我】> b【我】*，那么爱丽丝被授予 *1* 点。
*   如果*a【I】<b【I】*，那么 Bob 被奖励 *1* 点。
*   如果 *a[i] = b[i]* ，那么两个人都得不到一分。

比较分数是一个人获得的总分数。

给定 *a* 和 *b* ，确定各自的比较点。

**示例**

*a = [1，2，3]*

*b = [3，2，1]*

*   对于元素*0*，Bob 获得一个点，因为 *a[0]。*
*   *对于相等的元素 a[1]和 b[1]，不计分。*
*   *最后，对于元素 2，a[2] > b[2]所以爱丽丝得到一分。*
*   *返回数组为[1，1]爱丽丝的分数第一，鲍勃的分数第二。*

为了更好地解决这个问题，我们将采用约翰·约翰逊的方法，首先解决问题。然后，编写代码。

实施这种方法将使我们能够理解正在讨论的问题，并使我们能够想出解决它的更好的方法。这样，与直接进入代码相比，编写代码会容易得多。

## **让我们先解决问题**

Bob 和 Alice 正在接受一项挑战，这项挑战将从三个不同的方面(清晰度、创意和难度)对他们进行测试。他们的三个挑战的结果呈现在代表三个测试类别的三(3)个值的数组中。

现在我们的任务是比较 Bob 和 Alice 在三个不同类别中的表现。

用简单得多的方法，我们必须比较两个人的索引为 0 的数组。然后，我们再次比较他们在指数 1 和指数 2 上的表现。

**注意:**

*   当爱丽丝的 ***数组【0】***大于鲍勃的 ***数组【0】***时，我们奖励爱丽丝 1 点，反之亦然。
*   如果他们的价值相等，或者换句话说，他们平手，我们不会奖励他们任何一个人一分。
*   最后，我们将返回 Alive 和 Bob 之间的分数数组。

现在，我们将创建一个函数，它接收两个数组，并将它们相互比较，然后根据谁赢了给谁一分。

## **现在让我们编写代码**

进一步解释。我们已经声明了 ***alicePoint*** 和 ***bobPoint*** 来根据不同类别中谁获胜来存储商店。然后在 for 循环之后，我们遍历任意数组，因为我们知道两个数组长度相等。

该阵列将迭代和比较给定的指数，并有效地增加点，谁赢了，如果他们平手点奖励没有点。

然后我们会创建一个空数组，分别推送 Alice 和 Bob 的点。我们只需返回 ***finalArray*** 就可以了。

如果你想尝试挑战。你可以在这里 查看一下 [***。***](https://www.hackerrank.com/challenges/compare-the-triplets/problem)

## **结论**

感谢您通读我的解决方案。希望对你有帮助。

你认为我们可以添加什么或者如何进一步重构它？

如果你觉得我的内容有用，而你不是媒体成员，你可以在这里(媒体推荐链接)获得你的媒体成员资格[，以获得对所有内容的无限制访问，并作为作者支持我们。](https://amjohnphilip.medium.com/membership)

## **更读**

[](/javascript-data-structures-stack-implementation-bb85141a3f78) [## JavaScript 数据结构:堆栈实现

### JavaScript 中栈数据结构的实现

javascript.plainenglish.io](/javascript-data-structures-stack-implementation-bb85141a3f78) [](/javascript-challenge-check-if-two-strings-are-anagrams-e2efe65c6ef) [## JavaScript 挑战:检查两个字符串是否是字谜

### 检查两个字符串是否是字谜的 JavaScript 挑战

javascript.plainenglish.io](/javascript-challenge-check-if-two-strings-are-anagrams-e2efe65c6ef) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)