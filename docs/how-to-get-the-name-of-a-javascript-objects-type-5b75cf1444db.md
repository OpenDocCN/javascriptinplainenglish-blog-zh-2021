# 如何获取一个 JavaScript 对象的类型名？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-name-of-a-javascript-objects-type-5b75cf1444db?source=collection_archive---------3----------------------->

![](img/72b6939f7077c7c90b480609de46d4bc.png)

Photo by [Tim Mossholder](https://unsplash.com/@timmossholder?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

获取创建对象的构造函数的名字是我们有时不得不做的事情。

在本文中，我们将了解如何获取创建 JavaScript 对象的构造函数的名称。

# 构造函数属性

我们可以使用对象的`constructor`属性来获取创建它的构造函数。

例如，我们可以写:

```
const arr = [1, 2, 3];
console.log(arr.constructor === Array);
```

然后控制台日志记录`true`，因为`arr`是用`Array`构造函数创建的。

这也可以用于我们自己创建的构造函数:

```
class A {}
const a = new A()
console.log(a.constructor === A);
```

控制台日志也会记录`true`。

# 遗产

如果我们从一个子类创建一个对象，那么我们可以检查一个从当前子类创建的对象。

例如，我们可以写:

```
class A {}
class B extends A {}
const b = new B()
console.log(b.constructor === B);
```

然后控制台日志也会记录`true`，因为`b`是从`B`构造函数创建的。

`constructor`拥有`name`属性来获取字符串形式的构造函数名。

例如，我们可以写:

```
class A {}
const a = new A()
console.log(a.constructor.name === 'A');
```

与构造函数的名称进行比较。

# 运算符的实例

`instanceof`操作符还让我们检查一个对象是否是从构造函数中创建的。

例如，我们可以写:

```
const arr = [1, 2, 3];
console.log(arr instanceof Array);
```

那么控制台日志应该记录`true`，因为`arr`是一个数组。

然而，`Array.isArray`在检查变量是否为数组时更可靠，因为它适用于所有帧。

此外，我们可以写:

```
class A {}
const a = new A()
console.log(a instanceof A);
```

检查`a`是否是`A`的实例。

`instanceof`也适用于子类。

所以我们可以写:

```
class A {}
class B extends A {}
const b = new B()
console.log(b instanceof B);
```

并且会记录`true`。

# 结论

我们可以使用`instanceof`操作符和`constructor`属性来检查一个对象是否是从给定的构造函数中创建的。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)