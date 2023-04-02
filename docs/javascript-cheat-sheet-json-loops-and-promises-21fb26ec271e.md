# JavaScript 备忘单— JSON、循环和承诺

> 原文：<https://javascript.plainenglish.io/javascript-cheat-sheet-json-loops-and-promises-21fb26ec271e?source=collection_archive---------15----------------------->

![](img/2b6fa0734dd0d9e72cf46b8a3e558005.png)

Photo by [Anthony Fomin](https://unsplash.com/@aginsbrook?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 web 编程中最流行的编程语言之一。

在本文中，我们将研究现代 JavaScript 的基本语法

# JSON

我们可以用`JSON.stringify`方法从 JavaScript 对象创建 JSON 字符串:

```
const obj = {
  "name": "Jane",
  "age": 18,
  "city": "Chicago"
};
const json = JSON.stringify(obj);
```

我们可以用`JSON.parse`将 JSON 字符串转换回 JavaScript 对象:

```
const obj = JSON.parse(json);
```

我们可以用它在本地存储器中存储数据。

我们必须首先将对象转换成字符串来存储它们。

来储存我们称之为`localStorage.setItem`的物体:

```
const obj = {
  "name": "Jane",
  "age": 18,
  "city": "Chicago"
};
const json = JSON.stringify(obj);
localStorage.setItem('json', json);
```

第一个论点是关键。

我们可以用`getItem`键获取数据:

```
localStorage.getItem('json')
```

# 环

JavaScript 带有各种循环。

一种循环是`for`循环:

```
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

我们可以用`for-of`循环遍历任何类型的可迭代对象:

```
for (let i of custOrder) {
  console.log(i);
}
```

一些可迭代对象包括数组、字符串和节点列表。

另一种循环是`while`循环:

```
let i = 1;
while (i < 100) {
  i *= 2;
  console.log(i);
}
```

还有一个`do-while`循环:

```
let i = 1;
do {
  i *= 2;
  console.log(i);
} while (i < 100)
```

关键字`break`让我们提前结束循环:

```
for (let i = 0; i < 10; i++) {
  if (i == 5) {
    break;
  }
  console.log(i);
}
```

`continue`关键字让我们跳到下一个迭代:

```
for (let i = 0; i < 10; i++) {
  if (i == 5) {
    continue;
  }
  console.log(i);
}
```

# 数据类型

JavaScript 带有各种数据类型。

它们包括:

```
let age = 18;                           // number 
let name = "Jane";                      // string
let name = { first: "Jane", last: "Doe" };  // object
let truth = false;                      // boolean
let sheets = ["HTML", "CSS", "JS"];       // array
let a; typeof a;                        // undefined
let a = null;                           // value null
```

# 目标

我们可以用花括号创建一个对象:

```
let student = {
  firstName: "Bob",
  lastName: "Doe",
  age: 18,
  height: 170,
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
};
```

它有属性和方法。

`this`是`student`对象本身。

我们可以用`student.fullName()`调用`fullName`。

我们可以通过以下方式为属性赋值:

```
student.age = 19;
```

# 承诺

我们可以用`Promise`构造函数创建承诺:

```
function add(a, b) {
  return Promise((resolve, reject) => {
    setTimeout(() => {
      if (typeof a !== "number" || typeof b !== "number") {
        return reject(new TypeError("Inputs must be numbers"));
      }
      resolve(a + b);
    }, 1000);
  });
}
```

我们可以用这笔钱来履行诺言。

我们调用`reject`来拒绝一个错误的承诺。

然后我们可以调用`then`来获得解析的值，调用`catch`来获得错误值:

```
const p = sum(10, 5);
p.then((result) => {
  console.log(result)
}).catch((err) => {
  console.error(err);
});
```

# 结论

我们可以使用 JSON、本地存储、promises 和 JavaScript 循环。

*更多内容看* [***说白了***](https://plainenglish.io/)