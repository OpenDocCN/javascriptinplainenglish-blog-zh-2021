# 加速编码的 5 个有用的 JavaScript 技巧

> 原文：<https://javascript.plainenglish.io/5-useful-javascript-tips-to-speed-up-your-coding-38c54c42e911?source=collection_archive---------3----------------------->

## 用 JavaScript 更快编码的 5 种方法和技巧。

![](img/d3373e1a2e6f748e8d72536217fe55ee.png)

Photo by [Safar Safarov](https://unsplash.com/@codestorm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

JavaScript 是软件开发中功能强大的编程语言之一。你可以用它做很多事情，比如网络应用、移动应用、游戏，甚至人工智能和机器学习。你只需要擅长它，因为每年都有新的有用的特性在 es 版本中发布。然而，作为一名开发人员，你还需要快速编写代码，因为你将有更多的其他任务比编写代码更重要。

在本文中，我们将发现一些有用的 JavaScript 技巧或技术来加速您的编码。让我们开始吧。

# 1.类型转换

在 JavaScript 中，要将字符串转换成数字，我们使用方法`parseInt()`。但是也有一种不使用`parseInt`的简单方法。

我们可以通过在字符串的开头使用一元操作符`+`来达到同样的结果。

看看下面的例子:

*正常方式:*

```
let age = "23";
console.log(typeof age); //string
console.log(typeof **parseInt**(age)); //number
```

*简单易行:*

```
let age = "23";
console.log(typeof age); //string
console.log(typeof **+age**); //number
```

您也可以将一个数字转换为一个字符串，只需将该数字与一个空字符串连接起来。

这里有一个例子:

```
let age = 19 + **""**;console.log(typeof age); //string
```

正如您所看到的，使用这种技术可以很容易地将数字转换成字符串。

# 2.使用三元运算符

三元运算符使得使用`?`和`:`编写条件语句更快。

看看下面的例子:

*普通条件语句:*

```
let age = 35;**if**(age < 30){
 console.log('below 30');
}**else if**(age > 40){
 console.log('above 40');
}**else**{
 console.log('between 30 and 40');
}
//Output: between 30 and 40
```

*三元运算符:*

```
let age = 35;age < 30 **?** console.log('below 30') 
**:** age > 40 ? console.log('above 40') 
**:** console.log('between 30 and 40');//Output: between 30 and 40
```

如您所见，我们用三元运算符只用了 3 行代码就编写了相同的代码。

# 3.使用控制台日志的简单方法

我见过开发者在有大量数据需要调试的时候，会使用大量的`console.log`方法。

这里有一个例子:

```
let user1 = {name : "Mehdi", age : 19};let user2 = {name : "John", age : 23};let user3 = {name : "Alex", age : 25};**console.log(user1);
console.log(user2);
console.log(user3);**
```

您可以用一种`console.log`方法记录这三个对象:

```
let user1 = {name : "Mehdi", age : 19};let user2 = {name : "John", age : 23};let user3 = {name : "Alex", age : 25};**console.log({user1, user2, user3});**
```

第二种方法减少了代码，比第一种方法更容易编写。不需要写很多`console.log`方法。

# 4.展平阵列的简单方法

我见过开发人员使用 filter、concat 和其他方法来展平多维数组。他们只需使用方法`flat()`就能轻松做到同样的事情。

看看下面的例子:

*正常方式:*

```
let arr = [6, [12, 3], [8, 5], 4];let numbersArr = [].concat(...arr);console.log(numbersArr); // [6, 12, 3, 8, 5, 4]
```

*简单易行:*

```
let arr = [6, [12, 3], [8, 5], 4];console.log(arr.**flat()**); // [6, 12, 3, 8, 5, 4]
```

正如您所看到的，flat 方法使它变得更加容易、快速和可读。这就是为什么我更喜欢用它。

# 5.总是使用析构

析构是 ES6 中引入的最好的特性之一。这使得处理对象和数组变得更加容易。

下面是析构如何在处理对象时加快编码速度:

*无解构:*

```
let user = {
 name : "Mehdi",
 age : 19,
 isOnline : true
}console.log(`${**user.name**} is ${**user.age**} years old.`);
// Mehdi is 19 years old.
```

*带解构:*

```
let user = {
name : "Mehdi",
age : 19,
isOnline : true
}
**const {name, age} = user;** console.log(`${**name**} is ${**age**} years old.`);
// Mehdi is 19 years old.
```

当您想在一个对象中访问很多值时，这更有意义。

下面是析构如何在处理数组时加快编码速度:

*正常方式:*

```
let a = [5, 6, 7];
let b = [1, 2, 3];console.log(a); //[5, 6, 7]
console.log(b); //[1, 2, 3]
```

*简单易行:*

```
**const [a, b] = [[5, 6 , 7], [1, 2, 3]];**console.log(a, b); //[5, 6, 7] [1, 2, 3]
```

如您所见，第二种方法避免了在大量变量中存储大量数组，这对性能有好处。也比第一部写起来容易多了。

# 结论

这些只是使你的代码更容易编写的简单提示。因此，这将加快您的编码速度。

感谢您阅读这篇文章。希望你觉得有用。

**延伸阅读**

[](https://js.plainenglish.io/the-difference-between-foreach-and-map-in-javascript-f369c3207e50) [## JavaScript 中 ForEach 和 Map 的区别

### JavaScript 方法:forEach VS map 及示例。

js .平原英语. io](https://js.plainenglish.io/the-difference-between-foreach-and-map-in-javascript-f369c3207e50)