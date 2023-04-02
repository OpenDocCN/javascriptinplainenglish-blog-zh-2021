# 如何在 JavaScript 中对对象数组进行排序

> 原文：<https://javascript.plainenglish.io/how-to-sort-an-array-of-objects-in-javascript-8cfaebaec251?source=collection_archive---------4----------------------->

## 对一组对象进行排序的技术——日常 JavaScript 技巧、窍门和最佳实践。

![](img/bdb4228a3bd4a58448d493b86c189d04.png)

Photo by [Alex Block](https://unsplash.com/@alexblock?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在短时间内提供足够信息的东西。怀着类似的目标，我为日常前端开发创建了一些技巧。

这是我的一篇新文章，讲述了基于属性值对数组进行排序的一些方法。这些技巧可以是一些小石头，放在一起可以帮助你在 2021 年穿越 JavaScript 编码面试的河流。

> 我知道单个的小石头没什么大不了的，但是如果我们设法收集成千上万的石头，它们就会有所作为。

> *开始今天的话题吧。*

如果我们需要根据给定的有序列表对一组对象进行排序，这个实用函数会非常有用。

让我们检查我们想要排序的样本数据和订单列表。

```
const users = [{
        key: "A",
        name: "atit"
    },
    {
        key: "B",
        name: "patel"
    },
    {
        key: "C",
        name: "toronto"
    }
];const orderList = ["A", "B", "C"];
```

## 1.使用 reduce

使用 reduce，我们可以获取所提到的顺序列表的键，并可以将它们存储在 temp 值中，最后再次映射整个数组。

```
const sortByList = (list, arr) => {
    const tmpMap = arr.reduce((acc, item) => {
        acc[item.key] = item;
        return acc;
    }, {});return list.map(key => tmpMap[key]);
};console.log(JSON.stringify(sortByList(orderList, users)));//[{"key":"A","name":"atit"},{"key":"B","name":"patel"},{"key":"C","name":"toronto"}]
```

## 2.使用来自条目

该方法将一个键值对列表转换成一个对象，我们可以通过比较两个数组来对对象进行排序。

```
sortByList1 = (list, arr) => {
    const order = Object.fromEntries(list.map((k, i) => [k, i]));
    return arr.sort((a, b) => order[a.key] - order[b.key]);
};const orderList1 = ["B", "A", "C"];
console.log(JSON.stringify(sortByList1(orderList1, users)));//[{"key":"B","name":"patel"},{"key":"A","name":"atit"},{"key":"C","name":"toronto"}]
```

**你可以在这里查看我以前的文章:**

*更多内容请看*[***plain English . io***](http://plainenglish.io/)