# 提高速度和效率的 20 大 JavaScript 技巧

> 原文：<https://javascript.plainenglish.io/top-20-javascript-tips-and-tricks-to-increase-your-speed-and-efficiency-5698375d9d36?source=collection_archive---------8----------------------->

## 方便和有用的技术，以减少代码行，加快您的开发工作！

在我们的日常任务中，我们要编写函数，比如排序、搜索、查找唯一值、传递参数、交换值等。因此，我在这里列出了我的速记技巧清单，以便像专家一样把它们都写出来！✌🏻

![](img/ee34186247724e2af1d820f3e912f154.png)

> JavaScript 确实是一个令人敬畏的💛学习和工作语言。对于给定的问题，可以有多种方法来达到相同的解决方案。在本文中，我们将只讨论最快的方法。🚀

这些方法肯定会帮助您:

*   减少代码行的数量，
*   编码比赛，
*   黑客马拉松或
*   其他有时间限制的任务。⏱

尽管最新版本是 ECMAScript11 (ES2020)，但这些 JavaScript 黑客大多使用 ECMAScript6 (ES2015)以后的技术。

*注意:以下所有技巧都已经在谷歌 Chrome 的控制台上测试过了。*

## 1.声明和初始化数组

我们可以用默认值初始化一个特定大小的数组，比如`""`、`null`或`0`。您可能已经将这些用于一维数组，但是如何初始化二维数组/矩阵呢？

```
const array = Array(5).fill(''); 
// Output 
(5) ["", "", "", "", ""]const matrix = Array(5).fill(0).map(()=>Array(5).fill(0)); 
// Output
(5) [Array(5), Array(5), Array(5), Array(5), Array(5)]
0: (5) [0, 0, 0, 0, 0]
1: (5) [0, 0, 0, 0, 0]
2: (5) [0, 0, 0, 0, 0]
3: (5) [0, 0, 0, 0, 0]
4: (5) [0, 0, 0, 0, 0]
length: 5
```

## 2.找出总和、最小值和最大值

我们应该利用`reduce`方法快速找到基本的数学运算。

```
const array  = [5,4,7,8,9,2];
```

*   总和

```
array.reduce((a,b) => a+b);
// Output: 35
```

*   最大

```
array.reduce((a,b) => a>b?a:b);
// Output: 9
```

*   福建话

```
array.reduce((a,b) => a<b?a:b);
// Output: 2
```

## 3.字符串、数字或对象的排序数组

我们内置了对字符串排序的方法`sort()`和`reverse()`，但是对数字或对象数组呢？
让我们看看数字和对象的升序和降序排序技巧。

*   排序字符串数组

```
const stringArr = ["Joe", "Kapil", "Steve", "Musk"]
stringArr.sort();
// Output
(4) ["Joe", "Kapil", "Musk", "Steve"]stringArr.reverse();
// Output
(4) ["Steve", "Musk", "Kapil", "Joe"]
```

*   排序数字数组

```
const array  = [40, 100, 1, 5, 25, 10];
array.sort((a,b) => a-b);
// Output
(6) [1, 5, 10, 25, 40, 100]array.sort((a,b) => b-a);
// Output
(6) [100, 40, 25, 10, 5, 1]
```

*   排序对象数组

```
const objectArr = [ 
    { first_name: 'Lazslo', last_name: 'Jamf'     },
    { first_name: 'Pig',    last_name: 'Bodine'   },
    { first_name: 'Pirate', last_name: 'Prentice' }
];
objectArr.sort((a, b) => a.last_name.localeCompare(b.last_name));
// Output
(3) [{…}, {…}, {…}]
0: {first_name: "Pig", last_name: "Bodine"}
1: {first_name: "Lazslo", last_name: "Jamf"}
2: {first_name: "Pirate", last_name: "Prentice"}
length: 3
```

## 4.需要从数组中过滤出错误值吗？

