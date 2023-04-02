# 如何用 JavaScript 创建枚举？

> 原文：<https://javascript.plainenglish.io/how-to-create-enums-in-javascript-357d979cb14f?source=collection_archive---------8----------------------->

![](img/6ea020ce5a19c49ad84fce8c85cdbfe6.png)

Photo by [Ekaterina Tishkina](https://unsplash.com/@tishkinakaterina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

枚举是常量列表的容器实体。

JavaScript 中没有本地枚举数据类型。

然而，我们可以创建自己的 JavaScript 枚举。

在本文中，我们将看看如何用 JavaScript 创建枚举。

# 创建一个带有符号值的对象并冻结它

为了在 JavaScript 中创建一个枚举对象，我们可以创建一个带有符号属性值的对象。

例如，我们可以写:

```
const Colors = Object.freeze({
  RED: Symbol("Colors.RED"),
  BLUE: Symbol("Colors.BLUE"),
  GREEN: Symbol("Colors.GREEN")
});
console.log(Colors.RED)
console.log(Colors.BLUE)
console.log(Colors.GREEN)
```

我们用`RED`、`BLUE`和`GREEN`属性创建一个对象。

然后我们将它们的值设置为符号。

符号是可以用作唯一标识符的原始值。

我们用`Symbol`函数创建一个符号。

用`Symbol`函数创建的每个符号都是唯一的，即使我们向 symbol 函数传递相同的参数，所以:

```
Symbol("Colors.RED") === Symbol("Colors.RED")
```

是`false`。

然后我们在对象上调用`Object.freeze`来防止对象被冻结。

一旦对象被冻结，我们就不能添加或更改对象中的现有属性。

然后我们可以像在控制台日志语句中一样访问它们。

# 结论

我们可以用 JavaScript 通过创建一个带有符号值的对象来轻松地创建枚举。

然后我们可以用`Object.freeze`冻结对象，防止对象发生变化。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)