# JavaScript 基础:迭代对象的 4 种不同方法

> 原文：<https://javascript.plainenglish.io/javascript-basics-4-different-ways-to-iterate-over-an-object-a5d16335cef?source=collection_archive---------14----------------------->

## JavaScript 备忘单 2021

## 两分钟内掌握 JavaScript 基础知识。

![](img/dff9aa4ee987c30aaedf9514b22ba724.png)

Photo by [Pierre Bamin](https://unsplash.com/@bamin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我为日常前端开发创建了一些技巧。

这是一篇新文章，介绍了迭代对象和获取键值对的一些方法。这些技巧可以被认为是最终将帮助你在 2021 年跨过 JavaScript 编码面试这条河的小石头。

> 我知道小石头没多大作用，但如果我们有成千上万块这样的石头，它们就会起作用。这就是为什么我明天会带来新的石头。敬请关注。😉

# 我们如何在 JavaScript 中迭代一个对象并获得键值对？

JavaScript 中有四种不同的方法可以迭代任何对象。

## Object.values()

这个方法从对象的值返回一个数组。它的工作顺序与对象的值相同。

```
const obj1 = {
    test1: 'atit',
    test2: 53,
    test3: false,
};
console.log(Object.values(obj1));
// expected output: Array ["atit", 53, false]
```

## Object.keys()

此方法返回对象的键名数组。

```
const obj1 = {
    test1: 'atit',
    test2: 53,
    test3: false,
};
console.log(Object.keys(obj1));
// expected output: Array ["test1", "test2", "test3"]
```

## Object.entries()

这个方法返回一个对象的`[key, value]`对的数组。

```
const obj1 = {
    test1: 'atit',
    test2: 53,
    test3: false,
};for (let [key, value] of Object.entries(obj1)) {
    console.log(key, value);
}
//test1 atit
//test2 53
//test3 false
```

我们也可以使用 **hasOwnProperty** 来检查对象中是否存在这个键。

```
for (let key in obj1) {
    if (obj1.hasOwnProperty(key)) {
        console.log(key, obj1[key]);
    }
}
//test1 atit
//test2 53
//test3 false
```

## Object.fromEntries()

此方法将键值对列表转换为对象。

```
const test = new Map([
  ['atit', '51'],
  ['patel', 52]
]);const obj1 = Object.fromEntries(test);console.log(obj1);
// expected output: Object { atit: 51, patel: 52 }
```

## 如果你喜欢并想获得更多这样的内容，请点击[订阅](https://medium.com/@patel_ap/membership)

# 延伸阅读:

[](/javascript-basics-what-is-the-difference-between-splice-and-slice-fa47b80796c9) [## JavaScript 基础:拼接和切片有什么区别？

### 两分钟内掌握 JavaScript 基础知识。

javascript.plainenglish.io](/javascript-basics-what-is-the-difference-between-splice-and-slice-fa47b80796c9) [](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [## 2021 年你应该知道的 JavaScript 顶级优化技术

### 使用现代速记技术、技巧和诀窍优化您的 JavaScript 代码。

javascript.plainenglish.io](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [## 新引入的 JavaScript 特性可以提升您的知识

### 利用 ES2021 的新功能优化您的 JavaScript 代码。

javascript.plainenglish.io](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)