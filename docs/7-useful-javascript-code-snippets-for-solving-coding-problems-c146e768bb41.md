# 解决编码问题的 7 个有用的 JavaScript 代码片段

> 原文：<https://javascript.plainenglish.io/7-useful-javascript-code-snippets-for-solving-coding-problems-c146e768bb41?source=collection_archive---------9----------------------->

## 您经常需要使用的 JavaScript 代码片段。

![](img/a82bfab22af7c0e96c51a774bd203042.png)

Photo by [Shamin Haky](https://unsplash.com/@haky?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

众所周知，JavaScript 是当今流行的编程语言之一，尤其是在 web 开发方面。JavaScript 生态系统中充满了框架和库，让开发人员的生活变得更加轻松。

然而，有时候你不需要总是使用框架和库来编写 JavaScript 代码。这就是为什么在本文中，我想与您分享一些有用的 JavaScript 代码片段来解决简单的问题。所以让我们开始吧。

# 1.数组中的随机项

要从数组中返回一个随机项或元素，我们需要使用带有 length 属性的方法`Math.random()`和`Math.floor()`。

这里有一个例子:

```
let cars = ['Ford', 'Ferrari', 'BMW', 'Toyota'];//Store a random array item in a variable.
let randomCar = cars[**Math.floor(Math.random()*** **cars.length)**];//Print the random item from car array.
console.log(randomCar); //returns random element
```

每当您再次运行代码时，数组中的一个新的随机元素将被打印到控制台。

# 2.检查参数是否为数字

在下面的例子中，我们将使用三种方法`isNaN()`、`parseFloat()`和`isFinite()`来检查函数参数是否为数字。

看一看:

```
function isNumber(number){
   return **!isNaN(parseFloat(number)) && isFinite(number)**;
}isNumber(5); //returns true
isNumber("Hello"); //returns false
```

# 3.轻松反转字符串

为了容易地反转一个字符串，我们可以使用方法`reverse()`，但是它只对数组有效。这就是为什么我们将使用`split()`将字符串转换为数组，反转它，然后使用`join()`方法将其转换回字符串。

下面是代码示例:

```
let str = "Hello World";**str.split("").reverse().join("")**; //returns 'dlroW olleH'
```

# 4.从二进制转换为普通文本

要使用 JavaScript 将二进制代码转换成普通文本，我们需要先将二进制代码转换成小数。然后，我们将使用方法`String.fromCharCode()`将小数转换成文本。

这里有一个例子:

```
function binaryToText(binary) {
//Convert binary into an array of strings separated by whitespace.    **binary = binary.split(' ');**//convert from binary to decimals to text. 
**return binary.map(elem => String.fromCharCode(parseInt(elem, 2))).join("")**;
}binaryToText("01001001 00100000 01101100 01101111 01110110 01100101 00100000 01001010 01100001 01110110 01100001 01010011 01100011 01110010 01101001 01110000 01110100"); **//returns I love JavaScript**binaryToText("01010100 01101000 01100001 01110100 00100111 01110011 00100000 01100111 01101111 01101111 01100100"); **//returns That's good**
```

# 5.计算数字的阶乘

为了计算一个数的阶乘，我们将使用带有三元运算符的箭头函数。如下例所示:

```
const getFactorial = num =>
 num < 0 ?
 (()=>{
   throw new TypeError('No negative numbers');
 })()
 : num <= 1
  ? 1
  : num * getFactorial(num - 1);//examples:
getFactorial(0); //returns 1
getFactorial(5); //returns 120
```

# 6.从数组中返回最小值和最大值

通过使用扩展操作符的方法`Math.max()`和`Math.min()`。我们可以很容易地从一组数字中得到最大值和最小值。

下面是代码示例:

```
let nums = [67, 99, 4, 2, 77];//minimum number
**Math.min(...nums);** //returns 2//maximum number
**Math.max(...nums)**; //returns 99
```

# 7.检查性能

如果你想检查一段代码运行和执行需要多少时间，你可以使用下面例子中的方法`performance.now()`:

```
var start = **performance.now()**;//Your piece of code starts here
for(let i = 0; i < 100; i++){
 console.log(i);
}
//Your piece of code ends herevar duration = **performance.now()** - **start**;console.log(duration); //54.89999961853027
```

上面的 for 循环执行起来只用了 54.89ms。

# 结论

正如你在上面看到的，这些是一些有用的代码片段，在某些情况下你可能需要在 JavaScript 中使用。你不需要总是使用库。

*感谢您阅读本文。此外，如果你发现我的内容有用，而你不是一个媒体成员，你可以抓住你的媒体成员* [*这里*](https://mehdiouss.medium.com/membership) *(媒体推荐链接)获得所有内容的无限访问和支持我们作为作家。*

**延伸阅读:**

[](/7-useful-css-cheat-sheets-to-improve-your-skills-66d7d3a7cc8) [## 7 个有用的 CSS 备忘单来提高你的技能

### 一个很棒的 CSS 备忘单列表，你可以作为一个 web 开发者使用。

javascript.plainenglish.io](/7-useful-css-cheat-sheets-to-improve-your-skills-66d7d3a7cc8) [](/5-useful-javascript-regex-methods-every-developer-must-know-20ebb5993c8) [## 每个开发人员都必须知道的 5 个有用的 JavaScript Regex 方法

### JavaScript 中必须知道的正则表达式方法列表。

javascript.plainenglish.io](/5-useful-javascript-regex-methods-every-developer-must-know-20ebb5993c8) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)