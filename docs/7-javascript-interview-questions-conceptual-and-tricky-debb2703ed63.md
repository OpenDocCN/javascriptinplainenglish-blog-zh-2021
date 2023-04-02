# 7 个 JavaScript 面试问题——概念性的和棘手的

> 原文：<https://javascript.plainenglish.io/7-javascript-interview-questions-conceptual-and-tricky-debb2703ed63?source=collection_archive---------5----------------------->

![](img/5346a18b87f2cd97212a9a4dcc47f1bd.png)

在本文中，我们将讨论一些常见的基于概念的 JavaScript 面试问题。有许多简单的问题乍看起来很棘手。清楚地理解这些概念可能有助于我们克服这些棘手的问题。

在参加了几次前端开发人员的面试后，我写了这篇文章。希望这能帮助你为面试做好准备…

> ***1。理解闭包、超时和作用域的概念。***
> 
> ***闭包:*** 简单来说，这意味着一个函数内部的变量和属性是该函数独占的，但是该函数可以访问外部的属性。

这听起来很简单，但是当你的面试官问你一个基于类似下面代码的问题时，困难就出现了。

```
for (var i = 0;  i < 5;  i++) {
    setTimeout(function log(){
        console.log(i);
    }, 1000);
}
```

不，上面代码的输出不是 0 1 2 3 4。

当我们运行这个时，它们都是 5。原因是`console.log(i)`会立即执行并引用 console.log 中(I)的值。然而，一秒钟后，整个循环已经经历了每一次迭代，变量(I)在每一次迭代中都被覆盖。

这里，setTimeout 函数创建一个函数(闭包),它可以访问其外部作用域，即包含索引(I)的循环。迭代之后，执行函数并打印出(I)的值，在循环结束时，该值为 5。这里的问题是，在第一个 setTimeout()运行的时候，(I)已经在 5 了，没有办法引用它。

**解决方案:**解决此问题的两种简单方法是:

a.通过创建一个立即调用的函数表达式(IIFE):

```
for (var i = 0; i < 5; i++) {
   setTimeout((function(param){
        console.log(i);
    })(i), 1000);
}
```

b.通过使用 ES6 功能“let”，它为您提供了一个数据块范围。

```
for (let i = 0;  i < 5;  i++) {
    setTimeout(function log() {
        console.log(i);
    }, 1000);
}
```

上面的解决方案工作得很好，也就是说，你得到的输出是 0，1，2，3，4。

**附加:**此处输出同时显示。如果要求您让输出中的每个数字在一秒钟的间隔后显示出来，该怎么办？

这是解决办法。setTimeout 的第二个参数需要乘以(I)。

```
for (let i = 0;  i < 5;  i++) {
    setTimeout(function log() {
        console.log(i);
    }, i*1000);
}
```

> **②*。理解使用数字数组的排序方法。***
> 
> **方法对数组中的元素进行排序并返回排序后的数组。默认的排序顺序是升序，基于**将元素转换成字符串**，然后比较它们的 UTF-16 代码单元值序列。**

**假设有一组数字需要排序。下面的代码应该返回什么作为输出？**

```
**var myArray = [45,10,21,54,1,55,100];
myArray.sort();**
```

**如果你的猜测是这会输出为[1，10，21，45，54，55，100]，那么你就不对。不幸的是，对数字进行排序并不那么简单。如果我们将 sort 方法直接应用于 numbers 数组，我们将会看到一个意外的结果。**

**默认情况下，sort 方法按字母顺序对元素进行排序。上面排序数字数组的方法不能正确排序数组。**

****解决方案:**数字排序添加一个新方法来处理数字排序。**

**a.以下升序排序的输出:[1，10，21，45，54，55，100]**

```
**myArray.sort((a, b) => a - b);**
```

**b.以下升序排序的输出:[100，55，54，45，21，10，1]**

```
**myArray.sort((a, b) => b - a);**
```

> *****3。编写一个函数来检查给定的参数是偶数还是奇数，而不使用任何条件语句*****
> 
> **这是一个逻辑问题，用来检验你解决某个问题的方法。**

**担心如何在不使用 if-else 或三元的情况下执行检查。嗯，这个解决方案很有趣，也很怪异，足以让你在面试中思考几分钟。**

**解决方案:这个问题的解决方案是使用数组或对象。**

```
**function checkNumber(num){
    const check = ['even', 'odd'];
    console.log(`${num} is ${check[num%2]}`);
}checkNumber(6); // 6 is even
checkNumber(5); // 5 is odd**
```

> *****4。Slice 是一种内置的方法，可以用来在面试中欺骗你。*****
> 
> **我们都知道 **Slice()** 方法将数组的一部分的浅拷贝返回到一个从头到尾选中的新数组对象中。原始数组不会被修改。**