像`0`、`undefined`、`null`、`false`、`""`、`''`这样的假值可以通过下面的技巧轻松省略

```
const array = [3, 0, 6, 7, '', false];
array.filter(Boolean);
// Output
(3) [3, 6, 7]
```

## 5.对各种条件使用逻辑运算符

如果要减少嵌套的 If..否则或切换情况下，您可以简单地使用基本的逻辑运算符`AND/OR`。

```
function doSomething(arg1){ 
    arg1 = arg1 || 10; 
// set arg1 to 10 as a default if it’s not already set
return arg1;
}let foo = 10;  
foo === 10 && doSomething(); 
// is the same thing as if (foo == 10) then doSomething();
// Output: 10foo === 5 || doSomething();
// is the same thing as if (foo != 5) then doSomething();
// Output: 10
```

## 6.删除重复值

您可能已经将`indexOf()`与返回第一个找到的索引的 for 循环一起使用，或者使用一个较新的从数组返回布尔值 true/false 的`includes()`来找出/删除重复项。我们有两种更快的方法。

```
const array  = [5,4,7,8,9,2,7,5];
array.filter((item,idx,arr) => arr.indexOf(item) === idx);
// or
const nonUnique = [...new Set(array)];
// Output: [5, 4, 7, 8, 9, 2]
```

## 7.创建计数器对象或映射

大多数情况下，需要通过创建一个计数器对象或映射来解决问题，该对象或映射将变量作为键，将它们的频率/出现次数作为值来跟踪。

```
let string = 'kapilalipak';const table={}; 
for(let char of string) {
  table[char]=table[char]+1 || 1;
}
// Output
{k: 2, a: 3, p: 2, i: 2, l: 2}
```

和

```
const countMap = new Map();
  for (let i = 0; i < string.length; i++) {
    if (countMap.has(string[i])) {
      countMap.set(string[i], countMap.get(string[i]) + 1);
    } else {
      countMap.set(string[i], 1);
    }
  }
// Output
Map(5) {"k" => 2, "a" => 3, "p" => 2, "i" => 2, "l" => 2}
```

## 8.三元运算符很酷

如果…你可以避免嵌套条件。else…if…else…if 带三元运算符。

```
function Fever(temp) {
    return temp > 97 ? 'Visit Doctor!'
      : temp < 97 ? 'Go Out and Play!!'
      : temp === 97 ? 'Take Some Rest!';
}// Output
Fever(97): "Take Some Rest!" 
Fever(100): "Visit Doctor!"
```

## 9.与传统循环相比，for 循环速度更快

*   默认情况下，`for`和`for..in`获取索引，但是您可以使用 arr[index]。
*   `for..in`也接受非数字，所以要避免。
*   `forEach`，`for...of`直接获取你元素。
*   `forEach`能让你指数还而`for...of`不能。
*   `for`和`for...of`考虑数组中的孔洞，而另外两个不考虑。

## 10.合并 2 个对象

在日常工作中，我们经常需要合并多个对象。

```
const user = { 
 name: 'Kapil Raghuwanshi', 
 gender: 'Male' 
 };
const college = { 
 primary: 'Mani Primary School', 
 secondary: 'Lass Secondary School' 
 };
const skills = { 
 programming: 'Extreme', 
 swimming: 'Average', 
 sleeping: 'Pro' 
 };const summary = {...user, ...college, ...skills};// Output 
gender: "Male"
name: "Kapil Raghuwanshi"
primary: "Mani Primary School"
programming: "Extreme"
secondary: "Lass Secondary School"
sleeping: "Pro"
swimming: "Average"
```

## 11.箭头功能

arrow 函数表达式是传统函数表达式的一种紧凑替代形式，但它有局限性，不能在所有情况下使用。因为它们有一个词法作用域(父作用域),没有自己的`this`和`arguments`,所以它们引用定义它们的环境。

```
const person = {
name: 'Kapil',
sayName() {
    return this.name;
    }
}
person.sayName();
// Output
"Kapil"
```

