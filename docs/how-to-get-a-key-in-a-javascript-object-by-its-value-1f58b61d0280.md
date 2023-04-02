# 如何通过值获取 JavaScript 对象中的键？

> 原文：<https://javascript.plainenglish.io/how-to-get-a-key-in-a-javascript-object-by-its-value-1f58b61d0280?source=collection_archive---------12----------------------->

![](img/182bea69b8ebcbaec026c6d4387e10e0.png)

Photo by [Florian Berger](https://unsplash.com/@bergerteam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望通过值来获取 JavaScript 对象的键。

在本文中，我们将研究如何通过值获取 JavaScript 对象中的键。

# Object.keys 和 Array.prototype.find

我们可以使用`Object.keys`方法返回一个对象中非继承的字符串键数组。

我们可以使用 JavaScript 数组的`find`方法返回数组中满足给定条件的第一个实例。

例如，我们可以写:

```
const object = {
  a: 1,
  b: 2,
  c: 3
}
const value = 2;
const key = Object.keys(object).find(key => object[key] === value);
console.log(key)
```

我们有了想要在其中搜索关键字的`object`对象。

而`value`是我们要搜索的键值。

我们用`Object.kets`得到`object`的所有钥匙。

然后我们用返回`object[key] === value`的回调来调用`find`。

`key`是被迭代的`object`键，以找到给定`value`的键名。

因此，我们应该从控制台日志中看到`key`是`'b'`。

# Object.keys 和 Array.prototype.filter

我们可以用`filter`替换`find`，并从`filter`返回的数组中析构结果。

例如，我们可以写:

```
const object = {
  a: 1,
  b: 2,
  c: 3
}
const value = 2;
const [key] = Object.keys(object).filter(key => object[key] === value);
console.log(key)
```

对于`key`,我们得到了与上一个例子相同的结果。

# Object.entries 和 Array.prototype.find

我们可以使用`Object.entries`方法返回一个对象的键值对数组。

因此，我们可以使用返回的数组来查找具有给定值的对象的键。

例如，我们可以写:

```
const object = {
  a: 1,
  b: 2,
  c: 3
}
const value = 2;
const [key] = Object.entries(object).find(([, val]) => val === value);
console.log(key)
```

我们用一个回调函数调用`find`，这个回调函数有一个参数，其中的`val`变量是从这个参数中去掉的。

`val`具有键值对数组中的值。

所以当我们返回`val === value`时，我们返回与第一个例子相同的布尔表达式。

从`find`返回的结果中，我们可以通过析构从返回的键-值对中得到的键。

因此我们在控制台日志中记录了相同的值`key`。

# 结论

我们可以通过使用本地 JavaScript 对象方法找到具有给定值的键。