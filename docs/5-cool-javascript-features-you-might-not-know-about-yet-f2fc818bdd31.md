# 你可能还不知道的 10 个很酷的 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/5-cool-javascript-features-you-might-not-know-about-yet-f2fc818bdd31?source=collection_archive---------3----------------------->

## 优化代码的 JavaScript 特性。

![](img/86f3bfab730eb2755403bd56a8b930d1.png)

Photo by [Kevin Canlas](https://unsplash.com/@kvncnls?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你可能已经使用 JavaScript 很长时间了，它的最新版本是 ES12。您可能正在使用它的一些特性，今天，我想重点介绍一些特性，它们可能有助于您编写更好、更干净、更优化的 JavaScript 代码。

# 1.零操作符

如果左侧为空或未定义，则该运算符返回右侧值，否则返回左侧值。

```
const val= null ?? 'default';
console.log(val);
// expected output: "default"const val = 0 ?? 12;
console.log(val);
// expected output: 0
```

## 逻辑 OR (||)操作符做同样的事情，但是当作为值传递 0 时，它接受 false，这使得它容易被用于数字。

```
function add(a, b) {
    val1 = a || 1;
    val2 = b || 1;
    sum = val1 + val2;
    return sum;
} console.log(add(0, 0)); //output:2
```

## 当我们使用 Nullish 运算符时，情况也是如此

```
function add1(a, b) {
    val1 = a ?? 1;
    val2 = b ?? 1;
    sum = val1 + val2;
    return sum;
}

console.log(add1(0, 0)); //ouput:0
```

# 2.开关状态优化

如果你想优化你的开关语句，那么这个可以帮助你。

```
// Longhand
switch (data) {
    case 1:
        data1();
        break;
    case 2:
        data2();
        break;
    case 3:
        data();
        break;
        // And so on...
}
// Shorthand
var data = {
    1: data1,
    2: data2,
    3: data
};
const val = 1
data[val]();function data1() {
    console.log("data1");
}function data2() {
    console.log("data2");
}function data() {
    console.log("data");
}
```

# 3.控制台样式

你对使用同样的游戏机感到厌烦吗？现在我们可以设计我们的控制台了。

```
console.log(`%cabc`, 'font-weight:bold;color:red');
```

![](img/436800c47358f8c5c734cb844107a839.png)

# 4.AND (&&)运算符

如果我们想避免一个 If 语句，那么这个简写将是有帮助的。

```
//Longhand 
if (test1) {
 callMethod(); 
}//Shorthand 
test1 && callMethod();
```

# 5.简短的函数调用

我们可以使用三元运算符来实现这些功能。

```
// Longhand
function data1() {
    console.log('data1');
};function data2() {
    console.log('data2');
};
var data3 = 1;
if (data3 == 1) {
    data1();
} else {
    data2();
} //data1
// Shorthand
(data3 === 1 ? data1 : data2)(); //data1
```

# 6.返回速记

这将有助于避免一大块代码专门返回到基于返回语句的调用方法。

```
// Longhand
let value;function returnMe() {
    if (!(value === undefined)) {
        return value;
    } else {
        return callFunction('value');
    }
}var data = returnMe();
console.log(data); //output value
function callFunction(val) {
    console.log(val);
}// Shorthand
function returnMe() {
    return value || callFunction('value');
}
```

# 7.如果…否则速记

当我们有 if-else 语句时，这一条会有所帮助(确保最多有 2-3 条 if…else 语句，因为超过这一数量会降低代码的可读性)。

```
// Longhand
let mychoice: boolean;if (money > 100) {
    mychoice= true;
} else {
    mychoice= false;
}// Shorthand
let mychoice= (money > 10) ? true : false;//or we can use directly
let mychoice= money > 10;console.log(mychoice);
```

嵌套条件如下所示

```
let salary = 300,
checking = (salary > 100) ? 'greater 100' : (x < 50) ? 'less 50' : 'between 50 and 100';console.log(checking); // "greater than 100"
```

# 8.可选链接

有时，访问未定义的属性会出错，我们需要为所有嵌套的对象属性添加空检查。可以使用可选的链接来减少。

```
const data = {
    a: 1,
    b: 'atit',
    d: {
        test1: {
            test2: 'patel',
        },
    },
};console.log(data.val.test1); // here val is not present in object which leads the errorError: Cannot read properties of undefined (reading 'test1')console.log(data?.val); // using this we can check if the val is present in the data or not
```

# 9.对象属性分配

当我们想从两个字符串中创建对象，并保留与字符串相同的键时，可以使用这种简写方式。

```
let data1 = 'abcd'; 
let data2 = 'efgh';//Longhand 
let data = {data1: data1, data2: data2};//Shorthand 
let data = {data1, data2};
```

# 10.推迟

当 JavaScript 代码大小增加时，可能会导致浏览器必须等到所有脚本都执行完才能加载 DOM，这增加了等待时间。

通过使用这个属性，我们可以告诉浏览器不要等待脚本；相反，它将继续构建 DOM，并在后台加载脚本。

```
<p>heading before loads</p><script defer src="src/test.js"></script><p>heading after loads</p>
```

## 更多的 JavaScript 简写，可以让你的代码看起来更好，帮助你用 JavaScript 写出更简洁的代码。

# 如果速记

你是否厌倦了使用大量的 if 语句？让我们检查一些选项，这可能有所帮助。

```
//longhandif (fruit === 'apple' || fruit === 'banana' || fruit === 'orange' || fruit ==='mango') {
    //logic
}//shorthandif (['apple', 'banana', 'orange', 'mango'].includes(fruit)) {
   //logic
}
```

# 变量声明

当我们有相同类型的变量时，我们可以避免写两次。

```
//Longhand 
let data1;
let data2= 1;//Shorthand 
let data1, data2= 1;
```

[](/12-methods-for-finding-an-item-in-an-array-and-array-of-objects-in-javascript-84c7d46d85bd) [## 在 JavaScript 中查找数组(和对象数组)中的项目的 12 种方法

### JavaScript 中从数组和对象数组中删除重复项的方法。

javascript.plainenglish.io](/12-methods-for-finding-an-item-in-an-array-and-array-of-objects-in-javascript-84c7d46d85bd) 

# 检查非空值

如果我们想检查变量不为空呢？我们现在可以不用再写所有条件了。

```
// Longhand
if (data1 !== null || data1!== undefined || data1 !== '') {
    let data2 = data1;
}// Shorthand
let data2 = data1 || '';
```

# 分配默认值

```
let data1 = null,
    data2 = test1 || '';console.log("null check", data2); // output will be ""
```

# 未定义的值检查

```
let data1 = undefined,
    data2 = data1 || '';console.log("undefined check", data2); // output will be ""
```

正常值检查

```
let data1 = 'data',
    data2 = data1 || '';console.log(data); // output: 'data'
```

(注意:我们也可以对主题 4、5 和 6 使用`??`运算符)

# 赋值

```
//Longhand 
let data1, data2, data3;
data1 = 1;
data2 = 2;
data3 = 3;//Shorthand 
let [data1, data2, data3] = [1, 2, 3];
```

# 赋值运算符

它通常在我们处理算术运算符时使用，就个人而言，我喜欢手写，因为它可读性更强。

```
// Longhand
data1 = data1 + 1;
data2 = data2 - 1;
data3 = data3 * 30;// Shorthand
data1++;
data2--;
data3 *= 30;
```

# 无效支票

最常用的操作数之一，但要确保您的值为 true、非空字符串、已定义的值和非空值。

```
// Longhand
if (data1 === true) or if (data1 !== "") or if (data1 !== null)// Shorthand //
if (test1)
```

注意:如果 test1 有任何值，它将落入 If 循环之后的逻辑中，这个操作符主要用于空值或未定义的检查。

# 箭头功能

```
//Longhand 
function add(a, b) { 
   return a + b; 
} 
//Shorthand 
const add = (a, b) => a + b;
```

让我们再看一个例子

```
function function(value) {
  console.log('value', value);
}function= value => console.log('value', value);
```

# 隐性回报

即使不编写返回语句，箭头函数也有助于返回值。酷吧？

```
//longhandfunction calculate(diameter) {
  return Math.PI * diameter
}//shorthandcalculate = diameter => (
  Math.PI * diameter;
)
```

# 十进制基数指数

```
// Longhand
for (var i = 0; i < 100000; i++) { ... }// Shorthand
for (var i = 0; i < 1e5; i++) {
```

# 默认参数值

```
//Longhand
function add(data1, data2) {
    if (data1 === undefined) data1 = 1;
    if (data2 === undefined) data2 = 2;
    return data1 + data2;
}
//shorthand
add = (data1 = 1, data2 = 2) => data1 + data2;console.log(add()); //output: 3
```

# 传播算子

在另一个地方创建数组引用也很有用，对于浅层拷贝也是如此。

```
//longhand// joining arrays using concat
const testdata= [1, 2, 3];
const values = [4 ,5 , 6].concat(data);//shorthand// joining arrays
const testdata = [1, 2, 3];
const values = [4 ,5 , 6, ...testdata];
console.log(test); // [ 4, 5, 6, 1, 2, 3]
```

对于克隆，我们也可以使用扩展运算符。

```
//longhand// cloning arrays
const data1 = [1, 2, 3];
const data2 = data1.slice()//shorthand// cloning arrays
const data1 = [1, 2, 3];
const data2 = [...data1];
```

# 模板文字

如果你正在寻找在字符串中追加多个值的简写方法，那么这个简写方法正适合你。

```
//longhandconst literal = 'Hi ' + data1 + ' ' + data2 + '.'//shorthandconst literal= `Hi ${data1} ${data2}`;
```

# 多行字符串

```
//longhandconst literal = 'abc abc abc abc abc abc\n\t'
    + 'val test,test test test test\n\t'//shorthandconst literal = `abc abc abc abc abc abc
         val test,test test test test`
```

[](/javascript-basics-what-is-the-difference-between-splice-and-slice-fa47b80796c9) [## JavaScript 基础:拼接和切片有什么区别？

### 两分钟内掌握 JavaScript 基础知识。

javascript.plainenglish.io](/javascript-basics-what-is-the-difference-between-splice-and-slice-fa47b80796c9) 

# 数转换

```
//Longhand 
let test1 = parseInt('12'); 
let test2 = parseFloat('2.33');//Shorthand 
let test1 = +'12'; 
let test2 = +'2.33';
```

# 解构分配

```
//longhand
const data1 = this.data.data1;
const data2 = this.data.data2;
const data2 = this.data.data3;//shorthand
const { data1, data2, data3 } = this.data;
```

# Array.find 方法

从数组中查找第一个匹配值的数组方法之一。

```
const data = [{
        type: 'data1',
        name: 'abc'
    },
    {
        type: 'data2',
        name: 'cde'
    },
    {
        type: 'data1',
        name: 'fgh'
    },
]function datafinddata(name) {
    for (let i = 0; i < data.length; ++i) {
        if (data[i].type === 'data1' && data[i].name === name) {
            return data[i];
        }
    }
}//ShorthandfilteredData = data.find(data => data.type === 'data1' && data.name === 'fgh');
console.log(filteredData); // { type: 'data1', name: 'fgh' }
```

# 速记的按位索引

如果我们能把 indexof 方法和速记结合起来会怎么样？Bitwise indexof 为我们做了同样的工作。

```
//longhand
if (data.indexOf(item) > -1) { // item found
}
if (data.indexOf(item) === -1) { // item not found
}//shorthand
if (~data.indexOf(item)) { // item found
}
if (!~data.indexOf(item)) { // item not found
}
```

我们也可以使用 includes 函数。

```
if (data.includes(item)) { 
// true if the item found
}
```

[](/javascript-basics-4-different-ways-to-iterate-over-an-object-a5d16335cef) [## JavaScript 基础:迭代对象的 4 种不同方法

### 两分钟内掌握 JavaScript 基础知识。

javascript.plainenglish.io](/javascript-basics-4-different-ways-to-iterate-over-an-object-a5d16335cef) 

# Object.entries()

此功能有助于将对象转换为对象数组。

```
const data = {
    data1: 'abc',
    data2: 'cde',
    data3: 'efg'
};
const arr = Object.entries(data);
console.log(arr);//[
    ['data1', 'abc'],
    ['data2', 'cde'],
    ['data3', 'efg']
]
```

# Object.values()和 Object.keys()

迭代对象值会很有帮助。

```
const data = {
    data1: 'abc',
    data2: 'cde'
};
const arr = Object.values(data);
console.log(arr);//[ 'abc', 'cde']
```

Object.keys()有助于迭代对象中的键。

```
const data = {
    data1: 'abc',
    data2: 'cde'
};
const arr = Object.keys(data);
console.log(arr);//[ 'data1', 'data2']
```

# 双位速记

**(双非按位运算符方法仅适用于 32 位整数)**

```
// Longhand
Math.floor(1.9) === 1 // true// Shorthand
~~1.9 === 1 // true
```

# 多次重复一个字符串

这个字符串方法有助于一次又一次地重复相同的字符串值。

```
//longhand 
let data = '';
for (let i = 0; i < 5; i++) {
    data += 'data ';
}
console.log(str); // data data data data data//shorthand 
'data '.repeat(5);
```

# 找出数组中的最大值和最小值

```
const data = [1, 4, 3]; 
Math.max(…data); // 4
Math.min(…data); // 1
```

# 从字符串中获取字符

```
let str = 'test';
//Longhand 
str.charAt(2); // s//Shorthand 
Note: this is only works if we know the index of matched characterstr[2]; // c
```

# 超级速记

```
//longhandMath.pow(2,2); // 4//shorthand2**2 // 4
```

# 延伸阅读:

[](/most-commonly-used-string-methods-in-javascript-d24d5dd7073b) [## JavaScript 中最常用的字符串方法

### 最新 JavaScript 编码面试问题 2021

javascript.plainenglish.io](/most-commonly-used-string-methods-in-javascript-d24d5dd7073b) [](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [## 新引入的 JavaScript 特性可以提升您的知识

### 利用 ES2021 的新功能优化您的 JavaScript 代码。

javascript.plainenglish.io](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)