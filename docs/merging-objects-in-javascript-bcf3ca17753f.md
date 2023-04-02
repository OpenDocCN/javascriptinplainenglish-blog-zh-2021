# 如何在 JavaScript 中合并对象

> 原文：<https://javascript.plainenglish.io/merging-objects-in-javascript-bcf3ca17753f?source=collection_archive---------4----------------------->

## 如何使用 JavaScript 方法合并对象？

![](img/291d30977b94bd9b5bfd925fe5f6efba.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 使用 Object.assign

`Object.assign()`方法的工作原理是将另一个对象(称为源对象)的值和属性复制到我们试图更新的对象(称为目标对象)中。

有几种方法我们可以使用`Object.assign()`来合并我们的对象。第一种方法是简单地将我们想要更新的原始对象作为第一个参数，将包含我们想要合并的数据的另一个对象作为第二个参数。

```
Object.assign(target, source);
```

然而，这样做的问题是，它改变了原始对象。所以如果我们不希望我们的原始对象发生变化，我们可以把一个空对象作为第一个参数传入。

```
Object.assign({}, target, source);
```

这将把目标和源对象的所有属性和值分配到一个全新的对象中。

我们还可以添加更多的对象作为参数，与我们从中复制数据的其他对象合并在一起。这可以通过将对象作为参数内联传入或者先定义它然后传入来实现。

# 使用扩展运算符

spread 运算符是另一种常见的方法，它恰好与将一个对象的属性和值合并到另一个对象更相关。我发现它比使用`Object.assign()`更简单，可读性更强。

为了使用 spread 操作符，在传递数据时，我们在想要从中复制数据的对象前面加上`...`。

这将提取出所有的属性和值，并将它们合并到一个全新的用户对象中。

如果我们想添加更多的属性，我们可以像以前一样通过`Object.assign()`内联或作为预定义对象传递属性。

```
const updatedUser = {...userData, ...newUserData, updated: true};
```

这将给我们一个新的对象，所有的属性都被合并进来，并且添加的属性`updated`被设置为 true。

```
{
  email: "bob@email.com",
  name: "Bob",
  password: "bobspassword",
  updated: true
}
```

*   [Object.assign()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
*   [在对象中展开运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)