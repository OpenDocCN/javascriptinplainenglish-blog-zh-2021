# 如何计算对象数组中相同的属性值

> 原文：<https://javascript.plainenglish.io/how-to-count-the-same-property-values-in-array-of-objects-cc4719c5fc6d?source=collection_archive---------2----------------------->

## 日常 JavaScript 技巧、窍门和最佳实践

![](img/bd2097931a830cc55b69ea517b479741.png)

Photo by [Towfiqu barbhuiya](https://unsplash.com/@towfiqu999999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我为日常前端开发创建了一些技巧。

在这里，我将带来一篇新文章，介绍一些基于属性值对数组进行排序的方法。这些技巧可以成为你 2021 年 JavaScript 编码面试中的一块小石头。

> 我知道小石头没什么区别，但如果我们有成千上万的石头，就有区别了..为此我明天会带来新的石头。敬请期待

> *让我们开始今天的话题*

让我们检查一下当我们想要添加带有一些属性名的对象并想要获得新的对象数组时的场景。

在这个例子中，name 是惟一的属性，如果在对象数组中有多个 name 属性可用，我们希望合并这些顺序。

## ***我们在这里能想到什么逻辑？***

简单的方法是迭代对象数组，检查是否出现相同的名称，以及是否出现修改数组的情况。

```
const users = [{ name: "test1", orders: 20 },{ name: "test2", orders: 8 },{ name: "test1", orders: 8 },{ name: "test4", orders: 10 },{ name: "test3", orders: 30 }];
```

## **1。使用 forEach 方法**

在这里，我们创建一个空数组，迭代后，我们将值。

```
let result = [];users.forEach(function(a) {
    if (!this[a.name]) {
        this[a.name] = {
            name: a.name,
            orders: 0
        };
        result.push(this[a.name]);
    }
    this[a.name].orders += a.orders;
}, Object.create(null));let val = JSON.stringify(result);
console.log(val);
//[{"name":"test1","orders":28},{"name":"test2","orders":8},{"name":"test4","orders":10},{"name":"test3","orders":30}]
```

## **2。使用 reduce**

这里我们对迭代使用 reduce。

```
let result2 = Object.values(
    users.reduce((r, {
        name,
        orders
    }) => {
        r[name] ?? = {
            name,
            count: 0,
            orders: 0
        };
        r[name].count++;
        r[name].orders += orders;
        return r;
    }, {})
);console.log(JSON.stringify(result2));//[{"name":"test1","orders":28},{"name":"test2","orders":8},{"name":"test4","orders":10},{"name":"test3","orders":30}] 
```

## 进一步阅读

*更多内容请看*[***plain English . io***](http://plainenglish.io)