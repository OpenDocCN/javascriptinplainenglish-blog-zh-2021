# 如何检查一个 JavaScript 变量的类型是否为布尔型？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-the-type-of-a-javascript-variable-is-boolean-84b3d4cb31cc?source=collection_archive---------17----------------------->

![](img/64e46a0c6740735ad3a8cf5a1a30fa80.png)

Photo by [Louis Hansel @shotsoflouis](https://unsplash.com/@louishansel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

因为 JavaScript 是一种动态类型语言，它的变量可以包含任何类型的数据。

因此，我们需要一种方法来检查变量的数据类型。

在本文中，我们将研究检查 JavaScript 变量的数据类型是否为布尔值的方法。

# 运算符的类型

检查变量是否为布尔变量的一种方法是使用`typeof`操作符。

为此，我们写道:

```
if (typeof variable === "boolean") {
  // ...
}
```

我们用表达式 if`if`语句检查`variable`变量的数据是否为布尔型。

如果`variable`是一个布尔值，它将返回`true`。

# ===运算符

另一种检查变量是否为布尔值的方法是用`===`运算符检查它是否等于`true`或`false`。

例如，我们可以写:

```
const isBoolean = (val) => {
  return val === false || val === true;
}
console.log(isBoolean(true))
console.log(isBoolean('abc'))
```

我们创建了`isBoolean`来检查`val`是`false`还是`true`。

因为我们使用了`===`操作符，所以只有当`val`与被比较的值完全相等时，or 表达式中的任一个表达式才会返回`true`。

因此，第一个控制台日志应该记录`true`。

第二个应该记录`false`。

# 用 toString 检查变量的字符串表示

除了检查值是否正好等于`true`或`false`之外，我们还可以比较它的字符串值，看它是不是布尔值。

例如，我们可以写:

```
const isBoolean = (val) => {
  return val === true || val === false || toString.call(val) === '[object Boolean]';
}
console.log(isBoolean(true))
console.log(isBoolean('abc'))
```

我们用我们的`val`参数调用`toString.call`，看看它是否返回`‘[object Boolean]’`。

如果是的话，那么它给了我们更多的信心`val`是一个布尔值。

# 使用 valueOf 方法

如果我们有用`Boolean`构造函数装箱的布尔变量，我们也可以调用`valueOf`方法来返回布尔变量的原始版本。

例如，我们可以写:

```
const isBoolean = (val) => {
  return typeof val === 'boolean' ||
    (
      typeof val === 'object' &&
      val !== null &&
      typeof val.valueOf() === 'boolean'
    );
}
console.log(isBoolean(true))
console.log(isBoolean('abc'))
```

要添加:

```
(
  typeof val === 'object' &&
  val !== null &&
  typeof val.valueOf() === 'boolean'
)
```

为了检查`val`是否是一个不是`null`的对象，但是当我们调用`valueOf`时，我们得到了返回的`'boolean'`。

如果我们通过编写如下表达式来调用`Boolean`构造函数，那么这个表达式就是`true`:

```
new Boolean(true)
```

创建装箱的布尔对象。

控制台日志应该与前面的示例相同。

# 结论

有很多方法可以用来检查一个 JavaScript 变量是否是布尔变量。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)