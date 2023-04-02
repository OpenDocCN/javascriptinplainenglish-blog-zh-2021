# JavaScript —面试准备指南(50 个与输出相关的问题)

> 原文：<https://javascript.plainenglish.io/50-javascript-output-questions-818d45c3e381?source=collection_archive---------0----------------------->

## 前端开发人员备忘单

![](img/dce2ac66454f2a8848e494fef75d40f7.png)

## 问题 1:(字符串、数字、布尔型)

```
var num = 8;
var num = 10;
console.log(num);
```

**回答—** 10
**解释—** 用`var`关键字，可以声明多个同名变量。该变量将保存最新的值。你不能用`let`或`const`做到这一点，因为它们是块范围的。

## 问题 2:

```
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Ayush';
  let age = 21;
}

sayHi();
```

**回答—** `undefined`和`ReferenceError`
**解释—** 在函数内部，我们先用`var`关键字声明`name`变量。这意味着变量被提升(内存空间是在创建阶段设置的)，默认值为`undefined`，直到我们实际到达定义变量的那一行。我们还没有在试图记录`name`变量的那一行定义变量，所以它仍然保存着`undefined`的值。

带有`let`关键字的变量(和`const`)被提升，但与`var`不同，不要让*初始化*。在我们声明(初始化)它们之前，它们是不可访问的。这被称为“时间死区”。当我们试图在声明变量之前访问它们时，JavaScript 抛出一个`ReferenceError`。

## 问题 3:

```
function getAge() {
  'use strict';
  age = 21;
  console.log(age);
}

getAge();
```

**回答—** `ReferenceError`
**解释—** 用`"use strict"`，可以确保不意外声明全局变量。我们从来没有声明过变量`age`，由于我们使用了`"use strict"`，它会抛出一个引用错误。如果我们不使用`"use strict"`，它可能已经工作了，因为属性`age`已经被添加到全局对象中。

## 问题 4:

```
+true;
!'Ayush';
```

**答案—** `1`和`false` **解释—** 一元加号试图将一个操作数转换成一个数。`true`是`1`，`false`是`0`。

字符串`'Ayush'`是一个真值。我们实际上问的是，“这个真值是假的吗？”。这将返回`false`。

## **问题 5:**

```
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```

**答案—** `0 2 2`。
**解释—** 后缀一元运算符`++`:

1.  返回值(这将返回`0`)。
2.  增加数值(数字现在是`1`)。

前缀一元运算符`++`:

1.  增加数值(数字现在是`2`)。
2.  返回值(这将返回`2`)。

这将返回`0 2 2`。

## 问题 6:

```
function sum(a, b) {
  return a + b;
}

sum(1, '2');
```

**回答—** `"12"`
**解释—** JavaScript 是一种动态类型化的语言:我们不指定某些变量是什么类型。值可以在你不知道的情况下自动转换成另一种类型，这叫做*隐式类型强制*。强制是从一种类型转换成另一种类型。

在本例中，JavaScript 将数字`1`转换为字符串，以便函数有意义并返回值。在添加数字类型(`1`)和字符串类型(`'2'`)时，数字被视为字符串。我们可以像`"Hello" + "World"`一样连接字符串，所以这里发生的是`"1" + "2"`返回`"12"`。

## **问题 7:**

```
String.prototype.giveAyushPizza = () => {
  return 'Just give Ayush pizza already!';
};

const name = 'Ayush';

name.giveAyushPizza();
```

**回答—** `"Just give Ayush pizza already!"`
**解释—** `String`是一个内置的构造函数，我们可以给它添加属性。我只是在它的原型上添加了一个方法。原始字符串被自动转换成字符串对象，由字符串原型函数生成。所以，所有的字符串(字符串对象)都可以访问那个方法！

## 问题 8:

```
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

**回答—** `1` `2` `4` **解释—** 如果某个条件返回`true`，则`continue`语句跳过一次迭代。

## 问题 9:

```
function sayHi() {
  return (() => 0)();
}

