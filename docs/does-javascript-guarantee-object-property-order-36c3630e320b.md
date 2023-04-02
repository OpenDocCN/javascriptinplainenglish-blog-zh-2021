# JavaScript 保证对象属性顺序吗？

> 原文：<https://javascript.plainenglish.io/does-javascript-guarantee-object-property-order-36c3630e320b?source=collection_archive---------6----------------------->

![](img/8f60d50f5853a67620ffcc2b198869aa.png)

Photo by [Micheile Henderson](https://unsplash.com/@micheile?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 对象是动态的。

所以我们可以在任何时候插入任何属性。

在本文中，我们将了解 JavaScript 对象是否有保证的属性排序顺序。

# ES2015 对象

在 ES2015 中，顺序大多遵循插入顺序。

这是真的，有些键是数字。

如果混合了数字键和非数字键，那么首先遍历数字键。

然后遍历其他键。

不同浏览器的数字键行为可能有所不同。

Chromium 不考虑数字键的插入顺序，比如把它们放在第一位。

例如，如果我们有以下对象:

```
const obj = Object.create(null, {
  m: {
    value() {},
    enumerable: true
  },
  "2": {
    value: "2",
    enumerable: true
  },
  "b": {
    value: "b",
    enumerable: true
  },
  0: {
    value: 0,
    enumerable: true
  },
  [Symbol()]: {
    value: "sym",
    enumerable: true
  },
  "1": {
    value: "1",
    enumerable: true
  },
  "a": {
    value: "a",
    enumerable: true
  },
});for (const prop in obj) {
  console.log(prop)
}
```

当我们用 for-in 循环遍历它时，我们看到我们得到:

```
0
1
2
m
b
a
```

记录在案。

数字键最先出现。

然后，非数字字符串键按照插入的顺序循环。

以下方法保证按插入的顺序遍历键:

*   `Object.assign`
*   `Object.defineProperties`
*   `Object.getOwnPropertyNames`
*   `Object.getOwnPropertySymbols`
*   `Reflect.ownKeys`

但是这些方法或循环不能保证以任何顺序遍历对象:

*   `Object.keys`
*   `for..in`
*   `JSON.parse`
*   `JSON.stringify`

然而，如果我们使用`Object.keys`，我们可以对键进行排序，因为键是以数组的形式返回的。

# ES2015 之前

在 ES2015 之前，没有定义对象关键点的迭代顺序。

这意味着它们可以在不同的运行时环境中变化。

然而，它们中的大多数遵循与 ES2015 中相同的规则。

# 结论

不能保证 JavaScript 对象中的对象属性以任何顺序被遍历。

因此，如果我们想保证键按照我们想要的顺序被遍历，我们应该对它们进行排序或者使用 JavaScript 映射。

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报在这里***](http://newsletter.plainenglish.io) *。***