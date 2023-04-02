# JavaScript 基础知识:在数组中插入项目的最佳方式

> 原文：<https://javascript.plainenglish.io/javascript-basics-the-best-way-to-insert-items-in-an-array-799346aed944?source=collection_archive---------13----------------------->

## JavaScript 备忘单 2021

## 两分钟内掌握 JavaScript 基础知识。

![](img/41a6cb2c08b3d94e313d160e4aae131a.png)

Photo by [Michael Longmire](https://unsplash.com/@f7photo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我过去总是喜欢像报纸这样能在短时间内提供足够信息的东西。怀着类似的目的，在这里，我为日常前端开发创建一些技巧。

这是一篇介绍在数组中插入值的基本方法的新文章。这些技巧可以被认为是小垫脚石，最终将为你在 2021 年穿越 JavaScript 编码面试的汹涌水域铺平道路。

> *我知道小石头没什么区别；但是如果我们有几千块这样的石头，他们可能会。所以我明天会带着新石头回来。敬请关注。😉*

# 数组插入方法

当您知道想要在哪个索引处插入项目时，这种方法非常有用(*注意:*在内部，拼接方法可以创造奇迹)。

```
Array.prototype.insert = function(index, item) {
    this.splice(index, 0, item);
};let arr = ['test1', 'test2', 'test3', 'test4'];arr.insert(2, 'test5');console.log(arr);
// => arr == [ 'test1', 'test2', 'test5', 'test3', 'test4' ]
```

# 拼接方法

如果需要，splice 方法可以帮助指定带有删除计数的索引。

```
let data = ["abc", "cde", "efg"]
data.splice(2, 0, 'newval');console.log(data); //["abc", "cde", "newval", "efg"]
```

# 传播算子

spread 运算符可用于创建一个带引用的新数组。

```
const items = [10, 20, 30, 40, 50]
let result = [...items, 100];console.log(result)
// [10, 100, 20, 30, 40, 50]
```

# 如果你想在第一个位置插入一个项目呢？

这可以通过 unshift 和 concat 方法来实现。

会创建一个新的数组，它可以这样写。

```
const val = [30, 2, 1]const data = 4const test = [data].concat(val) // [ 4, 30, 2, 1 ]console.log(test); //[4, 30, 2, 1]
```

`unshift`是将任意值加到第 0 个元素，并将其他元素移位。

```
val.unshift(4);
console.log(val); //[4, 30, 2, 1]
```

# 如果要在最后一个位置插入一个项目呢？

推送是最常见的方法之一，但在此值得一提。

```
const val = [30, 2, 1]val.push(4);//[30,2,1,4]
```

**注意:** Concat 和 spread 运算符以非变异方式插入项目。

## 如果你喜欢并想得到更多这样的内容，请考虑订阅[。](https://medium.com/@patel_ap/membership)

# 延伸阅读:

[](/5-cool-javascript-features-you-might-not-know-about-yet-f2fc818bdd31) [## 你可能还不知道的 10 个很酷的 JavaScript 特性

### 优化代码的 JavaScript 特性。

javascript.plainenglish.io](/5-cool-javascript-features-you-might-not-know-about-yet-f2fc818bdd31) [](/javascript-basics-4-different-ways-to-iterate-over-an-object-a5d16335cef) [## JavaScript 基础:迭代对象的 4 种不同方法

### 两分钟内掌握 JavaScript 基础知识。

javascript.plainenglish.io](/javascript-basics-4-different-ways-to-iterate-over-an-object-a5d16335cef) [](/javascript-basics-what-is-the-difference-between-splice-and-slice-fa47b80796c9) [## JavaScript 基础:拼接和切片有什么区别？

### 两分钟内掌握 JavaScript 基础知识。

javascript.plainenglish.io](/javascript-basics-what-is-the-difference-between-splice-and-slice-fa47b80796c9) [](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [## 2021 年你应该知道的 JavaScript 顶级优化技术

### 使用现代速记技术、技巧和诀窍优化您的 JavaScript 代码。

javascript.plainenglish.io](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [## 新引入的 JavaScript 特性可以提升您的知识

### 利用 ES2021 的新功能优化您的 JavaScript 代码。

javascript.plainenglish.io](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)