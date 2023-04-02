# 如何在对象数组上调用 JavaScript Array 的 reduce 方法？

> 原文：<https://javascript.plainenglish.io/how-to-call-javascript-arrays-reduce-method-on-an-array-of-objects-cc7721f4fd59?source=collection_archive---------9----------------------->

![](img/e3a15dcf5b3fa73dea8222d6d5d7b718.png)

Photo by [Roy Perez](https://unsplash.com/@rmbdlp?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须在一个对象数组上调用 JavaScript 数组的`reduce`方法，并希望从中获得一个结果。

在本文中，我们将看看如何用 JavaScript array 的`reduce`方法产生一个结果并把它放入一个对象中。

# 对对象数组调用 reduce

要在对象数组上调用`reduce`，我们可以从回调中获取对象。

为此，我们写道:

```
const arr = [{
  x: 1
}, {
  x: 2
}, {
  x: 3
}];
const result = arr.reduce((a, b) => ({
  x: a.x + b.x
}));
console.log(result)
```

我们有`arr`阵列。

我们通过返回一个对象，将`a`和`b`的`x`属性和`x`属性加在一起，用回调来调用它的`reduce`。

`a`和`b`是来自`arr`数组的对象。

我们还可以获得`x`属性的值，并将它们相加。

例如，我们可以写:

```
const arr = [{
  x: 1
}, {
  x: 2
}, {
  x: 3
}];
const result = arr.reduce((acc, obj) => {
  return acc + obj.x;
}, 0);
console.log(result)
```

`acc`是所有`x`属性值的总和。

`obj`在`arr`中有我们正在迭代的对象。

我们返回`acc + obj.x`来返回总和。

第二个参数是返回结果的初始值。

我们将它设置为 0，这样我们就可以将`x`的值加在一起。

所以`result`是 6。

此外，我们可以在回调的第二个参数中析构对象，方法是:

```
const arr = [{
  x: 1
}, {
  x: 2
}, {
  x: 3
}];
const result = arr.reduce((acc, { x }) => {
  return acc + x;
}, 0);
console.log(result)
```

# 一起使用 map 和 reduce

此外，我们可以一起使用`map`和`reduce`方法。

我们使用`map`从`x`属性返回一个数字数组。

然后我们可以用`reduce`把所有的数字加在一起。

例如，我们可以写:

```
const arr = [{
  x: 1
}, {
  x: 2
}, {
  x: 3
}];
const result = arr.map((a) => a.x)
  .reduce((a, b) => a + b);
console.log(result)
```

我们用回调来调用`map`以返回`x`的值。

然后我们用回调函数调用`reduce`来返回总和。

# 结论

我们可以通过从参数中获取对象来调用对象数组上的`reduce`,并对它做我们想要做的事情。

或者我们可以使用`map`从数组条目中提取我们想要的值，并调用`reduce`以我们想要的方式组合这些值。

*更多内容看*[***plain English . io***](http://plainenglish.io)