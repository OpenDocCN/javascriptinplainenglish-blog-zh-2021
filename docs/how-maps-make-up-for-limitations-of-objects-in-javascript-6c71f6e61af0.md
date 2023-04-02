# 地图如何解决 JavaScript 中对象的局限性

> 原文：<https://javascript.plainenglish.io/how-maps-make-up-for-limitations-of-objects-in-javascript-6c71f6e61af0?source=collection_archive---------4----------------------->

## JavaScript 中地图的概述，以及它们如何弥补使用对象带来的限制。

![](img/524c913e11e0d6d4949f486685040668.png)

Photo by [Denise Jans](https://unsplash.com/@dmjdenise?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，对象是最常用的数据结构之一。它们为您提供了一种以键/值对的形式组织和存储数据的方法。尽管如此，它们也有一些值得指出的限制。在本文中，我们将讨论这些限制，并展示如何使用`Map`对象比使用常规对象更有效。

# 什么是地图对象？

`Map`对象最初是在 JavaScript 的 ES6 版本中引入的。像常规对象一样，它们可以包含键、值对，并允许您添加、检索、删除和检查这些键和值。

要创建一个`Map`对象的新实例，我们可以这样做:

```
const map = new Map([
    ["key", "value"]
]);
```

有几个内置的属性和方法与`Map`对象的实例一起提供。这些包括但不限于一些更常见的问题，例如:

*   `.set()` -添加键、值对，第一个参数是键，第二个是值`.set(key, value)`
*   `.get()` -通过将指定的键作为唯一参数传入来检索链接到键的值`.get(key)`
*   `.delete()` -删除由传入的键名`.delete(key)`标识的键、值对
*   `.has()` -检查键、值对是否存在，并返回一个布尔值。将密钥作为唯一参数`.has(key)`
*   `.size` -返回一个整数，表示包含在`Map`对象中的键/值对的数量

*要了解更多关于* `*Map*` *对象的内置属性和方法，请查看此* [*链接*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#constructor) *。*

# 使用地图避免使用对象的限制

为了展示使用`Map`对象如何解决使用对象时出现的限制，让我们来看看这些限制是什么，以及我们如何使用地图来避免它们。

## 不保证对象是有序的

尽管自 JavaScript 更新到 ES6 后这种情况有所改变，但常规对象的键/值对的排序仍然不可靠。

以我们声明的以下对象为例:

```
const obj = {
    1: 2,
    0: false,
    "Greet": "Hello World",
    a: "b",
    c: "c"
}
```

当我们将`obj`登录到控制台时，它显示的顺序与我们最初声明的顺序不同:

```
{0: false, 1: 2, Greet: 'Hello World', a: 'b', c: 'c'}
```

当我们试图用一个映射声明相同的键/值对时，

```
const map = new Map([
    [1, 2],
    [0, false],
    ["Greet", "Hello World"],
    ["a", "b"],
    ["c", "c"]
]);
```

相反，我们得到的是声明它们的原始顺序。

```
{1 => 2, 0 => false, 'Greet' => 'Hello World', 'a' => 'b', 'c' => 'c'}
```

## 没有快速确定物体长度或大小的方法

对于一个对象，我们通过使用 for 循环和计数器或者使用`Object.entries()`方法和`.length`迭代对象来手动确定大小。

```
const obj = {
    1: "one",
    2: "two",
    3: "three"
};Object.entries(obj).length; // 3
```

当我们需要找出一个`Map`对象中键/值对的数量时，我们可以使用`.size`属性轻松地得到它。

```
const map = new Map([
    [1, "one"],
    [2, "two"],
    [3, "three"]
]);console.log(map.size); // 3
```

## **地图对象自然是可迭代的，对象不是**

为了迭代对象，我们通常使用一个`for..in`循环来手动获取每个键和值。

```
// obj = {1: 'one', 2: 'two', 3: 'three'}for (let key in obj) {
    console.log(key, ": ", obj[key]);
    // 1: one
    // 2: two
    // 3: three
}
```

但是请注意，`Object.keys()`和`Object.values()`或`Object.entries()`也可以用来使一个对象可迭代。

```
Object.entries(obj)
  .forEach(entry => console.log(entry[0], ": ", entry[1]));
  // 1: one
  // 2: two
  // 3: three
```

可以使用类似`.forEach()`的方法轻松直接地迭代 map 对象来访问每个值。

```
// map = {1 => 'one', 2 => 'two', 3 => 'three'}map.forEach(value => console.log(value));
// one
// two
// three
```

## 对象的键类型只能是字符串或符号

当声明 Javascript 对象时，我们可以用作键的唯一类型是字符串或符号。

```
const obj = {
    ["key"]: "value"
};console.log(obj); 
// automatically converts array key to a symbol: {key: 'value'}const obj2 = {
    ["key"]: "value",
    function key(), "Value"
};console.log(obj2); // throws an error
```

虽然常规 JavaScript 对象的键只能是字符串或符号，但地图对象却不是这样。对于 Map 对象，它的键可以是任何类型，包括函数、对象和数组。

```
const map = new Map([
    [ ["key"], "value" ],
    [ function key() {}, "value" ],
    [ { "a": 1 }, "b" ],
]);console.log(map); 
// {Array(1) => 'value', ƒ => 'value', {…} => 'b'}
```

# 摘要

在 Javascript 中，映射是非常有用的数据结构。它们提供了比常规对象更大的灵活性，例如，映射让我们能够使用任何数据类型作为键，同时还能保持声明它们的原始顺序。

下一次当您使用普通的 ol' JavaScript 对象来存储某种复杂数据时，可以考虑使用映射。根据使用情况，它可能会更好地为您服务！

*   [地图](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#objects_vs._maps)
*   [物体对地图](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#objects_vs._maps)

*更多内容请看*[***plain English . io***](http://plainenglish.io)