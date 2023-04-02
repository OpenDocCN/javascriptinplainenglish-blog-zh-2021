# 在用 JavaScript 做 20 多个项目时，我用得最多的 9 个数组方法

> 原文：<https://javascript.plainenglish.io/9-array-methods-that-i-used-the-most-while-making-20-projects-in-javascript-8aa299eb731?source=collection_archive---------8----------------------->

## 除了基本的数组操作和排序。

![](img/a64c5395c8fcd44cb575c5b496490a2c.png)

Photo by [Paul Esch-Laurent](https://unsplash.com/@pinjasaur?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

花了很多时间在后端编程，最后决定学前端。

在学习 JavaScript 的时候，我发现了很多展示大量内容的资源。我想到将 80–20 帕累托原则应用到我的学习中，并决定只学习那些在项目中广泛使用的方法。

我遵循先做后做的方法，一旦我有了基本的知识，就投入到项目中。在过去的几周里，我做了 24 个项目，发现有 9 个数组方法是我用得最多的。

以下是我发现的 JavaScript 中最常用的 9 种方法。

## 1.地图()

在 JavaScript 中，`[map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)`方法是我最喜欢的。它通过遍历数组的元素并应用所需的修改来创建一个新数组。

与`forEach()`方法的[回调函数](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)相比，它不修改原始数组。

```
const foods = ['🍕', '🍔', '🌭', '🍝'];
const foodsWithFries = foods.map(food => food + ' 🍟');console.log(foodsWithFries);// ['🍕 🍟', '🍔 🍟', '🌭 🍟', '🍝 🍟']const numbers = [1, 2, 3, 4];
const squaredNums = numbers.map(num => num ** 2);
console.log(squaredNums); // [1, 4, 9, 16]
```

注意，这里我使用了一个箭头函数来定义回调函数。同一个函数可以用多种方式编写。

```
// 1\. 
const squaredNums = numbers.map(num => num ** 2);// 2\. 
const squaredNums = numbers.map(function(num) {
    return num ** 2;
});// 3\. 
function square(num) {
    return num ** 2;
}const squaredNums = numbers.map(square);
```

## 2.包括()

`includes()`方法在检查所需元素是否出现在数组中后返回一个布尔值。

在使用 API 检查数组中是否存在某个值时，我大量使用了它。

```
const vehicles = ['🚓', '🛺', '🚑', '🚒']
console.log(vehicles.includes('🛺')); // true
console.log(vehicles.includes('🚜')); // false
```

## 3.加入()

当我们想用一些分隔符连接数组的所有元素并返回一个字符串时，就会用到`[join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)`。默认的分隔符(当您不传递任何值作为参数时)是一个`comma (,)`。

```
const animals =['🐇', '🐵', '🐶', '🐴', '🐘'];
animals.join(); // '🐇,🐵,🐶,🐴,🐘'
```

您也可以将自定义分隔符作为参数传入。

```
const animals =['🐇', '🐵', '🐶', '🐴', '🐘'];
animals.join(' < '); // '🐇 < 🐵 < 🐶 < 🐴 < 🐘'
```

当我想在网站上显示带有自定义分隔符的数组元素(使用 DOM 操作)时，我特别使用它。

## 4.查找()

如果元素满足[回调函数](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)中提供的条件，则`find()`方法返回元素的第一个实例。

我用它来检查是否存在满足我的条件的元素。当没有元素满足条件时，函数返回`undefined`。

```
const numbers = [2, 4, 5, 6, 7];const odd = numbers.find(num => num % 2 !== 0);
console.log(odd); // 5const greaterThan12 = numbers.find(num => num > 12);
console.log(greaterThan12); // undefined
```

有一个类似的方法`findIndex()`返回第一个匹配元素的索引，当没有匹配时返回`-1`。

## 5.过滤器()

`[filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)`方法创建一个新的数组，其中的元素满足我们为它指定的条件。该方法采用一个[回调函数](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)，您必须在其中指定条件。

```
const numbers = [4, 2, 6, 9, 10, 13, 5];const evenNumber = numbers.filter(num => num % 2 === 0);
console.log(evenNumber); // [4, 2, 6, 10]
```

这里，`filter` 方法返回了一个包含所有偶数的新数组，因为这是我们的条件。

## 6.减少()

`[reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b)`方法执行一个 reducer 回调函数。就像你在现实生活中加多个数一样。您将从第一个值开始，在逐个添加值的同时迭代其他数字。

`reduce()` 方法做一些类似的事情，最后，你将得到一个单一的值。除了加法之外，它还能做很多你想做的事情。

```
const numbers = [1, 2, 3];
const sum = numbers.reduce( (previousValue, currentValue) => {
    return previousValue + currentValue;
});
console.log(sum); // 6 const vegetables = ['🥒', '🥬', '🥕'];
const salad = vegetables.reduce((prevVeg, ongoingSalad) => {
    return prevVeg + ongoingSalad;
});
console.log(salad); // 🥒🥬🥕
```

`reduce`方法不修改原始数组。

## 7.concat()

`[concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat?v=b)`方法用于合并数组。它返回一个全新的数组，而不修改所提供的任何数组。

```
const vegetables = ['🍅', '🥦', '🥔', '🧄'];
const fruits = ['🍎', '🍉', '🍌'];const food = vegetables.concat(fruits);
console.log(food); // ['🍅', '🥦', '🥔', '🧄', '🍎', '🍉', '🍌'];
```

我们还可以通过使用`concat`方法一次合并多个数组。

```
const vegetables = ['🍅', '🥦'];
const fruits = ['🍎', '🍉'];
const sweets = ['🧁', '🍫', '🍪'];const food = vegetables.concat(fruits, sweets);
console.log(food); // ['🍅', '🥦', '🍎', '🍉', '🧁', '🍫', '🍪'];
```

## 8.切片()

`[slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)`方法用于“切片”数组的一部分。它不会更改原始数组，而是创建数组的新深层副本。

当您不想改变原始数据，而是对阵列进行拷贝/“切片”时，这很有用。

```
const emojis = ['😀', '😁', '🙂', '🤩', '😮', '😇', '😆'];emojis.slice(0, 2); // ['😀', '😁']emojis.slice(3, 6); // ['🤩', '😮', '😇']
```

当我想创建整个数组的深层副本时，我使用的最多的是`slice`。通过使用这个，我可以放心，我没有修改我的原始数组，并可以用新数组做任何操作。

```
const emojis = ['😀', '😁', '🙂'];
const emojisCopy = emojis.slice();emojisCopy.push('🙄');console.log(emojis); // ['😀', '😁', '🙂']
console.log(emojisCopy);  // ['😀', '😁', '🙂', '🙄']
```

我们可以看到原始数组没有修改。但是，如果我们使用了`=`符号来创建新的数组，那么修改会在两个地方都反映出来，因为它是一个引用或浅层拷贝。

## 9.拼接()

`splice()`方法是 JavaScript 中多用途方法之一。`splice`方法的主要目的是从一个数组中删除元素。但是，您可以单独使用`splice`方法来添加、删除和更新元素。

它在列表末尾的原因是我没有经常使用它，因为它不是很简单。我使用了其他更简洁、可读性更强的方法来解决同样的问题。

要添加一个元素，我们需要传递 3 个参数。我们要插入元素的位置、从该位置开始要删除的元素数量以及要添加的元素的值。

```
const flowers = ['🌻', '🌼', '🌷'];
flowers.splice(2, 0, '🌹');console.log(flowers); // ['🌻', '🌼', '🌹', '🌷']
// Rose 🌹 added at the 2nd position.
```

当您使用`splice`方法删除元素时，它会返回一个包含这些被删除元素的新数组，并修改原始数组。

```
const flowers = ['🌻', '🌼', '🌷', '🌺'];
const deletedFlowers = flowers.splice(1, 2, '🌹');console.log(flowers); // ['🌻', '🌹', '🌺']
console.log(deletedFlowers); // ['🌼', '🌷']
```

这是我在 JavaScript 中使用最多的 9 个数组方法，我很喜欢使用它们。请分享你现在正在学习的东西。

如果你喜欢读这篇文章，并想支持我这个作家和平台上的其他人，考虑注册成为一名媒体成员。一个月只需 5 美元，你就可以无限制地访问 Medium 上的所有教程和文章。如果你注册使用我的链接，我会赚一小笔佣金。

[**这里是无限制访问媒体上所有内容的链接。**](https://arpitfalcon.medium.com/membership)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)