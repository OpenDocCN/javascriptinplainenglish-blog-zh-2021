# React 本机数组方法指南

> 原文：<https://javascript.plainenglish.io/react-native-array-methods-d469b7f10447?source=collection_archive---------6----------------------->

![](img/fd7509d1d0a3cf765eb26450f93b54ec.png)

让我们考虑什么是数组方法。简单地说，React 数组方法是新版本 JavaScript 中作为数组原型提供的方法，通过这些方法，我们可以借助回调函数逐个导航数组元素，并执行某些检查

首先，请记住，本文很可能适用于您使用的其他编程语言和框架，因为这些概念存在于许多其他语言和框架中。

举个例子，假设我们有这样的数据。

```
const products = [
  { id: 1, name: "Pencil", price: 5 },
  { id: 2, name: "Notebook", price: 10 },
  { id: 3, name: "Eraser", price: 2 },
  { id: 4, name: "Sharpener", price: 7 },
];
```

# 。查找()

用于查找数组中的元素。一旦找到元素，搜索就停止并返回找到的元素。如果有另一个元素满足相同的条件，则返回找到的第一个元素。

```
products.find((product) => product.price > 5); // {id: 2, name: "Notebook", price: 10}
```

# 。一些()

返回数组中是否至少有一个元素满足给定条件。

```
products.some((product) => product.price < 2); // false, There isn't a single one in the array that costs less than 2
products.some((product) => product.price > 9); // true, There is at least one price greater than 9 in the array
```

# 。每隔()

无论数组中的所有元素是否满足输入的条件，返回 true/false。

```
products.every((product) => product.price > 1); // true, All product prices are greater than 1
products.every((product) => product.price < 10); // false, All item prices NOT less than 10
```

# 。包括()

检查字符串中是否存在给定的表达式，并返回布尔值(true 或 false)。i̇ncludes 区分大小写。

```
products.some((product) => product.name.includes("Pencil")); // true, Some product names contain Pencil
products.every((product) => product.name.includes("Pencil")); // false, All product names do not contain Pencil
```

# 。地图()

它将输入的回调函数应用于给定的数组元素，并用获得的结果创建一个新数组。简单地说，它帮助我们在现有数组的基础上创建一组新的数组。

请记住，生成的数组将始终与原始数组的长度相同。

```
products.map((product) => `${product.name} price ${product.price} was dollars.`);
// ["The price of the pencil is $5.", "The price of the notebook is $10.", "The price of the eraser is $2.", "The price of the sharpener is $7."]
```

**在 React Native:**

```
function ShowProducts({ productList }) {
  return productList.map((product) => <Text key={product.id}>{product.name}</Text>);
}
```

# 。过滤器()

顾名思义，它的工作方式类似于`.map()`方法。将输入的回调函数应用于给定的数组元素。消除返回 false 的结果，并创建一个结果返回 true 的新数组。

```
products.filter((product) => product.name.includes("Pencil")); // [{id: 1, name: "Pencil", price: 5}, {id: 4, name: "Sharpener", price: 7}]
```

💡因为`.filter()`和`.map()`都返回一个新的数组，所以它们可以加在一起在一行中使用。

```
products
  .filter((product) => product.name.includes("Pencil")) // Find products with Pencil first
  .map((product) => `${product.name} price ${product.price} was dollars.`); // Then apply the given callback function to the found elements

// ["The price of the pencil is $5.", "The price of the sharpener is $7."]
```

# 。减少()

它将回调函数作为 reducer 应用于给定数组的元素。这个函数返回的结果在每次循环中都会被记住，下一个返回的结果会与前一个结果相加。reducer 函数有四个参数:累加器(每个循环结果的总和)、当前值(数组中下一个值的值)、当前索引(数组中下一个值的位置)和源数组(应用 reduce 的数组)。

`.reduce()`也可以取一个初始值作为第二个参数。对于数学运算，将输入一个数字作为开始，还有字符串、数组等。也可以进入。

**列表中产品的总价:**

```
products.reduce((total, product) => total + product.price, 0); // 24
```

**将产品名称写在一行:**

```
products.reduce((names, product) => names + " " + product.name, "Product Names:"); // "Product Names: Pencil Notebook Eraser Sharpener"
```

**根据产品名称和价格创建一个字符串，并将其创建为一个新数组:**

```
products.reduce(
  (newProductList, product) => [
    ...newProductList,
    `${product.name} ${product.fiyat} was dollars.`,
  ],
  [] // Initial value is empty array
);
// ["The price of the pencil is $5.", "The price of the notebook is $10.", "The price of the eraser is $2.", "The price of the sharpener is $7."]
```

如果你觉得这篇文章有趣，请用鼓掌图标为我鼓掌。

继续编码！

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****