console.log(typeof sayHi());
```

**回答—** `"number"`
**解释—**`sayHi`函数返回立即调用的函数表达式(IIFE)的返回值。这个函数返回了类型为`"number"`的`0`。

仅供参考:内置类型只有 7 种:`null`、`undefined`、`boolean`、`number`、`string`、`object`、`symbol`。`"function"`不是类型，因为函数是对象，所以它属于类型`"object"`。

## 问题 10:

```
console.log(typeof typeof 1);
```

**回答—** `"string"`
**解释—** `typeof 1`返回`"number"`。并且`typeof "number"`返回`"string"`。

## 问题 11:

```
!!null;
!!'';
!!1;
```

**答案—** `false` `false` `true`
**解释—** `null`是 falsy。`!null`返回`true`。`!true`返回`false`。

`""`是福尔西。`!""`返回`true`。`!true`返回`false`。

`1`是真理。`!1`返回`false`。`!false`返回`true`。

## 问题 12:

```
[...'Ayush'];
```

**答案—** `["A", "y", "u", "s", "h"]`
**解释—** 一个字符串是可迭代的。spread 运算符将 iterable 的每个字符映射到一个元素。

## 问题 13:

```
console.log(3 + 4 + '5');
```

**答案—** `"75"`
**解释—** 运算符结合律是编译器对表达式求值的顺序，可以是从左到右，也可以是从右到左。只有当所有操作员都有相同的*优先级时，才会发生这种情况。我们只有一种类型的操作员:`+`。对于加法，结合性是从左到右的。*

首先得到评估。这导致了数字`7`。

`7 + '5'`因强制而导致`"75"`。JavaScript 将数字`7`转换成一个字符串。我们可以使用`+`操作符连接两个字符串。`"7" + "5"`导致`"75"`。

## 问题 14:

```
var a = 10;
var b = a;
b = 20;console.log(a);
console.log(b);var a = 'Ayush';
var b = a;
b = 'Verma';console.log(a);
console.log(b);
```

**答案—** `1\. 10 and 20`
`2\. "Ayush" and "Verma"`
**解释—** 赋给原语数据类型变量的值是**紧耦合**。这意味着，每当您创建原始数据类型变量的副本时，该值都会被复制到新变量所指向的新内存位置。当你制作一个副本时，它将是一个真正的副本。

## 问题 15:

```
function sum(){
  return arguments.reduce((a, b) => a + b);
}

console.log(sum(1,2,3)); (1)function sum(...arguments){
  return arguments.reduce((a, b) => a + b);
}

console.log(sum(1,2,3)); (2)
```

**回答—** 1。将会引发错误。
2。6
**解释** —
1。参数不是全功能数组，它们只有一个方法`length`。其他方法不能用在他们身上。
2。`...` rest 操作符创建所有函数参数的数组。然后我们用这个返回它们的和。

## 问题 16:

```
console.log(1 == '1');
console.log(false == '0');
console.log(true == '1');
console.log('1' == '01');
console.log(10 == 5 + 5);
```

**回答—** 真真假假真。
**解释** — `'1' == '01'`当我们在这里比较两个字符串时，它们是不同的，但其他都是相等的。

**问题 17:**

```
console.log('1' - - '1'); (1)
console.log('1' + - '1'); (2)
```

**答案—** 1。2
2。“1–1”
**解释** —
1。使用类型强制字符串被转换为数字并被视为`1 - -1` = `2`。
2。+运算符在 javascript 中用于字符串的串联，所以计算为`'1' + '-1'` = `1-1`。

**问题 18:**

```
let lang = 'javascript';
(function(){
   let lang = 'java';
})();

console.log(lang); (1)(function(){
   var lang2 = 'java';
})();

console.log(lang2); (2)
```

**答案—** 1。
2。将会引发错误。
**解说** —
1。用`let`定义的变量是阻塞范围，不会添加到全局对象中。
2。用`var`关键字声明的变量是函数作用域的，所以将函数封装在闭包里会限制它在外部被访问，这就是它抛出错误的原因

**问题 19:**

```
(function(){
   console.log(typeof this);
}).call(10);
```

**回答—** 对象 **解释** — `call`调用带有新`this`的函数，在本例中是`10`，它基本上是`Number`的构造函数，`Number`是 javascript 中的对象。

**问题 20:**

```
console.log("[ayushv.medium.com/](https://ayushv.medium.com/)" instanceof String); (1)const s = new String('[ayushv.medium.com/](https://ayushv.medium.com/)');
console.log(s instanceof String); (2)
```

**回答—** 1。假
2。true
**解释** —只有用`String()`构造函数定义的字符串才是它的实例。

## 问题 21:(对象，数组)

```
const obj = { a: 'one', b: 'two', a: 'three' };
console.log(obj);
```

**回答—** `{ a: "three", b: "two"}"`
**解释—** 如果你有两个同名的键，那么这个键会被替换。它仍将位于第一个位置，但具有最后指定的值。

