# 如何访问 JavaScript 对象的第一个属性？

> 原文：<https://javascript.plainenglish.io/how-to-access-the-first-property-of-a-javascript-object-1934f9eaca41?source=collection_archive---------4----------------------->

![](img/040b4925cc6e73f379cba03c9ccf8abc.png)

Photo by [Tierra Mallorca](https://unsplash.com/@tierramallorca?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我们的 JavaScript 程序中，有时我们只想访问 JavaScript 对象的第一个属性。

在这篇文章中，我们将会看到访问 JavaScript 对象的第一个属性的各种方法。

# 对象.键

`Object.keys`方法返回一个包含对象的字符串键的数组。

因此，我们可以通过编写以下代码来访问对象中的第一个属性:

```
const obj = {
  a: 1,
  b: 2
};
const [prop] = Object.keys(obj)
console.log(obj[prop])
```

我们有带有一些属性的`obj`对象。

我们调用`Object.keys`并从返回的数组中析构第一个键，并将它赋给`prop`。

然后我们得到用`obj[prop]`返回的第一个属性的值。

所以我们从控制台日志中得到 1。

# for-in 循环和中断

我们可以使用 for-in 循环遍历一个对象，并在第一次迭代后中断。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2
};for (const prop in obj) {
  console.log(obj[prop])
  break;
}
```

我们有 for-in 循环并记录返回的第一个属性值。

`prop`有属性键字符串。

然后我们用`break`停止迭代。

# 对象.值

我们可以使用`Object.values`方法从对象中获取值。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2
};const [value] = Object.values(obj)
console.log(value)
```

如果我们只想要第一个属性值，那么我们可以使用`Object.values`并从返回的数组中析构它。

# 对象.条目

我们可以使用`Object.entries`方法返回一个键值对数组的数组。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2
};const [
  [key, value]
] = Object.entries(obj)
console.log(key, value)
```

从返回的数组中获取第一个键值对。

我们只是从嵌套数组中析构它。

因此`key`是`'a'`并且`value`是 1。

# 结论

我们可以使用 JavaScript 对象静态方法或 for-in 循环来获取 JavaScript 对象的第一个属性。

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***