# JavaScript 数组参考备忘单和细目分类—统计

> 原文：<https://javascript.plainenglish.io/javascript-arrays-reference-cheat-sheet-and-breakdown-stats-f0cae8416de?source=collection_archive---------10----------------------->

## 数组概述和方法分解。一些统计数据可以更好地组织数组方法以及每个方法的用法。

![](img/acca7563a8b112ededc1d50300992fc2.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一个 3 部分数组系列，1 部分数据，1 部分突变方法，1 部分非突变方法。这是本系列的第 1 部分。

第 2 部分: [JavaScript 数组引用备忘单和分解——变异方法](/javascript-arrays-reference-cheat-sheet-and-breakdown-mutating-methods-e89a3b0c7755)

第 3 部分: [JavaScript 数组引用备忘单和分解——非变异方法](/javascript-arrays-reference-cheat-sheet-and-breakdown-non-mutating-methods-c95288942800)

数组是包含一系列有序元素的数据结构，每个元素都有自己的编号索引。Array 对象上的方法被设计用来遍历(移动)和改变(改变)数组。

这些方法的大多数常见操作包括创建数组、在数组中添加和移除项、循环访问数组、查找数组中的特定元素、查找数组中的特定索引位置以及复制数组。

这些方法可以分为两类，不管它们是否改变了原始数组。一般来说，最好不要改变原始数组，大多数方法都不会改变原始数组。方法本身要么接受参数，要么不接受参数。方法还返回一个新数组、单值、字符串、布尔值、一个索引值、一个数组迭代器、length 属性、undefined 和 nothing(就地修改)。

总共有 31 个数组方法。
**注:方法参考自 MDN，不包含实验性或已弃用的方法。*

此外，只分解 Array.prototype 对象上的方法。
如果算上数组全局对象上的方法，总共有 34 个方法。

9 种方法变异了数组(29%)
22 种方法没有变异数组(71%)

21 个方法带参数(68%)
10 个方法不带参数(32%)

粗略地说，所有数组方法中大约有 2/3 的方法接受参数，并且不改变数组。

## 变异方法:

超过一半(56%)的变异方法涉及到在数组中添加或删除元素。

5 个方法接受参数(56%)
4 个方法不接受参数(44%)

5 个方法不返回值，而是改变数组*的内容并返回新的修改后的数组(56%)
4 个方法返回某种类型的值(44%)*

2 个方法返回值(22%)。

2 方法返回新数组的长度(22%)。

一般来说，大多数变异方法会接受一些参数，并且大多数方法会在适当的位置改变数组*的内容。*

## 5 个就地返回修改过的数组的方法

。copyWithin()
。fill()
。反向()
。sort()
。拼接()

## 2 个返回值的方法:

。pop()
。shift()

## 2 个返回数组新长度的方法

。推送()
。未移位()

## 非突变方法:

22 方法不改变数组。

这些方法会制作副本，并且会返回…

*   未定义的值(1)
*   一个新的阵列(6)
*   单一值(3)
*   弦乐(3)
*   布尔型(3)
*   一个索引值(3)
*   数组迭代器(3)

4 种方法不接受论点(18%)
18 种方法接受论点(82%)。

大多数数组方法都会接受某种类型的参数，无论是值还是回调函数。

在 18 个接受参数的方法中…
8 个接受值(44%)
10 个接受回调函数(56%)。

可以有把握地说，大约一半接受参数的方法要么是某种类型的值，要么是回调函数。

这 3 个方法是数组全局对象的一部分，虽然在最后会涉及到它们，但它们并不包含在统计数据中。原因是这里计算的方法是 Array.prototype 对象的一部分。

## 1 个返回未定义的方法:

。forEach()

## 6 个返回新数组的方法:

。concat()
。filter()
。map()
。slice()
。
平()。平面地图()

## 允许您搜索索引的 3 种方法:

。findIndex()
。indexOf()
。lastIndexOf()

## 3 个返回布尔值的方法:

。每()
。包含()
。一些()

## 3 个返回单个值的方法

。find()
。reduce()
。reduceRight()

## 3 个返回字符串的方法

。join()
。toLocaleString()
。toString()

## 3 个返回数组迭代器的方法

。条目()
。按键()
。值()

## 数组全局对象上的 3 个方法:

。
出自()。
(isArray)。属于()

# 阵列版本

JavaScript 作为一种语言，自诞生以来一直在不断发展，新的特性也在不断增加。早在 1995 年首次创建 JavaScript 时，并不是所有的数组方法都是一次性发布的。JavaScript 有多个版本，它们通过 EcmaScript 规范继续这样做，EcmaScript 规范被称为 ESNext。这些数组是按照每个数组方法发布的时间顺序排列的。

## ES1 — ECMAScript 1997:

*   Array.prototype.toString()
*   Array.prototype.join()
*   Array.prototype .反转()
*   Array.prototype.sort()

## ES2 — ECMAScript 1998:

## ES3 — ECMAScript 1999:

*   Array.prototype.toLocaleString()
*   Array.prototype.concat()
*   Array.prototype.pop()
*   Array.prototype.push()
*   Array.prototype.shift()
*   Array.prototype.slice()
*   Array.prototype.splice()
*   。未移位()

## ES5 — ECMAScript 2009:

*   Array.isArray()
*   Array.prototype.indexOf()
*   Array.prototype.lastIndexOf()
*   Array.prototype.every()
*   Array.prototype.some()
*   Array.prototype.forEach()
*   Array.prototype.map()
*   Array.prototype.filter()
*   Array.prototype.reduce()
*   Array.prototype.reduceRight()

## ES6 — ECMAScript 2015:

*   数组. from()
*   的数组()
*   Array.prototype.copyWithin()
*   数组.原型.条目()
*   Array.prototype.fill()
*   Array.prototype.find()
*   Array.prototype.findIndex()
*   array . prototype . key()
*   Array.prototype.values()

## ES7 — ECMAScript 2016

*   Array.prototype.includes()

## ES8 — ECMAScript 2017:

## ES9 — ECMAScript 2018:

## ES10 — ECMAScript 2019:

*   Array.prototype.flat()
*   Array.prototype.flatMap()

## ES11 — ECMAScript 2020:

## ES12 — ECMAScript 2021:

我们找到了。数组的快速概述您可以使用参考或备忘单。随着每个后续 ESNext 版本中更多数组的发布，数组方法也将得到更新。希望这有助于任何开发人员的参考！

*更多内容看*[***plain English . io***](http://plainenglish.io/)