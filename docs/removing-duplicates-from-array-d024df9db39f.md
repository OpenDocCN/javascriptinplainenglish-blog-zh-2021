# 如何从数组中删除重复项

> 原文：<https://javascript.plainenglish.io/removing-duplicates-from-array-d024df9db39f?source=collection_archive---------24----------------------->

在你的下一部 interview✌️中，他们会问你这个问题😁

![](img/dc722f61c05e21bd0ae17e7266af6f79.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 在后台

到目前为止，我的大部分故事都受到了你们所有人的喜爱，我很高兴。大多数读者(包括媒体)的爱帮助我重新定义了我呈现故事的方式。

早些时候，我喜欢写关于 JavaScript 基本方法的故事，谁会阅读它，以及它如何帮助读者。但是，一个大但是！我错了，因为最近，我读了一篇关于用 JavaScript 处理对象的文章，这个 2/3/4 分钟的小故事帮助我提高了我的技能，加快了我的发展。

所以，我认为写关于更大的现实世界问题的小事情只是两个部门，我是谁来判断和过滤它们的权重，如果我关于现实世界问题的故事对市场上的任何开发者都没有帮助，那么写它就没有意义，不是吗？

## 概观

今天的故事将是简短而甜蜜的，问题陈述是从一个数组中删除重复。

```
// [2, 3, 4, 5, 3, 4, 6]
This is an array and our job is to remvoe dublicates from it
```

## 使用 IndexOf 方法

第一种方法是使用 javascript 提供的`indexof`方法删除重复项，如果元素存在，则返回索引，如果不存在，则给出-1 值。

```
const arr = [2, 3, 4, 5, 3, 4, 6, 3, 2];const newArr = arr.filter((item, index) => {
  if(arr.indexOf(item) === index) return item
});
```

我们遍历数组中的每个元素，检查该元素是否存在于整个数组中，并将其推回到新数组中。

## 使用 includes 方法

Javascript 提供了一个`includes`方法，该方法根据数组中元素的可用性返回一个布尔值。

```
const arr = [2, 3, 4, 5, 3, 4, 6, 3, 2];
const newArr = [];arr.forEach(*item* => {
 if(newArr.includes(*item*)) return
 else newArr.push(*item*)
});
```

这种方法已经足够好了，但是它又需要一个数组，因此增加了太多的空间和时间复杂性问题。

## 使用哈希对象

这一部分有点棘手，因为我们知道对象比数组更容易和更快地遍历，并且不会占用太多空间，使用对象而不是数组是很好的解决方法。

```
const arr = [2, 3, 4, 5, 3, 4, 6, 3, 2];
const hashObject = {};arr.forEach(*item* => {
 if(!hashObject[*item*] && hashObject[*item*] !== *item*) hashObject[*item*] = *item*;
  else return
});const newNonDublicatesArr = (Object.keys(hashObject).map(*item* => hashObject[*item*]))
```

这种方法非常快，占用空间少，我们基本上是在传递一个对象中的每个键值，而这个对象在`hashObject`中并不存在。

## 结论

好了，这就是今天的故事，简短而又甜蜜，希望你喜欢。别忘了跟我来，下次再见，祝大家愉快。

```
For more such stories, visit our website - 💻 [**iHateReading**](http://www.ihatereading.in)
```

## 更多阅读

[](/last-4-interviews-and-one-common-question-a479bdc4877b) [## 最后 4 次采访和一个常见问题😁😎

### 如何开发一个具有无限滚动功能的类似 Twitter 的主页

javascript.plainenglish.io](/last-4-interviews-and-one-common-question-a479bdc4877b) [](/4-steps-for-reusable-user-wallet-logic-in-frontend-1626d1cd126a) [## 前端可重用用户钱包逻辑的 4 个步骤

### 一次编写，随时随地使用。😎✌️

javascript.plainenglish.io](/4-steps-for-reusable-user-wallet-logic-in-frontend-1626d1cd126a) [](https://medium.com/geekculture/3-ways-for-the-perfect-onboarding-process-9e3eee47e9d2) [## 完美入职流程的 3 种方式

### 致所有产品经理、设计师和开发人员💬

medium.com](https://medium.com/geekculture/3-ways-for-the-perfect-onboarding-process-9e3eee47e9d2) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)