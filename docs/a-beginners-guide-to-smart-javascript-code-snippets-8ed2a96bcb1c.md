# 智能 JavaScript 代码片段初学者指南

> 原文：<https://javascript.plainenglish.io/a-beginners-guide-to-smart-javascript-code-snippets-8ed2a96bcb1c?source=collection_archive---------16----------------------->

## 成为 JavaScript 专家的技巧

![](img/8ac7fb2bcfb468d6e2993c26813afe11.png)

Photo by [Mario Gogh](https://unsplash.com/@mariogogh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为开发人员，我们都必须知道如何让我们的代码工作。但是有多少次我们试图保持我们的代码简洁明了呢？你必须记住每一行代码都可能导致一个额外的问题——所以你必须对每一行代码保持警惕。每一行巧妙编写的代码都可以很容易地帮助您的大型应用程序运行良好，因为更少的代码在您的浏览器上会更容易。

这里有一些编写智能 JavaScript 代码的技巧。

# **1。短路评估**

如果你想评估一个你需要使用的变量是否不是`null`或者`undefined`或者为空，那么你需要用一种简单的方法来评估更小的代码。手写的方式大概是这样的—

```
if (var1 !== null || var1 !== undefined || var1 !== '') { console.log(var1);}
```

简而言之就是—

```
if(var1) { console.log(var1);}
```

# **2。隐式返回**

考虑一个函数，它只是进行某种计算并返回某个值，比如—

```
function calcuateArea() { return length * width;}
```

这个函数可以用箭头函数重写为一行——

```
calcuateArea = area => length * width;
```

# **3。展开运算符**

在处理数组时，Spread 操作符使我们避免了许多错误。spread 运算符是一种有用而快速的语法，用于向数组中添加项、组合数组或对象，以及将数组扩展到函数的参数中。

看看我们通常是如何向数组中添加元素以及克隆数组的—

```
const numbers = [4,5,6];// adding elements to the arrayconst numGroup = [1,2,3].concat(numbers);//cloning an arrayconst newNum = numbers.slice();
```

这可以用扩展运算符来代替—

```
const numbers = [4,5,6];// adding elements to the arrayconst numGroup = [1,2,3, …numbers];//cloning an arrayconst newNum = […numbers];
```

# **4。模板文字**

向任何字符串添加变量的老套方法是使用`+`操作符，很长一段时间我也是这么做的。

```
const errorMsg = 'Please upload a valid file. The error with the file is ' + exception.message;
```

ES6 给了我们一个聪明的方法来添加这样的变量到一个字符串中，就是使用模板文字(${}和` ` ),就像—

```
const errorMsg = `Please upload a valid file. The error with the file is ${exception.message}`;
```

# **5。多行字符串**

长文本会导致 lint 错误，所以我们不用`+`操作符来添加多行，而是使用反勾(```)操作符，就像—

```
const longText = `Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry’s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.`;
```

# **6。寻找数组中的元素**

我们通常遍历一个数组来寻找满足某个条件的元素—

```
const fruits = [‘Apple’, ‘Orange’, ‘Strawberry’, ‘Blueberry’, ‘PineApple’, ‘Avocado’];function findApple() { for(let i=0; i<fruits.length; i++) { if(fruits[i] === ‘Apple’) { return fruits[i]; } }}
```

不用遍历数组，使用 arrow 函数就可以很容易地做到—

```
findApple = fruit => ( fruits.find(aFruit => aFruit === ‘Apple’))
```

# **7。在数组中过滤**

如果你需要过滤一个对象数组，你可能已经知道了一般的方法，那就是反复检查每个元素，比如

```
const fruits = [ { name: ‘Apple’, color: ‘Red’ }, { name: ‘Orange’, color: ‘Orange’ }, { name: ‘Strawberry’, color: ‘Red’ }, { name: ‘Blueberry’, color: ‘Blue’}] function filterRedFruits() { let redFruits = []; for(let i=0; i<fruits.length; i++) { if(fruits[i].color === ‘Red’) { redFruits.push(fruits[i]); } } return redFruits;}
```

这可以很容易地用 filter 操作符写成—

```
let redFruits = fruits.filter(function(fruit) { return fruit.color === ‘Red’;})
```

# **结论**

这些都是提高 JavaScript 代码性能的非常小的方法，更多的技巧和窍门请查看我的其他文章

[](/stop-writing-javascript-like-this-a7fafbe451a5) [## 不要再这样写 JavaScript 了

### 写出更好的 JavaScript 代码的 10 种方法

javascript.plainenglish.io](/stop-writing-javascript-like-this-a7fafbe451a5) [](/8-useful-javascript-tricks-you-should-definitely-know-1b2c45d9ce2a) [## 你绝对应该知道的 8 个有用的 JavaScript 技巧

### 你可能没见过这些

javascript.plainenglish.io](/8-useful-javascript-tricks-you-should-definitely-know-1b2c45d9ce2a) [](/5-tips-to-write-better-javascript-31c6da86cc72) [## 编写更好的 JavaScript 的 5 个技巧

### 成为更好的开发人员的指南

javascript.plainenglish.io](/5-tips-to-write-better-javascript-31c6da86cc72) 

另外，如果你知道更多写更好的 JS 代码的方法，请留言。注意安全，善待他人！:)

*更多内容看*[***plain English . io***](http://plainenglish.io/)