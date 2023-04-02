# JavaScript 备忘单—基本 ES6 语法和方法

> 原文：<https://javascript.plainenglish.io/javascript-cheat-sheet-basic-es6-syntax-and-methods-7126d23b8a49?source=collection_archive---------10----------------------->

![](img/f9afb415351436c1367334115dd758ce.png)

Photo by [K8](https://unsplash.com/@k8_iv?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 web 编程中最流行的编程语言之一。

在本文中，我们将了解现代 JavaScript 的基本语法。

# 箭头功能

```
const sum = (a, b) => a + b
```

`sum(1, 2)`返回 3。

# 默认参数

```
function print(a = 5) {
  console.log(a)
}
```

`print()`日志 5。

# 让范围

我们可以用`let`来声明变量:

```
let a = 3
if (true) {
  let a = 10
  console.log(a) 
}
```

`console.log`应该日志 10。

# 常数

`const`变量在初始化时只能赋值一次:

```
const a = 11
```

如果我们再次尝试赋值`a`，我们会得到一个错误。

# 多行字符串

我们可以用反斜杠(`)创建多行字符串:

```
console.log(`
  This is a
  multiline string
`)
```

# 模板字符串

我们可以用`${}`插值表达式:

```
const name = 'james' 
const message = `Hello ${name}`
```

那么`message`就是`'Hello james'`

# 字符串包括()

我们可以使用`includes`方法来检查一个字符串是否有给定的子串。

因此

```
'apple'.includes('pl')
```

返回`true`。

# 字符串以()开头

`startsWith`方法让我们检查一个字符串是否以给定的子字符串开始:

```
'apple'.startsWith('ap')
```

# 字符串重复()

我们可以使用`repeat`方法来重复一个字符串:

```
'ab'.repeat(3)
```

返回`‘ababab’`。

# 解构数组

我们可以使用析构语法将数组条目赋给变量。

例如，我们写道:

```
let [a, b] = [3, 10];
```

那么`a`是 3`b`是 10。

# 解构对象

我们可以用析构语法将对象属性赋给变量。

例如，如果我们有:

```
let obj = {
  a: 15,
  b: 20
};
let {
  a,
  b
} = obj;
```

那么`a`是 15`b`是 20。

# 对象属性分配

我们可以用对象属性分配语法给对象分配属性。

例如，我们写道:

```
const a = 2
const b = 5
const obj = {
  a,
  b
}
```

那么`obj`就是:

```
{a: 2, b: 5}
```

# 目标功能分配

我们可以用简写语法向对象添加方法:

```
const obj = {
  a: 'foo',
  b() {
    console.log('b')
  }
}
```

然后我们可以调用`obj.b()`来记录`'b'`。

# 传播算子

spread 运算符允许我们将数组合并成一个。

例如，我们写道:

```
const a = [1, 2]
const b = [3, 4]
const c = [...a, ...b]
```

而`c`就是`[1, 2, 3, 4]`。

# 对象.分配()

方法让我们将多个对象合并成一个。

例如，我们写道:

```
const obj1 = {
  a: 1
}
const obj2 = {
  b: 2
}
const obj3 = Object.assign({}, obj1, obj2)
```

那么`obj3`就是`{ a: 1, b: 2 }`。

# Object.entries()

我们可以用`Object.entries()`方法将对象的键值对放入一个数组中。

例如，我们写道:

```
const obj = {
  frstName: 'james',
  lastName: 'smith',
  age: 22,
  country: 'uk',
};
const entries = Object.entries(obj);
```

然后`Object.entries`返回:

```
[
  [
    "frstName",
    "james"
  ],
  [
    "lastName",
    "smith"
  ],
  [
    "age",
    22
  ],
  [
    "country",
    "uk"
  ]
]
```

# 结论

JavaScript 附带了我们可以使用的标准库中有用的语法和方法。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)