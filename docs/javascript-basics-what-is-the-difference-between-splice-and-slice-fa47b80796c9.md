# JavaScript 基础:拼接和切片有什么区别？

> 原文：<https://javascript.plainenglish.io/javascript-basics-what-is-the-difference-between-splice-and-slice-fa47b80796c9?source=collection_archive---------11----------------------->

## JavaScript 备忘单 2021

## 两分钟内掌握 JavaScript 基础知识。

![](img/ccab210c96c02aa5c3f1472aa3c4e422.png)

Photo by [Kabir Kotwal](https://unsplash.com/@photo_scientist?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我为日常前端开发创建了一些技巧。

这是一篇新文章，介绍了 JavaScript 中 splice 和 slice 方法的区别。这些技巧可以被认为是最终将帮助你在 2021 年跨过 JavaScript 编码面试这条河的小石头。

> 我知道小石头没多大作用，但如果我们有成千上万块这样的石头，它们就有作用了。这就是为什么我明天会带来新的石头。敬请关注。😉

# JavaScript 中的切片与拼接

让我们检查一下这两种方法，以了解它们的区别。

## 切片()

Slice()用于对数组中的值进行切片。在这里，我们可以定义开始和结束位置。

```
var data = ['atit','patel','toronto'];console.log(data.slice(2));// *["toronto"]*var data1 = ['atit','patel','toronto'];
console.log(data1.slice(1, 2));
//*["patel"]*
```

## 拼接()

Splice()的工作方式完全相同，我们可以传递索引来从数组中删除项目。

```
var data2 = ['atit', 'patel', 'toronto'];console.log(data2.splice(2));// *["toronto"]*
```

# 那有什么区别呢？

*   唯一的区别是 Splice()修改了原始数组，而 Slice()返回新数组。

## 让我们看看在执行这两种方法后，与原始数组的区别。

## 切片:

```
var data = ['atit', 'patel', 'toronto'];console.log(data.slice(2)); //["toronto"]console.log(data); //["atit", "patel", "toronto"]
```

## 拼接:

```
var data2 = ['atit', 'patel', 'toronto'];console.log(data2.splice(2)); //["toronto"]console.log(data2); //["atit", "patel"]
```

# 延伸阅读:

[](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [## 2021 年你应该知道的 JavaScript 顶级优化技术

### 使用现代速记技术、技巧和诀窍优化您的 JavaScript 代码。

javascript.plainenglish.io](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [## 新引入的 JavaScript 特性可以提升您的知识

### 利用 ES2021 的新功能优化您的 JavaScript 代码。

javascript.plainenglish.io](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)