**但是，如果我们在将新值压入数组之前使用 slice while 提取数组值，会发生什么情况呢？**

**下面给出的代码是执行的代码片段，它可能不会给你想要的输出。**

```
**var obj = {
    name : 'Sourabh',
    sports : ['Chess', 'Football', 'Snooker']
}var mySports= obj.sports.slice();
obj.sports.push('Bowling');
console.log(mySports);**
```

**如果你的猜测是输出为[“国际象棋”、“足球”、“斯诺克”、“保龄球”]，那你就错了。但是如果你的猜测是[“保龄球”]，那么是的，你又错了。**

****解:**输出为[“象棋”、“足球”、“斯诺克”]。**

**原因是尽管数组是一个引用类型，我们仍然使用 slice 方法为数组创建一个新的引用指针。**

> *****5。识别全局和局部变量。*****
> 
> ****局部变量**是在函数中定义的变量。它们有局部作用域，这意味着它们只能在定义它们的函数中使用。**
> 
> ****全局变量**是在函数之外定义的变量。这些变量具有全局范围，因此它们可以被任何函数使用，而不需要将它们作为参数传递给函数。**

**下面是需要识别全局和局部变量的代码。**

```
**function myFunc() {
    let x = y = 0;
    return x += 1;
}myFunc();
console.log(typeof x);
console.log(typeof y);**
```

****解:**这里‘x’是局部变量，as‘y’是全局变量。**

**因此，x 的类型是“未定义的”。变量 x 存在于 myFunc()范围内，在范围外不可用。其中 y 是值为 0 的全局变量，y 的类型是“数字”。**

**你可以像下面给出的那样理解上面的代码。**

```
**function myFunc() {
    let x;
    window.y = 0;
    x= window.y;
    return x+= 1;
}myFunc();
typeof x;
typeof window.y;**
```

> *****6。失去“这个”。*****
> 
> ****‘this’**关键字指的是一个对象，这个对象正在执行当前的 javascript 代码。换句话说，每个 javascript 函数在执行时都有一个对其当前执行上下文的引用，称为“this”。**

**下面是使用“this”来引用相同范围内的值的代码，它应该显示问候消息。**

```
**let greeting = {
    message: 'Good morning!', 
    name: 'Sourabh',displayMessage() {
        console.log(`Hello ${this.name}, ${this.message}`);
    }
};setTimeout(greeting.displayMessage, 1000);;**
```

**不幸的是，它给出的输出是 Hello undefined，undefined。**

**这里，setTimeout()函数使用 greeting.displayMessage 作为回调，但它调用 greeting.displayMessage 作为常规函数，而不是方法。在常规的函数调用中，这相当于全局对象，在浏览器环境中是窗口。**

****解决方案:**我们既可以使用包装函数，也可以使用内置方法 bind。**

**a.使用包装函数。**

**这将起作用，因为它从外部词法环境接收问候，然后正常调用该方法。**

```
**let greeting = {
    message: 'Good morning!', 
    name: 'Sourabh',displayMessage() {
        console.log(`Hello ${this.name}, ${this.message}`);
    }
};setTimeout(function() {
  greeting.displayMessage();
}, 1000);**
```

**b.可以使用 Bind 关键字。**

**这里我们采用方法 greeting.displayMessage 并将其绑定到 greeting。displayMessage 是一个“绑定”函数，可以单独调用，也可以传递给 setTimeout(没关系，上下文是对的)。**

```
**let greeting = {
    message: 'Good morning!', 
    name: 'Sourabh',displayMessage() {
        console.log(`Hello ${this.name}, ${this.message}`);
    }
};let welcomeMessage = greeting.displayMessage.bind(greeting);setTimeout(welcomeMessage, 1000);**
```

> *****7。JavaScript 中的单例模式*****
> 
> **在 JavaScript 上下文中，Singleton 是一个对象，用于创建名称空间并将一组相关的方法和属性组合在一起(封装)，如果我们允许启动，那么它只能启动一次。**

**我能想到的最简单的方法是创建一个消耗更少时间的单例模式，同时避免面试中的交叉提问，如下所示。**

```
**function getInstance() {
  if(typeof instance === 'object') {
   console.log("object exists");
    return instance;
  }
  instance = this
}var a = new getInstance();
var b = new getInstance(); // object exists
var c = new getInstance(); // object exists**
```

**如果您不知道这些，那么您可能至少在 JavaScript 知识方面有了一点进步。如果你都知道，那么希望这是一次练习和增长知识的尝试。**

**祝你面试好运。享受阅读…谢谢！**

***最初发表于*[*https://codersread.com*](https://codersread.com/improve-performance-of-web-application-react-js/)**

***更多内容请看*[***plain English . io***](http://plainenglish.io/)**