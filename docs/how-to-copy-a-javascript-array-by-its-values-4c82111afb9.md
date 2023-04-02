# 如何通过值复制 JavaScript 数组

> 原文：<https://javascript.plainenglish.io/how-to-copy-a-javascript-array-by-its-values-4c82111afb9?source=collection_archive---------17----------------------->

![](img/aa9c3497e6d0b8b06aada113885b339c.png)

Photo by [Jen Theodore](https://unsplash.com/@jentheodore?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

复制 JavaScript 数组是我们在应用程序中经常要做的事情。

在本文中，我们将研究如何通过值来复制 JavaScript 数组。

# 数组.原型.切片

我们可以使用 JavaScript 数组实例中可用的`slice`方法。

例如，我们可以写:

```
const oldArray = [1, 2, 3, 4, 5];
const newArray = oldArray.slice();
console.log(newArray);
```

如果没有参数传入，`slice`方法返回它所调用的数组的副本。

# 传播算子

将一个数组的条目复制到另一个数组的另一种方法是使用 spread 运算符。

这是从 ES6 开始提供的。

例如，我们可以写:

```
const oldArray = [1, 2, 3, 4, 5];
const newArray = [...oldArray];
console.log(newArray);
```

我们用 spread 操作符将所有项目从`oldArray`复制到`newArray`。

所以`newArray`就是`oldArray`的翻版。

# 数组.原型.串联

我们也可以使用`concat`方法将一个数组复制到一个新的数组中。

要使用它，我们可以写:

```
const oldArray = [1, 2, 3, 4, 5];
const newArray = [].concat(oldArray);
console.log(newArray);
```

`concat`返回它所调用的数组，并将该数组作为参数传递给它。

此外，我们可以写:

```
const oldArray = [1, 2, 3, 4, 5];
const newArray = oldArray.concat();
console.log(newArray);
```

它也返回一个`oldArray`的副本。

# JSON.stringify 和 JSON.parse

我们可以使用`JSON.stringify`和`JSON.parse`来复制一个数组。

例如，我们可以写:

```
const oldArray = [1, 2, 3, 4, 5];
const newArray = JSON.parse(JSON.stringify(oldArray));
console.log(newArray);
```

`JSON.stringify`将`oldArray`转换成一个 JSON 字符串。

然后我们使用`JSON.parse`将 JSON 字符串转换回数组。

然后我们将返回值赋给`newArray`。

# 数组. from

另一种复制数组的方法是使用`Array.from`方法。

方法让我们从其他数组或类似数组的对象中创建一个数组。

要用它来复制一个数组，我们可以写:

```
const oldArray = [1, 2, 3, 4, 5];
const newArray = Array.from(oldArray);
console.log(newArray);
```

我们只需将想要复制的数组传入方法，它就会被复制。

# 洛达什

Lodash 有`clone`方法来做一个对象的浅层克隆。

它也有`cloneDeep`方法来做一个对象的深度克隆。

我们可以使用任何一个来复制一个数组。

例如，我们可以写:

```
const oldArray = [1, 2, 3, 4, 5];
const newArray = _.clone(oldArray)
console.log(newArray);
```

或者:

```
const oldArray = [1, 2, 3, 4, 5];
const newArray = _.cloneDeep(oldArray)
console.log(newArray);
```

复制`oldArray`并将其分配给`newArray`。

# 结论

使用 JavaScript 的标准库，有很多方法可以将一个数组复制到另一个数组中。

我们也可以用 Lodash 做同样的事情。

*更多内容请看*[***plain English . io***](http://plainenglish.io)