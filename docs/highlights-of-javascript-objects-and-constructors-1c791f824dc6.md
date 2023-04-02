# JavaScript 的亮点——对象和构造函数

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-objects-and-constructors-1c791f824dc6?source=collection_archive---------20----------------------->

![](img/c3224937f0d2df42f696cac58ea0bd72.png)

Photo by [Heidi Fin](https://unsplash.com/@heidifin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

要学习 JavaScript，我们必须学习基础知识。

在本文中，我们将了解 JavaScript 语言的最基本部分。

# 目标

我们需要对象来存储除原始值之外的值，如数字、字符串、布尔值等。

它充当我们想要存储的所有物品的容器。

例如，我们可以通过书写来定义一个对象:

```
const plan = {
  name: "Basic",
  price: 3,
  space: 100,
  transfer: 1000,
  pages: 10
};
```

我们创建了具有各种属性的`plan`对象。

`name`、`price`、`space`、`transfer`、`pages`为房产名称。

冒号后的表达式是它们的值。

属性用逗号分隔。

要访问一个属性，我们可以写:

```
plan.name
```

`plan.name`的值应为`'Basic'`。

我们可以分配不同值的属性。

例如，我们可以写:

```
plan.name = 'Deluxe';
```

那么`name`属性的新值就是`'Deluxe'`。

我们可以使用赋值运算符为任何数据类型赋值。

要检查对象中是否有属性，可以使用`in`运算符。

例如，如果我们有:

```
'name' in plan
```

那么应该返回`true`，因为`name`是`plan`的属性。

但是如果我们有:

```
'foo' in plan
```

则返回`false`，因为`foo`不是`plan`的属性。

我们需要用引号将属性名括起来，因为左操作数是一个字符串。

# 对象方法

对象可以有方法。

例如，我们可以写:

```
const plan = {
  name: "Basic",
  price: 3,
  space: 100,
  transfer: 1000,
  pages: 10,
  calcAnnualPrice() {
    return this.price * 12;
  }
};
```

将`calcAnnualPrice`方法添加到`plan`对象中。

`this`是对象本身，所以`this.price * 12`返回`price`属性乘以 12 的值。

# 构造器

我们可以用构造函数创建具有相同结构的对象。

它们是对象的模板。

为了创建一个构造函数，我们可以写:

```
function Plan(name, price, space, pages) {
  this.name = name;
  this.price = price;
  this.space = space;  
  this.pages = pages;
}
```

我们创建了`Plan`构造函数，它采用了`name`、`price`、`space`和`pages`参数。

然后将它们分配给同名`this`的属性。

当我们调用构造函数时，`this`将返回我们分配的所有属性。

要调用它，我们可以写:

```
const plan = new Plan('basic', 3, 100, 10)
```

我们使用`new`关键字来调用构造函数并创建对象。

`plan`的值为:

```
{
  name: "basic"
  pages: 10
  price: 3
  space: 100
}
```

编写构造函数的更好方法是使用类语法。

例如，我们可以写:

```
class Plan {
  constructor(name, price, space, pages) {
    this.name = name;
    this.price = price;
    this.space = space;
    this.pages = pages;
  }
}
```

`constructor`方法和我们之前的构造函数是一样的。

只是看起来不一样。这是创建构造函数的首选方式，因为它与其他流行的面向对象语言一致。

# 结论

我们可以创建对象在一个容器中存储多条数据。

为了创建具有相同结构的对象，我们可以创建构造函数。