# JavaScript 中高阶函数的介绍

> 原文：<https://javascript.plainenglish.io/intro-to-higher-order-functions-in-javascript-1ec23a2a28cf?source=collection_archive---------12----------------------->

## 使用通用数组函数

![](img/8191abdcb4d4833794c3dc72d44658be.png)

JavaScript 中最重要的技能之一是理解高阶函数和回调函数是如何工作的。简单地说，高阶函数是这样的函数:

1.  将不同的函数作为参数**和/或**
2.  返回一个新函数。

就是这样。回调函数就是被传入的函数。这些复合词隐藏了简单的概念。例如，这基本上是所有`forEach`做的事情:

```
const **fakeForEach** = (**arr**, **callbackFunction**) => {
  for (let **i** = 0; **i** < **arr**.length; **i**++) {
    const **value** = **arr**[**i**]
    const **index** = **i**;
    const **givenArr** = **arr**;
    **callbackFunction**(**value**, **index**, **givenArr**)
  }
}

const **myArr** = [*'a', 'b', 'c'*]
const **myCallback** = (**val**, **idx**, **arr**) => {
  **console**.log('*Value at index:*', **val**);
  **console**.log('*Current index:*', **idx**);
  **console**.log('*Original array*:', **arr**);
};

***// these will log the same things!***
**fakeForEach**(**myArr**, **myCallback**);
**myArr.**forEach(**myCallback**);
```

通过传入一个函数*但不调用它*，我们允许一个更高阶的函数，在这个例子中是`fakeForEach`或`.forEach`在循环的每次迭代中调用回调。现在让我们分解一些 JavaScript 内置的主要高阶数组函数。

当然，你也可以内联定义回调函数，但是在下面的例子中，我显式地创建了一个变量，这样就可以*非常*清楚回调引用了什么。

```
***//* *inline***
**arr**.forEach((**val**) => {
 **console**.log(**val**)
});

***// variable***
const **callback** = (**val**) => {
 **console**.log(**val**)
});
**arr**.forEach(**callback**);

// both are fine!
```

# 。为每一个

## 功能描述

`.forEach`遍历数组，不考虑返回值。如果你需要一个基本的循环或者改变一个现有的对象，这就是你的方法。

## 回拨描述

在每次迭代中，`forEach`的回调接受值、索引和原始数组。忽略所提供的回调的返回值。

```
const **letters** = [*'a', 'b', 'c'*];
const **callback** = (**val**, **idx**, **arr**) => {
 **console.**log('*Value at index:*', **val**);
 **console.**log('*Current index:*', **idx**);
 **console**.log('*Original array:*', **arr**);
};
**letters**.forEach(**callback**);
***// Value at index: a
// Current index: 0
// Original array: [ 'a', 'b', 'c' ]
// Value at index: b
// Current index: 1
// Original array: [ 'a', 'b', 'c' ]
// Value at index: c
// Current index: 2
// Original array: [ 'a', 'b', 'c' ]***
```

# 。地图

## 功能描述

`.map`很像`forEach`，除了它构建并返回一个新数组。

## 回拨描述

像`forEach`一样，提供的回调让您可以访问值、索引和原始数组。回调的每个单独的返回值都保存在新数组中。

```
const **numbers** = [10, 20, 30];

const **callback** = (**val**, **idx**, **arr**) => {
 **console.**log('*Value at index:*', **val**);
 **console.**log('*Current index:*', **idx**);
 **console.**log('*Original array:*', **arr**);
  ***return*** **val** * 100;
};
const **bigNumbers** = **numbers**.map(**callback**);

console.log('*bigNumbers*: ', **bigNumbers**);
***// bigNumbers:  [ 1000, 2000, 3000 ]***
```

# 。过滤器

## 功能描述

`filter`用于根据通过条件的值返回一个新数组。

## *回调描述*

回调函数有值、索引和数组，但是有趣的是返回值。如果一次迭代有一个真值返回值，那么该次迭代中数组中的值将被保存到新数组中。

```
const **names** = ['*tom*', '*ezekiel*', '*robert*'];

const **callback** = (**val**, **idx**, **arr**) => {
 ***return* val**.length > 3;
};
const **longNames** = **names**.filter(**callback**);
**console.**log('*longNames*: ', **longNames**);
***// longNames:  [ 'ezekiel', 'robert' ]***
```

# 。一些

## 功能描述

如果数组中至少有一个元素满足给定条件，则`some` 返回布尔值。

## 回拨描述

这是一个标准的价值，指数，数组的情况。然而，与目前为止的其他方法不同，一旦回调返回`true`，`some`将停止遍历数组。那是因为没必要继续下去了。记住，`some`只关心是否至少有一个值，如果你想要*精确的*真值，你应该使用`forEach`并保留一个`count`变量，或者`filter`然后只使用新数组的长度。`some`遍历整个数组的唯一方式是它永远找不到返回真值的值。此时`some`将返回`false`。

```
const **numbers** = [1, 4, 9001, 7, 12];
const **callback** = (**val, idx, arr)** => {
  console.log('*num*: ', **val**);
  return num > 9000;
};
const **isOver9000** = **numbers**.some(**callback**);
***// num:  1
// num:  4
// num:  9001*** 
**console.**log('*isOver9000*: ', **isOver9000**);
***// isOver9000:  true***
```

# 。每个

## 功能描述

`every`返回一个布尔值；`true`如果*数组中的每个*值都通过回调的条件，则`false`否则。

## 回拨描述

