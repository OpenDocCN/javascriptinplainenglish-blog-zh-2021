# 如何将传统的 For 循环转换成 JavaScript 数组方法

> 原文：<https://javascript.plainenglish.io/how-to-convert-traditional-for-loops-to-javascript-array-methods-89e4cb9e6250?source=collection_archive---------13----------------------->

通过例子解释一些 JavaScript 数组方法

![](img/352b647870d6a14d9f3d099aa7ccbf12.png)

Photo by [Clay Banks](https://unsplash.com/@claybanks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我想通过解决日常的用例来解释它们，而不是仅仅浏览一些顶级的 JavaScript 数组方法定义。每个用例都将从需求开始。每个用例之后都有一个初始代码块，这是一种不利用数组方法来解决它的方法。第二个代码块将是使用更现代的数组方法来解决它的方法。

## 用例 1:

**需求:**我需要我列出的水果的价格。

```
const fruits = [{type: 'Apple', price: .5}, {type: 'Banana', price: .25}];
const prices = [];
for (let i = 0; i < fruits.length; i++) {
  prices.push(fruits[i].price);
}
console.log(prices); // [.5, .25]
```

利用[映射](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)方法。`map`方法的目的是在对每个元素执行操作的同时，从给定的数组创建一个新的数组。一个常见的用例是修改数组中的值并返回一个新值；然而，在这个例子中，我们只需要数组中每个值的一个属性。

```
const fruits = [{type: 'Apple', price: .5}, {type: 'Banana', price: .25}]
const prices = fruits.map(fruit => fruit.price); 
console.log(prices) // [.5, .25]
```

## 用例 2:

**需求:**我想知道我现有的水果有多少是. 50 以下的。

```
const fruits = [{type: 'Apple', price: .5}, {type: 'Banana', price: .25}];
const fruitUnderFifty = [];
for (let i = 0; i < fruits.length; i++) {
  if (fruits[i].price < .5) {
    fruitUnderFifty.push(fruits[i]);
  }
}
console.log(fruitUnderFifty); // [{type: 'Banana', price: .25}]
```

利用[过滤器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)方法。`filter`方法旨在为数组中的每个值应用一个谓词。当返回值为`true`时，元素将被添加到正在创建的数组中。判断是否应该使用 filter 方法的一个简单方法是，在传统的 for 循环中是否有一个`if`条件来决定是否应该向数组中添加内容。如果你这样做了，你就有机会利用`.filter`方法

```
const fruits = [{type: 'Apple', price: .5}, {type: 'Banana', price: .25}];
const fruitUnderFifty = fruits.filter(fruit => fruit.price < .5);
console.log(fruitUnderFifty); // [{type: 'Banana', price: .25}]
```

## 用例 3:

**需求:**我需要知道是否每种水果都有现货。

```
const fruits = [{type: 'Apple', price: .5, inStock: true}, {type: 'Banana', price: .25, inStock: true}];
let areAllFruitsInStock = true;
for (let i = 0; i < fruits.length; i++) {
  if (!fruits[i].inStock) {
    areAllFruitsInStock = false;
    break;
  }
}
console.log(areAllFruitsInStock); // true
```

利用每一种方法。`every`方法返回一个布尔值，并测试数组中的每个元素，看它是否通过。如果只有一个元素没有通过测试，那么返回值为 false。

```
const fruits = [{type: 'Apple', price: .5, inStock: true}, {type: 'Banana', price: .25, inStock: true}];
const areAllFruitsInStock = fruits.every(fruit => fruit.inStock);
console.log(areAllFruitsInStock); // true
```

## 用例 4:

**需求:**我需要知道我的库存里有没有猕猴桃。

```
const fruits = [{type: 'Apple', price: .5}, {type: 'Kiwi', price: .33}];
let hasKiwi = false;
for (let i = 0; i < fruits.length; i++) {
  if (fruits[i].type === 'Kiwi') {
    hasKiwi = true;
  }
}
console.log(hasKiwi); // true
```

利用[点](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)的方法。在整个迭代过程中，只要满足**一次**条件，就会返回`true`。还有一个有用的方法叫做 [includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) ，但是它不用于这些类型的用例，因为我们想要检查一个对象上的特定字段。如果你想在这个场景中使用`.includes`，你可以选择`.map`，然后选择`.includes`。

```
const fruits = [{type: 'Apple', price: .5}, {type: 'Kiwi', price: .33}];
const hasKiwi = fruits.some(fruit => fruit.type === 'Kiwi');
console.log(hasKiwi); // true
```

## 用例 5:

需求:我需要汇总我当天水果的总销售额。

```
const sales = [.5, .25, .5, .5, .25];
let sum = 0;
for (let i = 0; i < sales.length; i++) {
  sum += sales[i];
}
console.log(sum); // 2
```

利用[减少](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)的方法。这是`reduce`的榜样，理由很充分。当你想从数组中取值并进一步减少它们时，那么`reduce`是一个很好的方法。

`reduce`方法通常是最难理解的。我建议在创建函数时使用命名良好的参数。下面，我们就用`sum`和`sale`。你会经常看到`previousValue`和`currentValue`。虽然这些是描述性的，但它们通常不足以描述您的用例。因此，通过给它们起更有意义的名字，这将有助于你更好地维护你的代码，同时也使新来者更容易理解。

```
const sales = [.5, .25, .5, .5, .25];
const totalSalesForTheDay = sales.reduce((sum, sale) => sum + sale);
console.log(totalSalesForTheDay) // 2
```

## 用例 6:

需求:我需要找到我的百香果。

```
const fruits = [{type: 'Passion Fruit', price: .75}, {type: 'Banana', price: .25}];
let passionFruit;
for (let i = 0; i < fruits.length; i++) {
  if (fruits[i].type === 'Passion Fruit') {
    passionFruit = fruits[i];
  }
}
console.log(passionFruit); // {type: 'Passion Fruit', price: .75}
```

利用[寻找](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)的方法。`find`方法将返回您请求的值。在这种情况下，它将返回百香果对象。

```
const fruits = [{type: 'Passion Fruit', price: .75}, {type: 'Banana', price: .25}];
const passionFruit = fruits.find(fruit => fruit.type === 'Passion Fruit');
console.log(passionFruit); // {type: 'Passion Fruit', price: .75}
```

## 结论

这些是一些最常用的 JavaScript 数组方法。它们有助于用更少的代码行解决常见的问题，并降低仅仅为了迭代一个数组而犯小错误的风险。通过使用数组方法，您还减少了对`let`的使用，这也有利于可读性和可维护性。事实上，如果您在使用数组时看到过`let`，这通常是可以使用数组方法的迹象。