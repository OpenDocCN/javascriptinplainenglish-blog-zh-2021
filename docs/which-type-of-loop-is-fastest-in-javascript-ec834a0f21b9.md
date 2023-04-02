# JavaScript 中哪种类型的循环速度最快？

> 原文：<https://javascript.plainenglish.io/which-type-of-loop-is-fastest-in-javascript-ec834a0f21b9?source=collection_archive---------0----------------------->

了解哪个 for 循环或迭代器适合您的需求，并防止您犯愚蠢的错误，影响您的应用程序性能。

![](img/9ca855e63138414ed78001ea59b785e7.png)

Photo by [Artem Sapegin](https://unsplash.com/@sapegin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 web 开发的新感觉。不仅仅是 NodeJS、React、Angular Vue 等 JS 框架。但是，香草 JS 也有一个庞大的粉丝群。先说现代 JavaScript。循环一直是大多数编程语言的重要组成部分。现代 JS 给了你很多方法来迭代或循环你的值。

但问题是，你真的知道哪个循环或迭代最适合你的需求吗？for loops 有很多选项，`for`，`for(reverse)`，`for...of`，`foreach`，`for...in`，`for...await`。本文将涉及这样一场辩论。

# 哪个 for 循环更快？

**回答:** `for (reverse)`

最令人惊讶的是，当我在本地机器上测试时，我开始相信`for (reverse)`是所有 for 循环中最快的。让我分享一个例子。取一个超过一百万个条目的`array`，执行一个循环。

***免责声明*** *: console.time()结果准确性高度依赖于您的系统配置。仔细查看准确度* [*这里*](https://johnresig.com/blog/accuracy-of-javascript-time/) *。*

```
const million = 1000000; 
const arr = Array(million);console.time('⏳');

for (let i = arr.length; i > 0; i--) {} // for(reverse) :- 1.5msfor (let i = 0; i < arr.length; i++) {} // for          :- 1.6ms

arr.forEach(v => v)                     // foreach      :- 2.1msfor (const v of arr) {}                 // for...of     :- 11.7ms

console.timeEnd('⏳');
```

原因:在这里，正向和反向 for 循环花费的时间几乎相同。只有 0.1 毫秒的差别，因为`for(reverse)`只计算一次起始变量`let i = arr.length`。在前向`for`循环中，它在变量每次增加后检查条件`i < arr.length`。这一点点差别都无所谓，可以忽略。

另一半`foreach`是一个数组原型的方法。与普通的`for`循环相比，`foreach`和`for...of`在数组的迭代上花费了更多的时间。

# 循环的类型，以及应该在哪里使用它们

## 1.For 循环(正向和反向)

可能大家都很熟悉这个循环。您可以使用`for`循环，在您需要的地方，运行一个重复的代码块来固定计数器时间。传统的`for`循环是最快的，所以你应该一直使用它，对吗？没那么快——性能不是唯一重要的东西。代码可读性通常更重要，所以默认适合你的应用的风格。

## 2.为每一个

这个方法接受一个回调函数作为输入参数，对于数组中的每个元素，这个回调函数都会执行。同样，`foreach`回调函数接受当前值和各自的索引。`foreach`此外，允许在回调函数中使用`this`作为可选参数。

```
const things = ['have', 'fun', 'coding'];const callbackFun = (item, idex) => {
    console.log(`${item} - ${index}`);
}things.foreach(callbackFun); o/p:- have - 0
      fun - 1
      coding - 2
```

注意:-如果你使用`foreach`，你不能利用 JavaScript 中的短路。如果你不知道短路，让我给你介绍。当我们在 JavaScript 中使用像`AND(&&)`、`OR(||)`这样的逻辑操作符时，它将帮助我们提前终止和/或跳过一个循环的迭代。

## 3.为了…的

`for...of`在 ES6(ECMAScript 6)中是标准化的。`for...of`创建一个循环，在一个可迭代的对象上迭代，比如数组、映射、集合、字符串等。这个循环的另一个优点是可读性更好。

```
const arr = [3, 5, 7];
const str = 'hello';for (let i of arr) {
   console.log(i); // logs 3, 5, 7
}for (let i of str) {
   console.log(i); // logs 'h', 'e', 'l', 'l', 'o'
}
```

注意:-不要在发电机上重复使用`for...of`，即使`for...of`提前终止。退出循环后，生成器被关闭，再次尝试重复它不会产生进一步的结果。

## 4.为了…在

`for...in`在一个对象的所有可枚举属性上迭代一个指定的变量。对于每个不同的属性，`for...in`语句除了返回数字索引之外，还将返回用户定义属性的名称。

因此，在迭代数组时，最好使用传统的带数字索引的`for`循环。因为`for...in`语句除了迭代数组元素之外，还迭代用户定义的属性，即使修改数组对象(比如添加自定义属性或方法)。

```
const details = {firstName: 'john', lastName: 'Doe'};
let fullName = '';for (let i in details) {
    fullName += details[i] + ' '; // fullName: john doe
}
```

`for..of`和`for...in`的区别

`for..of`和`for...in`的主要区别在于它们迭代的内容。`for...in`循环迭代对象的属性，而`for...of`循环迭代可迭代对象的值。

```
let arr= [4, 5, 6];

for (let i in arr) {
   console.log(i); // '0', '1', '2'
}

for (let i of arr) {
   console.log(i); // '4', '5', '6'
}
```

![](img/b82444f0ee287daf9db6e28e24088ff6.png)

Photo by [Tine Ivanič](https://unsplash.com/@tine999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 结论

*   `for`速度最快，但可读性差。
*   `foreach`快速，对迭代属性的控制。
*   `for...of`缓慢，但更甜。
*   `for...in`慢，不那么得心应手。

最后，给你一个明智的建议。把你的优先级设置为可读性。当你开发一个复杂的结构时，代码的可读性是必不可少的，但是你也应该关注性能。尽量避免在代码中添加不必要的额外装饰，有时这会影响应用程序的性能。祝你编码愉快。