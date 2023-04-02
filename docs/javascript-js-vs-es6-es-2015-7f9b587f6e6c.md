# JavaScript: ES5 与 ES6+

> 原文：<https://javascript.plainenglish.io/javascript-js-vs-es6-es-2015-7f9b587f6e6c?source=collection_archive---------9----------------------->

## 通过例子了解 ECMAScript5 JavaScript 和 ECMAScript6+ JS 的区别。

![](img/4ca003653b03584794f6d7a25d703ec5.png)

Photo by [Nathan da Silva](https://unsplash.com/@silvawebdesigns?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript-es6?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

**JavaScript 和 ES6 简介**

如今，JavaScript 已经广泛用于前端开发(如 React)和后端开发(NodeJS)。人们可能会对 StackOverFlow 等网站上发布的 JavaScript 解决方案的不同变体感到困惑。

ECMA =欧洲计算机制造商协会。

ES6 也被称为 ECMAScript6(即 ECMAScript 的第 6 个版本)。其他同义词包括 ES2015 和 ECMAScript 2015。这是因为 ECMAScript 委员会决定转向年度更新，因此 ES6 版被重命名为 ES2015，以反映发布年份。

**JS 和 ES6 的关系**

ECMAScript

*   **脚本语言标准**
*   JS 基于 ECMAScript 标准

Java Script 语言

*   脚本语言
*   ECMAScript 标准最流行的实现
*   JS 实现 ECMAScript 并在它的基础上构建

让我们从常用的 ES6 的一些核心特性(与 ES5 相比，如果有的话)开始。

const 和 let
它们是 ES6 中声明变量的新关键字。

`let`是新的`var`。`var`是函数作用域的(作用域为直接函数体)，而`let`是块作用域的(作用域为用{ }表示的直接封闭块)。因此，用`var`声明的变量将被定义

```
// **ES5**
var firstName = 'Sandy'// **ES6**
let firstName = 'Sandy'// Example of the difference
function example() {
  var a = 'a';
  let b = 'b'; console.log(a,b); // a b {
    var c = 'c';
    let d = 'd';
  } console.log(c); // c
  console.log(d); // ReferenceError: d is not defined
}
```

`const`用于单次赋值，仅在变量没有进一步变化时使用。就像一个`let`，`const`声明被阻塞了作用域。
记下！因为它不能被重新分配，所以它必须在声明期间被初始化。

```
// **ES5**
var firstName = 'Sandy'// **ES6**
const firstName = 'Sandy'
```

对不可变变量使用`const`是一个很好的实践。这有助于提高代码的可读性，因为其他开发人员会清楚地知道哪些变量不应该有变化，并且还会减少错误，因为不会发生意外的赋值。

**箭头功能**
该箭头功能给人一种现代感，使代码更简单、更有结构。

```
// **ES5**
function sayHelloES5(name) {
  return 'ES5 Hello, ' + name;
}
console.log(sayHelloES5('Sandy')) // ES5 Hello, Sandy// **ES6**
const sayHelloES6 = (name) => {
  return `ES6 Hello, ${name}`;
}
console.log(sayHelloES6('Sandy')) // ES6 Hello, Sandy
```

箭头功能可用于其他内置功能，如`map`、`filter`和`reduce`。

```
const arr = [1,2,3,4,5];var es5EvenArr = arr.filter(function(item) {
  return item % 2 == 0;
})
console.log(es5EvenArr);  // [2,4]var es6OddArr = arr.filter(function(item) {
  return item % 2 != 0;
})
console.log(es6OddArr);  // [1,3,5]
```

**字符串插值的模板文字** 不再需要使用`+`进行字符串连接。你可能在前面的例子中见过。

```
// in **ES5**, you have to use +
var es5Name = 'Sandy';
console.log('Welcome, ' + es5Name); // Welcome, Sandy// in **ES6**, you can simply embed the variable within the same string
// enclosed in **``**
const es6Name = 'Sandy';
console.log(`Welcome, ${es6Name}`)  // Welcome, Sandy
```

**默认参数值** ES6 允许您设置功能参数的默认值。如果开发人员遗漏了任何参数，这将防止未定义的值，并消除使用条件流检查未定义参数的需要(- >所需代码更少！).

```
// ES5
function rewardPoint(name, point) {
  return name + ' has been rewarded: ' + point;
}
console.log(rewardPoint('Sandy')); // Sandy has been rewarded: undefined// ES6
const rewardPoint = (name, point=50) => {
  return `${name} has been rewarded: ${point}`;
}
console.log(rewardPoint('Sandy')); // Sandy has been rewarded: 50
```

**休息参数** 这是 ES6 中新增的参数。它提供了一种改进的方法，将不定数量的参数表示为函数参数中的数组。简单地说，它将元素(函数的参数)集合成一个数组。

```
const calSum = (...input) => {
  let sum = 0;
  for (let i of input) {
    sum += i;
  }
  return sum;
}console.log(calSum(1,2,3)); // 6
console.log(calSum(1,2,3,4,5,6,7,8,9,10,11,12,13,14,15)); // 120
```

**展开运算符** 与 Rest Parameter 的语法相似。这扩展了任何数组的内容。

```
const arr1 = ['a', 'b', 'c'];
const arr2 = [1,2,3];const combinedArr12 = [...arr1, ...arr2];
const combinedArr = [...arr1, 'Sandy', 'John'];console.log(combinedArr12); // [ 'a', 'b', 'c', 1, 2, 3 ]
console.log(combinedArr);  // [ 'a', 'b', 'c', 'Sandy', 'John' ]
```

**级**

ES6 提供了一种更直观的编写类的方式，这种方式更接近于面向对象编程(OOP)风格——使用“class”关键字，同时也支持继承。在 ES5 中，使用“原型”来定义属性。

```
// **ES6**class Animal {
  constructor (id, name) {
    this.id = id;
    this.name name;
  }

  eat() {
    console.log(`${name} is eating.`);
  } toString() {
    return `Animal Id: ${this.id}`;
  }
}// **Inheritance**class Dog extends Animal {
  constructor (id, name, breed) {
    super(id, name);
    this.breed = breed;
  } toString() {
    return `Dog -> ${super.toString()}`;
  }
}const a = new Animal(1, 'Barney');
a.eat();                                       // Barney is eating.
console.log(a.toString());                     // Animal Id: 1const dog = new Dog(2, "nilo" ,"Golden Retriever");
console.log(dog.toString());                   // Dog -> Animal Id: 2
```

**模块导入/导出** 在 ES6 中，可以向/从模块导入/导出值，而不会污染全局名称空间。语法也发生了变化。有两种类型:命名和默认。

名称导出是通过名称来区分的。使用名称导出导出的类、变量或函数只能使用相同的名称导入。此外，名称导出可以允许导入和导出多个变量和函数。

默认导出最多只能有一个要导出的值。

```
// **Named Export**
// **ES5**
var a = require('moduleA');
var b = require('moduleB');module.exports = {
  getReward: function() {...},
  points: a.points,
  name: b.name
};// **ES6** // Person.jsclass Person {
  // properties
  // methods
}const getRewards = () => {
  ...
}export {Person};
export {getRewards};*// alternatively, export multiple entities
export {Person, getRewards};*
```

导入命名导出

```
// ES6
// App.jsimport {Person, getRewards} from './Person.js';// Alternatively, use the one can import all export statements all together
// But it might be too difficult to track if there are too many of such statements, hence we use an alias
import * as person from './Person.js';// usage
person.Person
person.getRewards()
```

默认导出可以以任何名称导入，与命名导出不同，默认导出中只能有一个 export 语句。

```
// **Default Export**
// **ES6** // Person.jsclass Person {
  // properties
  // methods
}export default Person;// App.js
import Person from './Person.js';
```

有了新版本的 ES，人们可以写得更少，同时保持代码的可读性。有兴趣了解更多关于 ES6 必须提供的东西吗？更多详情请查看他们的[官方](http://es6-features.org)页面。

*更内容于* [***通俗易懂的英语中***](http://plainenglish.io/)