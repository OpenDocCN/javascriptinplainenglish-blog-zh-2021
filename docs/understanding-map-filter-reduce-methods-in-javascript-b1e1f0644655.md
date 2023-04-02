# 理解 JavaScript 中的 Map、Filter & Reduce 方法

> 原文：<https://javascript.plainenglish.io/understanding-map-filter-reduce-methods-in-javascript-b1e1f0644655?source=collection_archive---------9----------------------->

## 详细了解 JavaScript 的 3 种最常用的方法。

![](img/10ab2ea932d776828e5c166cb974e120.png)

[Reach to our website for more logs](http://ihatereading.in/logs)

## 在后台

无论你是一名经验丰富的开发人员还是业余开发人员，在用 JavaScript 编码时，你一定遇到过`map`、`filter`和`reduce`方法。无论您是 Node.js 还是 React 开发人员，理解这些方法都是非常重要的，因为在关于它们的面试中，您会被问到很多问题。

## 入门指南

让我们直接从方法 1 开始。

## 映射方法

map 方法遍历数组的每个元素，并调用您在数组中定义的回调函数。它将总是返回一个数组，并且输出数组将总是与输入数组大小相同。

```
const data = [ 
  { id: 1, name: 'shrey', count: 43 }, 
  { id: 2, name: 'parv', count: 23 }, 
  { id: 3, name: 'Dinesh', count: 58 },
  { id: 4, name: 'Akhil', count: 14 }
];
```

在上面的例子中，`map`函数将迭代数据数组的每个元素，并返回计数为> 30 的元素；否则，它将返回 undefined。

```
data.map(item => if(item.count > 30) { return item })// the output array will be like this
[ 
  { id: 1, name: 'shrey', count: 43 }, 
  { undefined }, 
  { id: 3, name: 'Dinesh', count: 58 },
  { undefined }
]
```

请注意，最终数组的大小将始终保持不变。

## 该过滤方法

顾名思义，filter 方法将过滤输入数组，并将过滤后的子数组作为输出返回。执行筛选和排序时，通常需要此方法。

```
data.filter(item => item.count > 30 );// the output array will be same as those return by map method but size will decrease.[ 
  { id: 1, name: 'shrey', count: 43 }, 
  { id: 3, name: 'Dinesh', count: 58 },
]
```

这比`map`方法要好得多，因为你在最终数组中使用的空间更少，处理更小的数组的速度更快。

## 该简化方法

reduce 方法与 filter 和 map 稍有不同，但它采用回调并迭代每个元素来返回单个值，而不是像上面两种方法那样返回一个数组。

*   reducer 方法获取该元素，并继续向其添加下一个元素，直到到达末尾。
*   它有助于从数组中过滤出单个元素。
*   它有助于对数组进行计算以减少单个值，例如，使用 reduce 方法可以很容易地计算出 4 名学生的总数。
*   它不会改变原始数组

```
data.reduce(*item*  => { if(*item*.count > 30) { return *item* } })// will return { id: 1, name: 'shrey', count: 43 }
```

## 结论

在 JavaScript 世界中，有很多其他处理数组的方法，并且非常容易理解。在今天的故事中，我已经介绍了最常用和被广泛接受的方法。下次再见，祝大家愉快！

```
For more such stories visit our wesbite - 💻 [iHateReading Logs](http://ihatereading.in/logs)
```

*更多内容请看*[***plain English . io***](http://plainenglish.io/)