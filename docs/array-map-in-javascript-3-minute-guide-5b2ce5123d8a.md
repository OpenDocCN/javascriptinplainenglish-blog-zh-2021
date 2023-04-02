# 数组。JavaScript 中的 map():3 分钟指南#01

> 原文：<https://javascript.plainenglish.io/array-map-in-javascript-3-minute-guide-5b2ce5123d8a?source=collection_archive---------16----------------------->

## 踏入函数式编程和不变性的大门

![](img/3eeff45e3c85b8a0bc0afc676a23076c.png)

Illustration made by [Author](http://www.arnoldcode.com) with ❤️

当我在早年编程时第一次遇到这个小函数时。我不知道函数式编程和不可变对象。我之前的学习思考了我的想法，找到抽象成代码的现实世界问题的解决方案更重要。

让代码工作是我的总体想法！如果我有这么短的 3 分钟指南，我肯定不会有任何借口不读它，并且提高得更快！

## 数组的定义。地图()

数组。Map()用于通过对传递的数组的每个元素调用函数来创建一个新的数组。

只需快速浏览一下下面来自 developer.Mozilla.org 的官方定义，因为每当我想学习新的东西时，我总是被这些抽象的展示方式弄糊涂。

```
var new_array = arr.map(function callback(currentValue[, index[, array]]) {
    // returned element for new_array
}[, thisArg])
```

我相信值得记住的显著例子可以让任何大脑进入开放的思维状态。因此，我们走吧！

# 魔术师和治疗药剂

想象一下，我们的 RPG 角色有一个存货清单，由一个简单的数组表示，(`potions`)装满了生命药剂，在我们的旅程中，我们遇到了一个名叫 **Gandolon** 的魔术师，他让我们施展一个咒语，将每一种生命药剂转换成魔法药剂。然后这个魔术师会使用`Array.prototype.map()`。

在迭代过程中，`potion`可以被解释为数组的当前条目，在`=>`之后的任何条目都将被返回。这就是 lambda 表达式的工作方式。

假设我们创建了一个新的数组`potions`，并在调用`MagicSpell()`后将其打印出来。原始数组保持不变。这样做是函数式编程的一部分，保持原始变量不变而不是改变它们的状态是编码不可变的一部分。

老式的方法是命令式的，这意味着使用语句来改变状态。我们迭代旧数组`potions`，并将条目推入新数组`magicPotions`。我们改变了`magicPotions`的状态。

你能发现这样做带来的开销吗？

这也是以函数的方式来做，但不处理不可变的对象。我们创建一个新的数组并返回它，而不是直接改变`potions`。因为`potions`只是一个`let`而不是`const`，我们可以改变它的状态。使用`const`变量或多或少会迫使你学习函数式编程。

[](https://medium.com/front-end-weekly/i-bet-your-javascript-const-isnt-const-at-all-c1e476716cfe) [## 我打赌你的 JavaScript const 根本不是 const！

### 真正谈论如何使你的对象不可变！

medium.com](https://medium.com/front-end-weekly/i-bet-your-javascript-const-isnt-const-at-all-c1e476716cfe) 

# 最好不要使用数组。地图()

不要用`Array.prototype.map()`去做的事情就是遍历数组。您应该始终使用新创建的数组！前车之鉴。

这里，更好的选择是使用`Array.forEach()`而不是`Array.map()`，因为`forEach()`不返回值。

# 外卖食品

*   `Array.prototype.map()`是声明性的，这意味着它使用函数来描述状态
*   老式的方法是强制性的，这意味着它使用语句来改变状态
*   当你不想使用返回的数组时，千万不要用`Array.prototype.map()`遍历一个数组。
*   [***节省自己大量的时间，专注于重要的主题。***](https://arnoldcodeacademy.ck.page/26-web-dev-cheat-sheets)

![](img/227a060a3bfa55f41fa795d5990e6032.png)

Arnold Code Academy 26 Web Developer Cheatsheets

# 参考

Mozilla.org—Array . prototype . map()—[https://developer . Mozilla . org/de/docs/Web/JavaScript/Reference/Global _ Objects/Array/map](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array/map)