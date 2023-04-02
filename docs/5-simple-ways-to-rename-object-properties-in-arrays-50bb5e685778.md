# 在 JavaScript 数组中重命名对象属性的 5 种简单方法

> 原文：<https://javascript.plainenglish.io/5-simple-ways-to-rename-object-properties-in-arrays-50bb5e685778?source=collection_archive---------1----------------------->

## JAVASCRIPT 备忘单 2021

## 如何在 JavaScript 中重命名对象数组中的键？

![](img/862c4414ef3bf456aeffcc9ce7a34f1a.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名开发人员，很难记住语法、方法和其他东西。当你工作或编码时，手边有一个列表是很好的。

出于这个原因，我想出了一些在需要时可以派上用场的文章(这样你就可以保存它们)。

今天，我们将讨论对数组中的项目进行排序的不同方法。

# 1.使用地图

map 创建一个新的数组，其工作方式与迭代中的每个循环完全相同。

```
let countries = [{ id: 1, name: "india" },{ id: 2, name: "canada" },{ id: 3, name: "america" }];const transformed = countries.map(({ id, name }) => ({label: id,value: name}));console.log("1", JSON.stringify(transformed));[{"label":1,"value":"india"},{"label":2,"value":"canada"},{"label":3,"value":"america"}]
```

# 2.使用带参数的地图

```
const transformed2 = countries.map(({
    id: label,
    name: value
}) => ({
    label,
    value
}));console.log("2", JSON.stringify(transformed2));[{"label":1,"value":"india"},{"label":2,"value":"canada"},{"label":3,"value":"america"}]
```

# 3.使用 lodash

```
const test1= _.mapKeys({ a: 1, b: 2 }, function(value, key) {return key + value;});console.log("3",test1);
//*{a1: 1, b2: 2}*
```

如果我们想重命名对象键呢？让我们来看看解决方案。

# 4.对值的对象使用 lodash

```
var users = {'atit':    { 'user': 'atit',    'age': 40 },'mahesh': { 'user': 'mahesh', 'age': 15 }};const test2 = _.mapValues(users, function(o) { return o.age; });console.log("4",test2);
//*{atit: 40, mahesh: 15}*//shorthandconst test3 =_.mapValues(users, 'age');console.log("5",test3);
//*{atit: 40, mahesh: 15}*
```

# 5.使用对象析构

```
const rename = (({id: a_b_c, ...rest}) => ({a_b_c, ...rest}))console.log(rename({id: 1, val: 2}))
//*{a_b_c: 1, val: 2}*
```

# 你可以看看我以前的文章

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)