## 问题 22:

```
let c = { greeting: 'Hey!' };
let d;d = c;
c.greeting = 'Hello';
console.log(d.greeting);
```

**回答—** `Hello`
**解释—** 在 JavaScript 中，所有对象在设置为彼此相等时，都通过*引用*进行交互。

首先，变量`c`保存一个对象的值。稍后，我们给`d`赋予与`c`相同的引用。当你改变一个对象时，你改变了所有的对象。

## 问题 23:

```
let a = 3;
let b = new Number(3);
let c = 3;console.log(a == b);
console.log(a === b);
console.log(b === c);
```

**答案—** `true` `false` `false`
**解释—** `new Number()`是内置函数构造器。虽然它看起来像一个数字，但它不是真正的数字:它有一堆额外的功能，是一个对象。

当我们使用`==`运算符时，它只检查是否有相同的*值*。它们的值都是`3`，所以它返回`true`。

然而，当我们使用`===`操作符时，值*和*类型应该是相同的。不是:`new Number()`不是数字，是对象。双双返回`false.`

## 问题 24:

```
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

**回答—** `"object"`
**解释—**rest 参数(`...args`)让我们将所有剩余的参数“收集”到一个数组中。数组是一个对象，所以`typeof args`返回`"object"`。

## 问题 25:

```
let greeting;
greetign = {}; // Typo!
console.log(greetign);
```

**回答—** `{}`
**解释—** 它记录对象，因为我们只是在全局对象上创建了一个空对象！当我们把`greeting`错打成`greetign`时，JS 解释器实际上把这个看成`global.greetign = {}`(或者浏览器中的`window.greetign = {}`)。

为了避免这种情况，我们可以使用`"use strict"`。这可以确保在将变量设置为任何值之前，您已经声明了该变量。

## 问题 26:

```
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log('You are an adult!');
  } else if (data == { age: 18 }) {
    console.log('You are still an adult.');
  } else {
    console.log(`Hmm.. You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```

**回答—** `Hmm.. You don't have an age I guess`
**解释—** 测试相等时，原语通过其*值*进行比较，对象通过其*引用*进行比较。JavaScript 检查对象是否引用了内存中的相同位置。

我们比较的两个对象没有这个:我们作为参数传递的对象引用了内存中不同的位置，而不是我们用来检查相等性的对象。

这就是为什么`{ age: 18 } === { age: 18 }`和`{ age: 18 } == { age: 18 }`都返回`false`的原因。

## 问题 27:

```
const obj = { 1: 'a', 2: 'b', 3: 'c' };
const set = new Set([1, 2, 3, 4, 5]);

obj.hasOwnProperty('1');
obj.hasOwnProperty(1);
set.has('1');
set.has(1);
```

**回答—**`true``true``false``true`
**解释—** 所有的对象键(不包括符号)都是头罩下的字符串，即使你自己不把它打成字符串。这就是为什么`obj.hasOwnProperty('1')`也返回 true。

对一组来说就不是这样了。我们的集合中没有`'1'`:`set.has('1')`返回`false`。它的数值类型为`1`，`set.has(1)`返回`true`。

## 问题 28:

```
const a = {};
const b = { key: 'b' };
const c = { key: 'c' };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

**答案—** `456`
**解释—** 对象键自动转换成字符串。我们试图将一个对象设置为对象`a`的键，值为`123`。

然而，当我们字符串化一个对象时，它变成了`"[object Object]"`。所以我们在这里说的是。然后，我们可以尝试再次做同样的事情。`c`是我们隐式字符串化的另一个对象。于是乎，`a["[object Object]"] = 456`。

然后，我们登录`a[b]`，实际上是`a["[object Object]"]`。我们只是将其设置为`456`，所以它返回`456`。

## 问题 29:

```
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers);
```

**回答—** `[1, 2, 3, 7 x empty, 11]`
**解释—** 当你给数组中的一个元素设置的值超过了数组的长度，JavaScript 就会创建一个叫做“空槽”的东西。这些实际上有`undefined`的值，但是你会看到类似于:

`[1, 2, 3, 7 x empty, 11]`

取决于你在哪里运行它(每个浏览器、节点等都不一样。).

## 问题 30:

```
let person = { name: 'Ayush' };
const members = [person];
person = null;

console.log(members);
```

**答—** `[{ name: "Ayush" }]`
**解释—** 我们只修改了`person`变量的值，而不是数组中的第一个元素，因为该元素有一个不同的(复制的)对对象的引用。`members`中的第一个元素仍然保持其对原始对象的引用。当我们记录`members`数组时，第一个元素仍然保存被记录的对象的值。

## 问题 31:

```
const person = {
  name: 'Ayush',
  age: 21,
};

for (const item in person) {
  console.log(item);
}
```

**回答—** `"name", "age"`
**解释—** 用一个`for-in`循环，我们可以迭代对象键，这里是`name`和`age`。在幕后，对象键是字符串(如果它们不是符号的话)。在每次循环中，我们将`item`的值设置为等于它正在迭代的当前键。首先，`item`等于`name`，并被记录。然后，`item`等于`age`，记录下来。

## 问题 32:

```
[1, 2, 3].map(num => {
  if (typeof num === 'number') return;
  return num * 2;
});
```

**回答—** `[undefined, undefined, undefined]`
**解释—** 映射数组时，`num`的值等于当前循环的元素。在这种情况下，元素是数字，所以 if 语句的条件`typeof num === "number"`返回`true`。map 函数创建一个新数组，并插入从该函数返回的值。

但是，我们不返回值。当我们没有从函数返回值时，函数返回`undefined`。对于数组中的每个元素，函数块都被调用，所以对于每个元素，我们返回`undefined`。

## 问题 33:

```
var obj = {a:1};
var secondObj = obj;
secondObj.a = 2;console.log(obj);
console.log(secondObj);var obj = {a:1};
var secondObj = obj;
secondObj = {a:2};console.log(obj);
console.log(secondObj);
```

**回答—** `1\. { a:2 }`和`{ a:2 }
2\. { a:1 }``{ a:2 }` **解释—** 1。如果对象属性被改变，那么新的对象指向相同的内存地址，所以原来的对象属性也会改变。
(引用调用)2。如果该对象被重新分配了一个新对象，那么它将被分配到一个新的内存位置，即它将是一个**真实副本**(通过值调用)。

## 问题 34:

```
const arrTest = [10, 20, 30, 40, 50][1, 3];   
console.log(arrTest);
```

**回答—** `40` **解释—** 第二个数组的最后一个元素作为索引，像`arrTest[3]`一样从第一个数组中获取值。

## 问题 35:

```
console.log([] + []);               (1)
console.log([1] + []);              (2)
console.log([1] + "abc");           (3)
console.log([1, 2, 3] + [1, 3, 4]); (4)
```

**答案—** `1\. ""
2\. "1"
3\. "1abc"
2\. "1,2,31,3,4"` **解释—** 1 .在 console.log 中打印时，空数组被视为 Array.toString()，因此它会打印一个空字符串。
2。在 console.log 中打印的空数组被视为`Array.toString()`，因此基本上是`“1” + “”` = `""`。
3。`“1” + “abc”` = `"1abc"`。
4。`“1, 2, 3” + “1, 3, 4”` = `"1,2,31,3,4"`。

## 问题 36:

```
const ans1 = NaN === NaN;
const ans2 = Object.is(NaN, NaN);
console.log(ans1, ans2);
```

**答案—** 假真
**解释—** `NaN`是唯一值所以在相等性检查中失败，但它是同一个对象所以`Object.is`返回`true`。

## 问题 37:

```
var a = 3;
var b = {
  a: 9,
  b: ++a
};
console.log(a + b.a + ++b.b);
```

**回答—** 18
**解释—** 前缀运算符递增数字后返回。所以下面的表达式会被求值为`4 + 9 + 5` = `18`。

## 问题 38:

```
const arr = [1, 2, undefined, NaN, null, false, true, "", 'abc', 3];
console.log(arr.filter(Boolean)); (1)const arr = [1, 2, undefined, NaN, null, false, true, "", 'abc', 3];
console.log(arr.filter(!Boolean)); (2)
```

**回答—
1。**【1，2，真，《abc》，3】。**2。它会抛出一个错误。
**解释—** 1。`Array.filter()`返回符合条件的数组。因为我们已经传递了 Boolean，所以它返回所有的真值。
2。当`Array.filter()`接受一个函数时，`!Boolean`返回不是函数的`false`，因此抛出一个错误`Uncaught TypeError: false is not a function`。**

## 问题 39:

```
const person = {
  name: 'Ayush Verma',
  .25e2: 25
};

console.log(person[25]);
console.log(person[.25e2]);
console.log(person['.25e2']);
```

**回答—** 25 25 未定义 **解释—** 在分配键时，对象对数值表达式求值，所以它变成了`person[.25e2] = person[25]`。因此，当我们使用`25`和`.25e2`进行访问时，它返回值，但对于`'.25e2'`是`undefined`。

## 问题 40:

```
console.log(new Array(3).toString());
```

**回答—** “，，” **解释—** `Array.toString()`用逗号分隔值创建数组的字符串。

## 问题 41: (setTimeout 和“this”关键字)

```
const foo = () => console.log('First');
const bar = () => setTimeout(() => console.log('Second'));
const baz = () => console.log('Third');bar();
foo();
baz();
```

**回答—** `First` `Third` `Second`
**解释—** 我们有一个`setTimeout`函数，先调用它。然而，它是最后被记录的。

这是因为，在浏览器中，我们不仅有运行时引擎，我们还有一个叫做`WebAPI`的东西。`WebAPI`为我们提供了`setTimeout`函数，例如 DOM。WebAPI 不能在准备好的时候就把东西添加到堆栈中。相反，它将回调函数推到一个叫做*队列*的地方。事件循环查看堆栈和任务队列。如果堆栈是空的，它将获取队列中的第一个内容，并将其推送到堆栈上。

## 问题 42:

```
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

**回答—** `3 3 3`和`0 1 2` **解释—** 由于 JavaScript 中的事件队列，`setTimeout`回调函数在循环执行完毕后被调用*。因为第一个循环中的变量`i`是使用`var`关键字声明的，所以这个值是全局的。在循环过程中，我们使用一元运算符`++`，每次都将`i`的值增加`1`。在调用`setTimeout`回调函数时，第一个例子中的`i`等于`3`。*

在第二个循环中，变量`i`是用`let`关键字声明的:用`let`(和`const`)关键字声明的变量是块范围的(块是在`{ }`之间的任何东西)。在每次迭代中，`i`将有一个新的值，并且每个值都在循环中。

## 问题 43:

```
let obj = {
    x: 2,
    getX: function() {
        setTimeout(() => console.log('a'), 0);
        new Promise( res =>  res(1)).then(v => console.log(v));
        setTimeout(() => console.log('b'), 0);
    }
}obj.getX();
```

**答案—** `1 a b` **解释—** 一个宏任务完成后，先依次执行其他所有的微任务，然后执行下一个宏任务。

微任务包括:`MutationObserver`、`Promise.then()`和`Promise.catch()`，其他基于 Promise 的技术如 fetch API、V8 垃圾收集过程、节点环境中的`process.nextTick()`。

宏任务包括初始脚本、`setTimeout`、`setInterval`、`setImmediate`、I/O、UI 渲染。

由于事件循环*的优先级*使作业从作业队列(存储已履行承诺的回调)中出队优先于任务队列(存储超时的`setTimeout()`回调)中的任务，所以立即解决的承诺比立即计时器处理得更快。

## 问题 44:

```
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};console.log(shape.diameter());
console.log(shape.perimeter());
```

**回答—**`20``NaN` **解释—** 注意，`diameter`的值是常规函数，而`perimeter`的值是箭头函数。

对于箭头函数，`this`关键字引用它当前的周围范围，不像常规函数！这意味着当我们调用`perimeter`时，它不是指 shape 对象，而是指它的周围范围(比如 window)。

那个对象上没有值`radius`，它返回`NaN`。

## 问题 45:

```
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person('Ayush', 'Verma');
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```

**回答—** `TypeError` **解释—** 在 JavaScript 中，函数是对象，因此，方法`getFullName`被添加到构造函数对象本身。因此，我们可以调用`Person.getFullName()`，但是`member.getFullName`抛出一个`TypeError`。

如果希望一个方法对所有对象实例都可用，必须将其添加到 prototype 属性中:

```
Person.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};
```

## 问题 46:

```
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const ayush = new Person('Ayush', 'Verma');
const sarah = Person('Sarah', 'Smith');

console.log(ayush);
console.log(sarah);
```

**回答—** `Person {firstName: "Ayush", lastName: "Verma"}`和`undefined` **解释—** 对于`sarah`，我们没有使用`new`关键字。使用`new`时，`this`是指我们新建的空对象。但是，如果不加`new`，`this`指的是全局对象！

我们说`this.firstName`等于`"Sarah"`，`this.lastName`等于`"Smith"`。我们实际做的是定义`global.firstName = 'Sarah'`和`global.lastName = 'Smith'`。`sarah`本身是左边的`undefined`，因为我们没有从`Person`函数返回值。

## 问题 47:

```
const person = { name: 'Ayush' };

function sayHi(age) {
  return `${this.name} is ${age}`;
}

console.log(sayHi.call(person, 21));
console.log(sayHi.bind(person, 21));
```

**回答—** `Ayush is 21` `function` **解释—** 有了这两者，我们就可以传递我们希望`this`关键字所指的对象。但是，`.call`也是*立即执行*！

`.bind.`返回函数的*副本*，但是带有绑定的上下文！它不会立即执行。

## 问题 48:

```
let obj = {
    x: 2,
    getX: function() {
        console.log(this.x);
    }
}obj.getX(); (1)let x = 5;
let obj = {
    x: 2,
    getX:() => {
        console.log(this.x)
    }
}obj.getX(); (2)let x = 5;
let obj = {
    x: 2,
    getX: function(){
        let x = 10;
        console.log(this.x);
    }
}let y = obj.getX;
y(); (3)
```

**回答—** `1) 2
2) undefined
3) undefined` **解释—** 第一种情况是常规函数，根据调用函数的 ***上下文*** 将`this`关键字绑定到不同的值。这里 obj 正在调用这个函数，它将指向当前 obj。

第二种情况是一个箭头函数，它将使用`this`在它们的 ***词法范围*** *中的值，即 x 在周围范围中的*值。这里环绕的是全局范围或窗口对象。在这种情况下，“x”被声明为 let，`let`与`var`不同，不在全局对象上创建属性。“x”不存在，即返回未定义。如果“x”被声明为 var，它将返回 5。

在第三种情况下，“y”被赋值为`obj.getX,`，并且“y”在全局范围或窗口对象中。因此,“this”将指向全局范围，即全局“x ”,由于“x”被声明为 let，所以全局“x”是未定义的。如果“x”被声明为 var，它将返回 5。

## 问题 49:

```
let a = 10, b = 20;
setTimeout(function () {
  console.log('Ayush');
  a++;
  b++;
  console.log(a + b);
});
console.log(a + b);
```

**回答—**30“ayu sh”32。
**解释—** Settimeout 在事件循环中把函数压入 BOM 栈或者在主函数执行完一切后执行。所以结果打印在主函数的 console.log 之后。

## 问题 50:

```
function a() {
  this.site = 'Ayush';

  function b(){
    console.log(this.site);
  } 

  b();
}

var site = 'Wikipedia';
a(); (1)function a() {
  this.site = 'Ayush';

  function b(){
    console.log(this.site);
  } 

  b();
}

var site = 'Wikipedia';
new a(); (2)function a() {
  this.site = 'Ayush';

  function b(){
    console.log(this.site);
  } 

  b();
}

let site = 'Wikipedia';
new a(); (3)
```

**回答—** `1\. 'Ayush'`。
`2\. 'Wikipedia'
3\. undefined`

**解释—** 1。当执行具有正常语法的函数时，如果在执行时没有设置，将使用最近的父节点的值`this`，所以在这种情况下它是`window`，然后我们在`window`对象中更新设置属性`site`并在内部访问它，所以它是`'Ayush'`。

2.当用关键字`new`调用一个函数作为构造函数时，那么`this`的值将是在执行时创建的新对象，所以目前是`{ site: 'Ayush' }`。

但是当一个具有正常语法的函数被执行时，`this`的值将默认为全局范围，如果它在执行时没有被赋值的话，所以它是`b()`的`window`并且`var site = 'Wikipedia';`将该值添加到全局对象，因此当它在`b()`内部被访问时，它打印`'Wikipedia'`。

3.用`let`定义的变量不会添加到全局范围。因此，未定义。

我希望你已经发现这是有用的。感谢您的阅读！

*更多内容请看*[***plain English . io***](http://plainenglish.io)