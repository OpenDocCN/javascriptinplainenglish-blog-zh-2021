# 如何移除 JavaScript 数组中的重复对象

> 原文：<https://javascript.plainenglish.io/removing-duplicate-objects-in-a-javascript-array-c555dbc7bc54?source=collection_archive---------5----------------------->

## React-Redux、Reducers 和 Sets

## 借助字典过滤数据

![](img/b04533aff6ce45a994298e4ab2d43f00.png)

Photo by [Piotr Łaskawski](https://unsplash.com/@tot87?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/scrabble?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在过去的一周里，我在处理应用程序的 reducer 逻辑时遇到了一个问题。我需要确保 reducer 没有向 state 添加重复的数据。通常，我会利用一个`Set`来删除任何重复的值，但是从我的 API 返回的数据是一个 JavaScript 对象数组。

`Set`可以删除数组中同一对象的*的任何副本，但*无法检测到不同对象具有相同的键和值*。*

How set works with JS objects

# 迭代:一种不太理想的方法

一种简单的方法是利用嵌套循环遍历集合，检查整个集合中的每个元素，看是否存在重复的元素。这导致时间复杂度为 O(n ),效率低得可怜。

Don’t do this

# 该买字典了

虽然 JavaScript 缺乏真正的`Dictionary`数据结构，但是可以很容易地实现为普通的旧 JavaScript 对象。通过将每个对象的 ID 作为一个键，并将值指定为`true`，我可以在遍历元素一次时跳过任何重复的元素，从而获得 O(n)的时间复杂度。

An improved algorithm

# 优化 Redux

最后一步是为 Redux 优化一切。虽然上面的算法可以工作，但我决定将字典存储在 state 中，允许 reducer 只检查由我的 API 调用返回的新对象。这减少了解析新数据所需的迭代次数，同时只略微增加了内存使用量(具有`strings`和`booleans`的键/值对的字典占用相对较少的空间)。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)