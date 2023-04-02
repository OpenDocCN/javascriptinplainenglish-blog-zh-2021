# 如何在 JavaScript 中创建关联数组或散列

> 原文：<https://javascript.plainenglish.io/how-create-an-associative-array-or-hash-in-javascript-15c887f07e21?source=collection_archive---------6----------------------->

![](img/bc57e0ddf2a15de87ebf0330ed32e1cb.png)

Photo by [Mariana Montes de Oca](https://unsplash.com/@marianamontesdeoca?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在许多编程语言中，关联数组允许我们在 JavaScript 应用程序中存储键值对。

在本文中，我们将看看如何用 JavaScript 创建关联数组或散列。

# 创建与对象相关联数组

创建关联数组的一种方法是使用 JavaScript 对象。

这是因为我们可以动态删除 JavaScript 对象属性。

属性名是键，值是值。

例如，我们可以写:

```
const dictionary = {}
dictionary.a = 1
dictionary.b = 2
console.log(dictionary)
```

创建具有属性`a`和`b`的`dictionary`对象。

`dictionary`是`{a: 1, b: 2}`。

我们也可以将属性名作为字符串放在方括号中。

例如，我们可以写:

```
const dictionary = {}
dictionary['a'] = 1
dictionary['b'] = 2
console.log(dictionary)
```

这让我们可以在代码中动态添加属性名。

然后，为了遍历对象，我们可以使用`Object.keys`、`Object.values`或`Object.entries`方法。

`Object.keys`返回一个对象的键数组。

`Object.values`返回一个对象的值数组。

`Object.entries`返回一个对象的键值对数组的数组。

例如，我们可以写:

```
const dictionary = {}
dictionary.a = 1
dictionary.b = 2for (const key of Object.keys(dictionary)) {
  console.log(key, dictionary[key])
}
```

然后我们得到:

```
a 1
b 2
```

从控制台日志中。

`key`有一个被 for-of 循环遍历的键。

我们可以用`Object.values`循环遍历这些值:

```
const dictionary = {}
dictionary.a = 1
dictionary.b = 2for (const value of Object.values(dictionary)) {
  console.log(value)
}
```

所以我们得到:

```
1
2
```

从控制台日志中。

我们可以用`Object.entries`遍历键值对:

```
const dictionary = {}
dictionary.a = 1
dictionary.b = 2for (const [key, value] of Object.entries(dictionary)) {
  console.log(key, value)
}
```

我们从被迭代的数组中析构键和值，以获得键和值。

所以我们得到:

```
a 1
b 2
```

由于`Object.keys`、`Object.values`或`Object.entries`方法返回数组，我们可以用它们返回的`length`属性得到长度。

# `Maps`

ES6 带有`Map`构造函数，让我们创建关联数组或散列。

例如，我们可以这样使用它:

```
const map = new Map()
map.set('a', 1)
map.set('b', 2)
```

我们分别用键和值调用`set`方法来添加条目。

然后我们可以用 for-of 循环遍历它，因为它是一个可迭代的对象:

```
for (const [key, value] of map) {
  console.log(key, value)
}
```

我们可以使用带有键的`get`方法来获取给定键的值:

```
const map = new Map()
map.set('a', 1)
map.set('b', 2)
console.log(map.get('a'))
```

我们传入`'a'`来返回 1，这是我们在地图上看到的。

为了获得大小，我们使用了`size`属性:

```
const map = new Map()
map.set('a', 1)
map.set('b', 2)
console.log(map.size)
```

控制台日志应该显示 2。

# 结论

我们可以用带有映射的 JavaScript 对象创建一个关联数组或散列。