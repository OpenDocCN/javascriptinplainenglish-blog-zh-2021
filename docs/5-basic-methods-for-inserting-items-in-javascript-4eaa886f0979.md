# 在 JavaScript 中插入项目的 5 种基本方法

> 原文：<https://javascript.plainenglish.io/5-basic-methods-for-inserting-items-in-javascript-4eaa886f0979?source=collection_archive---------10----------------------->

## JavaScript CheatList 2021

## 让你在 2021 年成为专业开发人员的每日 JavaScript 技巧

![](img/2991c76a110c205bae9d2aa70594269f.png)

Photo by [Christopher Robin Ebbinghaus](https://unsplash.com/@cebbbinghaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名开发人员，很难记住语法、方法和其他东西。当你工作或编码时，手边有一个列表是很好的。

出于这个原因，我想出了一些在需要时可以派上用场的文章(这样你就可以保存它们)。

> 今天，我们将讨论在数组中插入项目的不同方法。

# 1.使用数组插入方法

当您知道想要插入哪个索引项时，这种方法很有帮助(注意:在内部，拼接方法产生了奇迹)。

```
Array.prototype.insert = function(index, item) {
    this.splice(index, 0, item);
};let arr = ['test1', 'test2', 'test3', 'test4'];arr.insert(2, 'test5');console.log(arr);
// => arr == [ 'test1', 'test2', 'test5', 'test3', 'test4' ]
```

# 2.使用拼接方法

如果需要，splice 方法可以帮助指定带有删除计数的索引。

```
let data = ["abc", "cde", "efg"]
data.splice(2, 0, 'newval');console.log(data); //["abc", "cde", "newval", "efg"]
```

# 3.使用扩展运算符

spread 运算符可用于创建一个带引用的新数组。

```
const items = [10, 20, 30, 40, 50]
let result = [...items, 100];console.log(result)
// [10, 100, 20, 30, 40, 50]
```

# 4.如果你想在第一个位置插入一个项目呢？

这可以通过 unshift 和 concat 方法实现。

会创建一个新的数组，它可以这样写。

```
const val = [30, 2, 1]const data = 4const test = [data].concat(val) // [ 4, 30, 2, 1 ]console.log(test); //[4, 30, 2, 1]
```

`unshift` 是将任意值加到第 0 个元素，并将其他元素移位。

```
val.unshift(4);
console.log(val); //[4, 30, 2, 1]
```

# 5.如果要在最后一个位置插入一个项目呢？

推送是最常见的方法之一，但在此值得一提。

```
const val = [30, 2, 1]val.push(4);//[30,2,1,4]
```

**注意:** Concat 和 spread 运算符以非变异方式插入项目。

# 进一步阅读

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)