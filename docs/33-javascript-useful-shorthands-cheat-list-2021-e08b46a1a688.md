# 2021 年你应该知道的 JavaScript 顶级优化技术

> 原文：<https://javascript.plainenglish.io/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688?source=collection_archive---------2----------------------->

## 使用现代速记技术、技巧和诀窍优化您的 JavaScript 代码。

![](img/4ac6c09044f6d50e1c85335b2f90fb42.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名开发人员，我体会到学习是一个持续的过程。由于新技术和升级每年都会出现，我们需要相应地更新以充分利用它。

今天，我分享了一份备忘单，它帮助我简化了一些代码，也让我的代码更具可读性。

***注:*** *有时速记会让不了解代码的开发人员更难理解代码*😊*。*

> 那我们来看一下名单。

# 1.如果速记

大量使用 If 语句是否已经让你感到厌烦？让我们检查一些可以在这里有所帮助的选项

```
//longhandif (fruit === 'apple' || fruit === 'banana' || fruit === 'orange' || fruit ==='mango') {
    //logic
}//shorthandif (['apple', 'banana', 'orange', 'mango'].includes(fruit)) {
   //logic
}
```

# 2.如果…否则速记

当我们有 if-else 语句时，这一条会有所帮助。(确保您有最多 2-3 个，如果..否则会降低代码的可读性)

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

# 3.变量声明

当我们有相同类型的变量时，我们可以避免写两次。

```
//Longhand 
let data1;
let data2= 1;//Shorthand 
let data1, data2= 1;
```

# 4.检查非空值

如果我们想检查变量不为空呢？我们现在可以不用再写所有条件了。

```
// Longhand
if (data1 !== null || data1!== undefined || data1 !== '') {
    let data2 = data1;
}// Shorthand
let data2 = data1 || '';
```

# 5.分配默认值

```
let data1 = null,
    data2 = test1 || '';console.log("null check", data2); // output will be ""
```

# 6.未定义的值检查

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

# 7.零操作符

如果左侧为空或未定义，此运算符将返回右侧的值。

```
const data= null ?? 'data';
console.log(data);
// expected output: "data"const data1 = 1 ?? 4;
console.log(data1);
// expected output: 1
```

# 8.赋值

```
//Longhand 
let data1, data2, data3;
data1 = 1;
data2 = 2;
data3 = 3;//Shorthand 
let [data1, data2, data3] = [1, 2, 3];
```

# 9.赋值运算符

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

# 10.无效支票

最常用的操作数之一，但要确保您的值为 true、非空字符串、已定义的值和非空值。

```
// Longhand
if (data1 === true) or if (data1 !== "") or if (data1 !== null)// Shorthand //
if (test1)
```

注意:如果 test1 有任何值，它将落入 If 循环后的逻辑中，该操作符主要用于空值或未定义的检查。

# 11.AND(&&)运算符

如果我们想避免一个 If 语句，那么这个简写将是有帮助的

```
//Longhand 
if (test1) {
 callMethod(); 
}//Shorthand 
test1 && callMethod();
```

# 12.返回速记

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
} // Shorthand
function returnMe() {
    return value || callFunction('value');
}
```

# 13.箭头功能

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

# 14.简短的函数调用

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

# 15.开关状态优化

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

# 16.隐性回报

即使不编写返回语句，箭头函数也有助于返回值。酷吧？

```
//longhandfunction calculate(diameter) {
  return Math.PI * diameter
}//shorthandcalculate = diameter => (
  Math.PI * diameter;
)
```

# 17.十进制基数指数

```
// Longhand
for (var i = 0; i < 100000; i++) { ... }// Shorthand
for (var i = 0; i < 1e5; i++) {
```

# 18.默认参数值

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

# 19.传播算子

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

# 20.模板文字

如果你正在寻找在字符串中追加多个值的简写方法，那么这个简写方法正适合你。

```
//longhandconst literal = 'Hi ' + data1 + ' ' + data2 + '.'//shorthandconst literal= `Hi ${data1} ${data2}`;
```

# 21.多行字符串

```
//longhandconst literal = 'abc abc abc abc abc abc\n\t'
    + 'val test,test test test test\n\t'//shorthandconst literal = `abc abc abc abc abc abc
         val test,test test test test`
```

# 22.对象属性分配

```
let data1 = 'abcd'; 
let data2 = 'efgh';//Longhand 
let data = {data1: data1, data2: data2}; //Shorthand 
let data = {data1, data2};
```

# 23.数转换

```
//Longhand 
let test1 = parseInt('12'); 
let test2 = parseFloat('2.33');//Shorthand 
let test1 = +'12'; 
let test2 = +'2.33';
```

# 24.解构分配

```
//longhand
const data1 = this.data.data1;
const data2 = this.data.data2;
const data2 = this.data.data3;//shorthand
const { data1, data2, data3 } = this.data;
```

# 25.Array.find 方法

从数组中找到第一个匹配值的方法之一..

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

# 26.速记的按位索引

如果我们能把 indexof 方法和速记结合起来会怎么样？按位索引为我们做同样的工作。

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

我们也可以使用包含函数。

```
if (data.includes(item)) { 
// true if the item found
}
```

# 27.Object.entries()

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

# 28.Object.values()和 Object.keys()

迭代对象值会很有帮助。

```
const data = {
    data1: 'abc',
    data2: 'cde'
};
const arr = Object.values(data);
console.log(arr);//[ 'abc', 'cde'] 
```

Object.keys()有助于迭代 Object 中的键

```
const data = {
    data1: 'abc',
    data2: 'cde'
};
const arr = Object.keys(data);
console.log(arr);//[ 'data1', 'data2']
```

# 29.双位速记

**(双非按位运算符方法仅适用于 32 位整数)**

```
// Longhand
Math.floor(1.9) === 1 // true// Shorthand
~~1.9 === 1 // true
```

# 30.多次重复一个字符串

这个字符串方法有助于一次又一次地重复相同的字符串值

```
//longhand 
let data = '';
for (let i = 0; i < 5; i++) {
    data += 'data ';
}
console.log(str); // data data data data data //shorthand 
'data '.repeat(5);
```

# 31.找出数组中的最大值和最小值

```
const data = [1, 4, 3]; 
Math.max(…data); // 4
Math.min(…data); // 1
```

# 32.从字符串中获取字符

```
let str = 'test';
//Longhand 
str.charAt(2); // s//Shorthand 
Note: this is only works if we know the index of matched characterstr[2]; // c
```

# 33.超级速记

```
//longhandMath.pow(2,2); // 4//shorthand2**2 // 4
```

*更多内容尽在*[plain English . io](http://plainenglish.io/)

## 如果你喜欢并想获得更多这样的内容，请订阅

# 延伸阅读:

[](/most-commonly-used-string-methods-in-javascript-d24d5dd7073b) [## JavaScript 中最常用的字符串方法

### 最新 JavaScript 编码面试问题 2021

javascript.plainenglish.io](/most-commonly-used-string-methods-in-javascript-d24d5dd7073b) [](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [## 新引入的 JavaScript 特性可以提升您的知识

### 利用 ES2021 的新功能优化您的 JavaScript 代码。

javascript.plainenglish.io](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9)