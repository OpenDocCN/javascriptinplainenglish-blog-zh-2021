# JavaScript 挑战:给学生评分(HackerRank 挑战)

> 原文：<https://javascript.plainenglish.io/javascript-challenge-grading-students-hackerrank-challenge-763d65135364?source=collection_archive---------2----------------------->

## 了解如何解决分级学生面试准备的挑战

![](img/31979a3adf29f92c42efa3eab2245878.png)

Photo by [Zoran Borojevic](https://unsplash.com/@fresh_studio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这个挑战中，我们将学习如何解决来自 HackerRank 的算法挑战。这个挑战在平台上被标上了 easy 的难度等级。

## **挑战**

哈克兰大学有以下评分政策:

每个学生都会得到一个从 0 到 100 的分数。

任何低于 40 分的分数都是不及格。

Sam 是大学的教授，他喜欢按照以下规则对每个学生进行分组:

如果等级与下一个 5 的倍数之差小于 3，则将等级向上舍入到下一个 5 的倍数。

如果等级的值小于 38，则不会进行舍入，因为结果仍然是不及格等级。

例子

*   舍入到(85–84 小于 3)
*   不舍入(结果小于 40)
*   不要四舍五入(60–57 等于 3 或更高)

给定 Sam 的 n 个学生中每一个的年级初始值，编写代码来自动完成舍入过程。

## **功能描述**

在下面的编辑器中完成**学生评分**功能。

gradingStudents 具有以下参数:

int grades[n]:舍入前的等级

返回

int[n]:适当舍入后的等级

## **解决问题**

首先，让我们更好地理解问题想从我们这里得到什么。我们给学生打分，通知他们一个整数数组。

根据给定的整数，我们应该给学生打分。从分数来看，如果一个学生的分数低于 38，我们不会把他的分数四舍五入。

当学生的分数与 5 的倍数之差小于 3 时，我们将分数四舍五入到下一个 5 的倍数。

举个例子，如果分数= 43，我们应该把它四舍五入到 45。因此，如果 grade-(grade % 5)小于 2，则不进行四舍五入。记住，如果 5 和余数之差小于 3，我们将把它四舍五入到 5 的下一个倍数。

同样，我们应该返回最终的舍入数组。

首先，我们可以遍历数组，然后找出给定数组的余数与 5 的差。

之后就可以做测试条件，检查成绩是否大于 38，差是否大于 3。如果条件为真，我们将差额加到成绩上。

然后我们可以返回处理过的数组。

## **编写代码**

## **结论**

感谢您查看此解决方案。希望对你有帮助。

你认为我们可以添加什么或者如何进一步重构它？

如果你觉得我的内容有用，而你不是媒体会员，你可以在这里[获得你的媒体会员资格](https://amjohnphilip.medium.com/membership)(媒体推荐链接)以无限制地访问所有内容并支持我们作为作者。

**更多阅读**

[](/javascript-challenge-sales-by-match-hackerrank-challenge-708fd140bf31) [## JavaScript 挑战:按匹配销售(HackerRank 挑战)

### 了解如何解决 HackerRank 的面试准备挑战

javascript.plainenglish.io](/javascript-challenge-sales-by-match-hackerrank-challenge-708fd140bf31) [](/how-to-configure-dependabot-in-a-nuxt-js-project-cb4d19953364) [## 如何在 Nuxt.js 项目中配置 Dependabot

### 使用 Dependabot 自动更新您的依赖项

javascript.plainenglish.io](/how-to-configure-dependabot-in-a-nuxt-js-project-cb4d19953364) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)