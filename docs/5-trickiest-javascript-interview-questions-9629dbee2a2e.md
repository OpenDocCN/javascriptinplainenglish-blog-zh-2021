# 5 个最棘手的 JavaScript 面试问题

> 原文：<https://javascript.plainenglish.io/5-trickiest-javascript-interview-questions-9629dbee2a2e?source=collection_archive---------1----------------------->

## 用这 5 个最常见的 JavaScript 面试问题来测试你的 JavaScript 技能。

![](img/10acc78f9ad5fa0ca68fb634d93030a0.png)

Photo by [Michał Parzuchowski](https://unsplash.com/@mparzuchowski?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你是一个想换工作的前端开发人员吗？你在考虑别人可能会问的棘手问题吗？或者你是一名高级 JavaScript 开发人员，正在寻找听起来有点棘手的面试问题？不要担心，如果上述两个问题都适用于你，请继续阅读(或者如果你只是一个好奇想知道我对 tricky 的定义是什么的 JavaScript 书呆子，请自便)。

我刚刚整理了所有我或我的朋友在面试中可能会遇到的棘手问题。

首先，永远记住没有狡猾这回事。如果你已经掌握了基本知识，那么问的任何问题都是扭曲的英语，意在吓退你。

# **1。鹰眼测试**

这些基本上是测试你是否已经检查过任何被截取的代码中提供的每个字符的问题。例如，考虑下面的问题-

以下代码片段的输出是什么，

```
const numbers = [1, 2, 3, 4];for (var i = 0; i < numbers.length; i++);{ console.log(`The number is ${numbers[i]}`)}
```

如果你的答案是-

```
The number is 1The number is 2The number is 3The number is 4
```

很抱歉你错了，但是请仔细看看 for 循环右边的分号(`;`),现在它改变了一切，不是吗？所以这个问题的正确答案是-

```
The number is undefined
```

# **2。吊装**

我喜欢各种与提升相关的问题，人们很容易被类似于"*未定义和未在 JavaScript 中定义的区别*"或者类似于寻找输出的问题所迷惑，比如-

```
numbers();var numbers = function () { console.log(“Number one”);}numbers();function numbers() { console.log(“Number two”);}numbers();
```

猜猜上面代码片段的输出，理想情况下应该是-

```
Number twoNumber oneNumber one
```

上面案例中的第三个输出是最棘手的，如果你对提升有深入的了解，就能够解决这样的问题。

考虑另一个非常基本的代码片段-

```
console.log(a);var a;console.log(b);
```

这段代码的输出将会是-

```
undefinedUncaught ReferenceError: b is not defined
```

# **3。关闭**

一个优秀的 JavaScript 开发人员总是对闭包有深刻的了解。大多数关于终结的理论问题会是-

*   关闭的替代方案是什么？
*   关闭的利弊是什么？

以下 JavaScript 代码片段的输出会是什么

```
let counter = function() { let k = 0; return () => k++;}();console.log(counter());console.log(counter());console.log(counter());console.log(counter());
```

输出将是-

```
0123
```

考虑另一个关于闭包的问题

```
let count = 0;(function immediate() { if (count === 0) { let count = 1; console.log(count); // What is logged? } console.log(count); // What is logged?})();
```

这样的输出会是-

```
10
```

# **4。经典— *本*本**

`this`关键字对我来说一直是个谜。考虑下面的代码片段-

```
var length = 4;function callback() { console.log(this.length);}const object = { length: 5, method() { arguments[0](); }};object.method(callback, 1, 2);
```

上述代码的输出将是-

```
3
```

# **5。数组长度**

当数组长度设置为 0 时，元素的所有元素被删除？你知道吗？这对我来说确实是新闻。以下代码片段的输出是什么-

```
const fruits = [‘mango’, ‘apple’];fruits.length = 0;console.log(fruits[0]);
```

它的输出会很简单-

```
undefined
```

# **结论**

有可能你在这篇文章中读到这里，甚至没有发现一个棘手的问题，这仅仅意味着你是一个 JavaScript 呆子，你应该能够给我们一些提示，关于你对棘手的定义是什么。至于其他人，很高兴这是一些帮助。

*更多内容看*[***plain English . io***](http://plainenglish.io/)