回调函数有值、索引和数组，这是我们所熟悉和喜爱的。它的工作方式与`some`完全一样，将返回值评估为 true/falsy。但是，如果单个值返回 falsy，它将放弃迭代，这与`some`相反。这有点像`||`对`&&`短路。

```
const **numbers** = [9001, 9002, 7, 12];

const **callback** = (**val, idx, arr**) => {
  console.log('*num*: ', **num**);
 **return** num > 9000;
}
const **areAllOver9000** = **numbers**.every(**callback**)
***// num:  9001
// num:  9002***

console.log('*areAllOver9000*: ', **areAllOver9000**);
***// areAllOver9000:  false***
```

# 更复杂的迭代器

接下来的方法与回调的`val, idx, arr`模式有些不同，稍微复杂一些。因此，让我们更深入地解释一下。

# 。减少(基本使用案例)

该方法将一组值简化为一个值。提供的回调的第一个参数是`accumulator`。第二个参数是`current value`。`reduce`的主要技巧是无论迭代器从一次迭代中返回什么，都将成为下一次迭代的`accumulator`。`reduce`的最终返回值是`accumulator`在最后一次迭代中建立起来的值。

## 第一次迭代呢？

`reduce`有一个可选的但强烈推荐的第二个参数，它为`accumulator`设置了`initial value`。如果没有提供初始值，`reduce`实际上将取数组的第一个值，将其视为`initial value`，将数组中的第二个值视为`current value`。一般来说，你应该总是提供一个`initial value`，因为它会导致更少的错误。

```
const **numbers** = [12,8,23,5];
const **startingVal** = 0;
const **callback** = (**accumulator**, **currentVal**) => {
  **console**.log('*Accumulator*', **accumulator**);
  **console**.log('*Value at index:*', **currentVal**);
 ***// console.log('Current index:', idx);
  // console.log('Original array:', arr);***
 ** *return* accumulator + currentVal**;
}

const **total** = **numbers**.reduce(**callback**, **startingVal**);
***// Accumulator 0
// Value at index: 12
// Accumulator 12
// Value at index: 8
// Accumulator 20
// Value at index: 23
// Accumulator 43
// Value at index: 5***
console.log('total', **total**);
***// total: 48***
```

# 。减少(高级用例)

在一天结束的时候，`reduce`只是把事情加到一个累加器中。但是没人说蓄电池不能...一个物体？？看看如何使用`reduce`来构建一个对象。为了比较，我们做完全相同的事情，但是使用`.forEach`。现在要记住的关键事情是初始值*必须*被显式设置为一个对象。同样，在这种情况下我们不需要它们，但是`idx`和`arr`参数仍然可用。

```
const **arr** = [*'x', 'y', 'z', 'z', 'x', 'z'*];
const **countForEach** = (**arr**) => {
  const **result** = {};
  **arr.**forEach((**letter**) => {
    **result**[**letter**] = (**result**[**letter**]) ? **result**[**letter**] + 1 : 1;
  });
 ***return*** **result**;
};

const **countReduce** = (**arr**) => **arr**.reduce((**acc**, **letter**) => {
  **acc**[**letter**] = **acc**[**letter**] ? **acc**[**letter**] + 1 : 1;
 **return *acc***;
}, {});

**console.**log(**countForEach**(**arr**));
***// { x: 2, y: 1, z: 3 }***
**console**.log(**countReduce**(**arr**));
***// { x: 2, y: 1, z: 3 }***
```

# 。分类

默认的`sort()`方法按照字母顺序对*进行排序。这意味着`[1, 3, 2, 11]`将被归入`[1, 11, 2, 3]`。这并不理想。为了正确地对数字进行排序，您需要传入一个`compare`回调函数。`compare`函数需要返回正数、负数或 0。然后，JS 将使用这些数字来确定值的顺序是否正确。在伪代码中，您会看到一个具有以下条件的函数:*

```
*const compare = (a, b) => {
  if (a is less than b by some ordering criterion) {
    return a negative number;
  }
  if (a is greater than b by the ordering criterion) {
    return a positive number;
  }
  // a must be equal to b
  return 0;
}*
```

这是一个*非常*的手动设置，可能对非数值排序有用。然而，如果你比较的是数值，你可以用一个*非常简单的回调来完成同样的事情:*

```
// sorts smallest to biggest (ascending)
let **compare** = (**a, b**) => **a - b**;
// sorts biggest to smallest (descending)
**compare** = (**a, b**) => **b - a**;
```

用于上下文中，`sort`看起来是这样。

```
const **numbers** = [4, 2, 5, 1, 3];
**numbers**.sort((**a, b**) => **a - b**); 
**console**.log('*numbers:*', **numbers**);
**// [ 1, 2, 3, 4, 5 ]**
```

compare 函数也可以轻松地处理对象，只需访问所需的任何属性。

```
const **houses** = [
  { color: *'blue'*, price: 350000 },
  { color: '*red*', price: 470000 },
  { color: '*pink*', price: 280000 },
];
**houses.**sort((**a, b**) => **a**.price - **b**.price);
**console**.log('*houses*:', **houses**);
// houses [
//   { color: 'pink', price: 280000 },
//   { color: 'blue', price: 350000 },
//   { color: 'red', price: 470000 }
// ]
```

这里需要注意的一点是，与这个列表中的其他迭代器函数不同，`**sort**` ***不是纯粹的***；它会改变原来的数组，而不是创建一个新的。

# 更多高阶函数在等着您！

这只是更高层次的山的基础，关于这个概念还有太多需要探索的地方。但是，您现在应该已经很好地掌握了基础知识，我鼓励您打开一个控制台，摆弄一下这些值，直到它成为您的第二天性。

大家编码快乐，

麦克风

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***