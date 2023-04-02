# 获取 JavaScript 对象的键的最好方法是什么？

> 原文：<https://javascript.plainenglish.io/what-are-the-best-ways-to-get-the-key-of-a-javascript-object-7c7e3d79fe1c?source=collection_archive---------19----------------------->

![](img/420c5ebe8f487b5f94089618828d8462.png)

Photo by [Florian Berger](https://unsplash.com/@bergerteam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

通常，我们必须获取 JavaScript 对象的键和值。

在本文中，我们将研究如何从对象中获取键和值。

# 使用 Object.keys 方法获取对象键

我们可以使用`Object.keys`方法来获取一个对象的键。

它返回一个包含对象的字符串键的数组。

例如，我们可以写:

```
const obj = {
  first: 'someVal',
  second: 'otherVal'
};
const keys = Object.keys(obj)
console.log(keys)
```

那么`keys`就是`[“first”, “second”]`。

# 使用 Object.values 方法获取对象属性值

要获得一个对象的属性值，我们可以使用`Object.values`方法。

它返回一个包含对象属性值的数组。

例如，我们可以写:

```
const obj = {
  first: 'someVal',
  second: 'otherVal'
};
const values = Object.values(obj)
console.log(values)
```

那么`values`就是`[“someVal”, “otherVal”]`。

# 使用 Object.entries 方法获取对象键值对

要获得一个对象的键值对数组，我们可以使用`Object.entries`方法。

例如，我们可以写:

```
const obj = {
  first: 'someVal',
  second: 'otherVal'
};
const pairs = Object.entries(obj)
console.log(pairs)
```

那么`pairs`就是:

```
[
  [
    "first",
    "someVal"
  ],
  [
    "second",
    "otherVal"
  ]
]
```

# 结论

我们可以很容易地用一些 JavaScript 对象方法单独或一起获得一个 JavaScript 对象的键和值。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)