但是

```
const person = {
name: 'Kapil',
sayName : () => {
    return this.name;
    }
}
person.sayName();
// Output
""
```

## 12.可选链接

可选链接？。如果之前的值为。。为 undefined 或 null 并返回 undefined。

```
const user = {
  employee: {
    name: "Kapil"
  }
};
user.employee?.name;
// Output: "Kapil"
user.employ?.name;
// Output: undefined
user.employ.name
// Output: VM21616:1 Uncaught TypeError: Cannot read property 'name' of undefined
```

## 13.打乱数组

利用内置的`Math.random()`方法。

```
const list = [1, 2, 3, 4, 5, 6, 7, 8, 9];
list.sort(() => {
    return Math.random() - 0.5;
});
// Output
(9) [2, 5, 1, 6, 9, 8, 4, 3, 7]
// Call it again
(9) [4, 1, 7, 5, 3, 8, 2, 9, 6]
```

## 14.零融合算子

零化合并算子(？？)是一种逻辑运算符，当其左侧操作数为空或未定义时，返回右侧操作数，否则返回左侧操作数。

```
const foo = null ?? 'my school';
// Output: "my school"const baz = 0 ?? 42;
// Output: 0
```

## 15.休息和传播运营商

那些神秘的 3 个点`...`可以休息也可以扩散！🤓

```
function myFun(a,  b, ...manyMoreArgs) {
   return arguments.length;
}
myFun("one", "two", "three", "four", "five", "six");// Output: 6
```

和

```
const parts = ['shoulders', 'knees']; 
const lyrics = ['head', ...parts, 'and', 'toes']; lyrics;
// Output: 
(5) ["head", "shoulders", "knees", "and", "toes"]
```

## 16.默认参数

```
const search = (arr, low=0,high=arr.length-1) => {
    return high;
}
search([1,2,3,4,5]);// Output: 4
```

## 17.将十进制转换为二进制或六进制

我们可以使用一些内置的方法，如`.toPrecision()`或`.toFixed()`来实现很多帮助功能，同时解决问题。

```
const num = 10;num.toString(2);
// Output: "1010"
num.toString(16);
// Output: "a"
num.toString(8);
// Output: "12"
```

## 18.使用析构简单交换 2 个值

```
let a = 5;
let b = 8;
[a,b] = [b,a][a,b]
// Output
(2) [8, 5]
```

## 19.单行回文检查

这不是一个简单的技巧，但是它会给你一个清晰的思路去弹奏琴弦。

```
function checkPalindrome(str) {
  return str == str.split('').reverse().join('');
}
checkPalindrome('naman');
// Output: true
```

## 20.将对象属性转换为属性数组

使用`Object.entries()`、`Object.keys()`和`Object.values()`

```
const obj = { a: 1, b: 2, c: 3 };Object.entries(obj);
// Output
(3) [Array(2), Array(2), Array(2)]
0: (2) ["a", 1]
1: (2) ["b", 2]
2: (2) ["c", 3]
length: 3Object.keys(obj);
(3) ["a", "b", "c"]Object.values(obj);
(3) [1, 2, 3]
```

伙计们，现在就这样吧！🤗

如果你知道更多类似上面的技巧，让我们通过 [GitHub 库](https://github.com/kapilraghuwanshi/quick-javascript-tips-tricks-hacks)合作，这样我们可以一起学习它们。

如果您真的从这篇文章中学到了一些新东西，或者它真的让您的开发工作比以前更快了，那么请喜欢它，将它加入书签，并与您的同事分享。希望你们会喜欢它！🤩

> *让我们在* [*LinkedIn*](https://www.linkedin.com/in/kapilraghuwanshi/) *和*[*Twitter*](https://www.twitter.com/techygeeeky)*上连线，了解更多此类引人入胜的科技文章和教程。🤝*

*更多内容看* [***说白了. io***](http://plainenglish.io/)