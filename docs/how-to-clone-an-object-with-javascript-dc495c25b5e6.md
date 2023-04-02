# 如何用 JavaScript 克隆一个对象

> 原文：<https://javascript.plainenglish.io/how-to-clone-an-object-with-javascript-dc495c25b5e6?source=collection_archive---------17----------------------->

![](img/ed962769555dadd8f883d7b6fcb864cc.png)

Photo by [Sangga Rima Roman Selia](https://unsplash.com/@sxy_selia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时我们想在 JavaScript 代码中克隆一个对象。

在本文中，我们将看看如何用 JavaScript 克隆一个对象。

# 使用 Object.assign 方法

克隆 JavaScript 对象的一种方法是使用`Object.assign`方法。

例如，我们可以写:

```
const obj = {
  a: 1
};
const copy = Object.assign({}, obj);
console.log(copy);
```

我们用一个空对象调用`Object.assign`，用`obj`将`obj`的属性复制到空对象上并返回。

那么`copy`和`obj`的内容是一样的。

# 使用扩展运算符

克隆对象的另一种方法是使用扩展操作符。

其工作原理与`Object.assign`相同。

例如，我们可以这样使用它:

```
const obj = {
  a: 1
};
const copy = {
  ...obj
};
console.log(copy);
```

然后我们得到和上一个例子一样的结果。

# 使用 Lodash cloneDeep 方法

如果我们需要深度克隆一个对象，那么我们可以使用 Lodash `cloneDeep`方法来进行克隆。

它将克隆所有级别的属性，而不仅仅是顶层。

例如，我们可以这样使用它:

```
const obj = {
  a: 1
};
const copy = _.cloneDeep(obj);
console.log(copy);
```

那么`copy`就是`obj`的深度复制。

# 结论

我们可以用`Object.assign`方法或 spread 操作符复制一个对象。

要深度克隆一个对象，我们可以使用 Lodash `cloneDeep`方法。

*更多内容请看*[***plain English . io***](http://plainenglish.io)