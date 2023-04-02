# JavaScript 备忘单—分布、变量和条件

> 原文：<https://javascript.plainenglish.io/javascript-cheat-sheet-spread-variables-and-conditionals-ce59c3d0aa44?source=collection_archive---------14----------------------->

![](img/3816c478a8e7bd113bb7fee099b893dc.png)

Photo by [Boris Smokrovic](https://unsplash.com/@borisworkshop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 web 编程中最流行的编程语言之一。

在本文中，我们将了解现代 JavaScript 的基本语法。

# 传播算子

我们可以使用 spread 运算符将其他对象的属性添加到一个对象中。

例如，我们可以写:

```
const a = {
 frstName: "james",
 lastName: "smith",
}
const b = {
 ...a,
 lastName: "White",
 canSing: true,
}
```

那么`b`就是:

```
{
  "frstName": "james",
  "lastName": "White",
  "canSing": true
}
```

# 解构嵌套对象

我们可以将嵌套的对象析构为变量。

例如，我们写道:

```
const bob = {
  name: "bob jones",
  age: 29,
  address: {
    country: "Westeros",
    state: "Crownlands",
    pinCode: "500014",
  },
};
const {
  address: {
    state,
    pinCode
  },
  name
} = bob;
```

那么`state`就是`'Crownlands'`，`pinCode`就是`'500014'`。

# 指数算子

我们可以使用指数运算符来做幂运算。

所以我们可以写:`2 ** 8`得到 256。

# 承诺与最后

我们可以调用`finally`来运行代码，而不考虑承诺的结果。

例如，我们写道:

```
Promise.resolve(1)
  .then((result) => {})
  .catch((error) => {})
  .finally(() => {})
```

# 如果-否则

我们可以使用`if-else`来编写有条件运行的代码。

例如，我们可以写:

```
if ((age >= 15) && (age < 19)) {
  status = "Eligible.";
} else {
  status = "Not eligible.";
}
```

如果`age`在 15 和 19 之间，那么第一个程序块运行。

否则，第二个块运行。

# 交换语句

我们可以使用`switch`语句来检查不止一种情况，如果值匹配就运行代码。

例如，我们写道:

```
switch (new Date().getDay()) {
  case 6:
    text = "Saturday";
    break;
  case 0:
    text = "Sunday";
    break;
  default:
    text = "";
}
```

如果`getDay`返回 6，那么`text`就是`'Saturday'`。

如果返回 0，那么`text`就是`'Sunday'`。

否则，`text`为空字符串。

# 分配变量

我们可以用`let`给变量赋值:

```
let x
```

`x`未初始化。

我们可以初始化它:

```
let y = 1
```

我们可以给它分配一个字符串:

```
let a = 'hi'
```

我们可以给它分配一个数组:

```
let b = [1,2,3]
```

我们可以给它分配一个布尔值:

```
let c = false;
```

和正则表达式:

```
let d = /()/
```

或者给它分配一个功能:

```
let e = function(){};
```

我们可以创造一个常数:

```
const PI = 3.14;
```

我们可以在一行中分配多个变量:

```
let a = 1, b = 2, c = a + b;
```

# 严格模式

我们可以在代码中添加`'use strict'`来让我们写出更好的 JavaScript 代码。

例如，我们不能写这样的代码:

```
a = 1
```

因为严格模式会阻止创建全局变量。

# 价值观念

JavaScript 有一些像布尔值一样的值:

```
false, true
```

数字:

```
1.2, 0n001, 0xF6, NaN
```

字符串:

```
'foo', 'bar'
```

和特殊值的保留字:

```
null, undefined, Infinity
```

# 结论

JavaScript 附带了各种构造来帮助我们创建程序。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容看*[***plain English . io***](https://plainenglish.io/)