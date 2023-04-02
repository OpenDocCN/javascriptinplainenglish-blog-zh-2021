# 如何用对象代替数组使用 JavaScript 数组映射方法？

> 原文：<https://javascript.plainenglish.io/how-to-use-javascript-array-map-method-with-objects-instead-of-arrays-fe6392b59bd8?source=collection_archive---------11----------------------->

![](img/c48c27add190c0e3676e3ef86a10a834.png)

Photo by [Donald Giannatti](https://unsplash.com/@wizwow?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望将对象的对象属性值映射到新值，而不是映射数组值。

在本文中，我们将了解如何使用 JavaScript array 的`map`方法来处理对象而不是数组。

# 对象.键

`object.keys`方法返回一个 JavaScript 对象的字符串键数组。

因此，我们可以遍历这些键，将属性值映射到它们的新值。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
};
for (const key of Object.keys(obj)) {
  obj[key] *= 2
}
console.log(obj)
```

我们有一个包含 3 个属性的`obj`对象。

然后我们用`Object.keys`和`obj`来返回密钥。

然后我们使用 for-of 循环遍历这些键。

然后我们就可以用它来做我们想做的事情。

在本例中，我们将每个属性值乘以 2。

因此，`obj`现在是:

```
{a: 2, b: 4, c: 6}
```

# Object.keys 和 reduce

我们还可以将`Object.keys`方法与`reduce`方法结合起来，将对象的属性值映射到新值。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
};const newObj = Object.keys(obj).reduce((result, key) => {
  result[key] = obj[key] * 2
  return result
}, {})
console.log(newObj)
```

我们在由`Object.keys`返回的字符串键数组上调用`reduce`。

`reduce`回调拥有`result`对象，这是我们目前拥有的对象。

`key`有字符串键值。

然后我们得到`result[key]`我们想要的值。

我们得到`obj[key]`值，并将其乘以 2。

然后我们返回`result`值。

第二个参数被设置为一个对象，因此`result`的初始值是一个对象。

这样，我们可以将属性值放入其中。

因此，`newObj`的值与前面的示例相同。

# `Object.fromEntries and Object.entries`

我们可以使用`Object.fromEntries`方法从键-值对的数组中创建一个对象。

我们可以使用`Object.entries`返回一个对象的键值对数组。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
};const newObj = Object.fromEntries(
  Object.entries(obj).map(
    ([key, value]) => ([key, value * 2])
  )
)
console.log(newObj)
```

我们用`obj`调用`Object.entries`来获取数组中的键值对。

然后我们用一个回调函数调用`map`，这个回调函数析构键值对。

我们返回一个键值对数组。

我们通过将该值乘以 2 来改变它。

然后我们使用`Object.fromEntries`从新的键值对数组中创建一个对象。

因此`newObj`是:

```
{a: 2, b: 4, c: 6}
```

就像我们以前一样。

# 结论

我们可以通过使用 JavaScript 标准库中一些方便的对象方法将对象属性映射到新值。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)