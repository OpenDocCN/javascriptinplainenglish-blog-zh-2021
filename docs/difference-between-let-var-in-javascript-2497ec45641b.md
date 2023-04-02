# JavaScript 中字母和变量的区别

> 原文：<https://javascript.plainenglish.io/difference-between-let-var-in-javascript-2497ec45641b?source=collection_archive---------3----------------------->

## 让我们了解一下为什么在 JavaScript 中有两种声明变量的方式，提升和闭包概念。

![](img/1cea62a3572e5b9ee87e666a399348b4.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 ECMAScript6 (2015)之前，JavaScript 只有全局作用域和函数作用域。现在我们又有了一个:块范围。ES6 引入了两个重要的新 JavaScript 关键字: **let** 和 **const** 。

我们所说的范围是什么意思？

范围决定了变量可见或可访问的区域。

我们可以谈论两个不同的范围，即**全局**和**局部**。其中，局部有两个子类型，即**功能**和**块**。

为了更好地理解什么是作用域，我们可以看下面的例子:

```
const message = 'Hello';console.log(message);     // 'Hello'
```

好了，正如所料，我们将消息常量打印为“Hello”。让我们看看当我们把声明移到 if 语句中时会发生什么:

```
if (true) {const message = 'Hello';}console.log(message); // Uncaught ReferenceError: message is not defined"
```

我们无法打印，因为我们试图在我们定义的范围之外打印。它是不可访问的。

作用域是一条规则，规定你不能访问这个区域之外的变量。

当一个变量*是全局作用域*时，这意味着它在你程序的任何地方都是可用的。全局范围是最外层的范围。它可以从任何内部(又名*局部*)作用域访问。

让我们深入本地范围。

**封锁范围:**

我们所说的块是由花括号分隔的代码片段。

```
{StatementList}
```

如果需要，可以标记块。

```
LabelIdentifier: {StatementList}
```

我们在上面给出了块范围的第一个例子。当我们试图在 if 语句中声明 constant 时，我们遇到了块范围的变量。

**功能范围:**

顾名思义，它被认为是可以在函数中访问的。

```
function ring() {// "ring" function scopevar message = '**One Ring to rule them all, One Ring to find them,** **One Ring to bring them all and in the darkness bind them**.';console.log(message); // '**One Ring to rule them all, One Ring to find them,** **One Ring to bring them all and in the darkness bind them**.'} ring();console.log(message); // Uncaught ReferenceError: message is not defined"
```

就是这样！因为它是函数范围的。同样，我们不能打印消息变量

关于作用域的一个关键点是*内部作用域*可以访问其*外部作用域*的变量。

```
function ring() {// "ring" function scopeconst message = '**One Ring to rule them all, One Ring to find them,** **One Ring to bring them all and in the darkness bind them**.';if (true) {// "if" code block scopeconst carrier = 'Frodo';console.log(message); // '**One Ring to rule them all, One Ring to find them,** **One Ring to bring them all and in the darkness bind them**.' }console.log(carrier); // throws ReferenceError} ring();
```

我们可以在内部作用域(if 语句)打印*消息*变量，但是我们不能在外部作用域打印*载体*变量。

我假设您已经了解了什么是作用域，现在是时候看看两个变量声明之间的区别了。

## let 和 var 的差异:

**var** 是声明变量的老办法，也是最弱的关键字。为什么？因为:

*   **变量**是函数作用域
*   **设**是块范围的
*   **var** 可以更新，也可以重新申报
*   **让**可以更新但不能重新声明

在一个例子中检查关于**变量**的问题:

```
var offer = "The story ends";var pill = blue;

if (pill == red ) {
 var offer = "Stay In Wonderland"; 
}

console.log(offer); // "Stay In Wonderland"
```

因此，我们在全球范围内接受了蓝色药丸，但当我们打印报价时，我们不得不呆在仙境中:(

这是因为**变量**不是块范围的。我们可以在 if 语句中访问 *offer* 变量。并且它改变分配给*报价*的字符串值。

由于作用域的不同，我们也从具有闭包的循环中获得不同的值，如下所示:

```
// Logs 3 thrice, not what we meant.
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}// Logs 0, 1 and 2, as expected.
for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j), 0);
}
```

如果对你来说这还不够，还有一个问题:

**我们可以更新两种变量类型，而不会出现错误:**

用**让**

```
**let offer = "The story ends";
offer = "Stay in Wonderland";**
```

用 **var**

```
**var offer = "The story ends";
offer = "Stay in Wonderland";**
```

**但是当我们试图重新声明它们的时候:**

用**让**

```
let offer = "**The story ends**";
let offer = "**Stay in Wonderland**"; // Uncaught SyntaxError: Identifier 'offer' has already been declared"
```

用 **var**

```
var offer = "**The story ends**";
var offer = "**Stay in Wonderland**";
```

我们不想无意中声明一个变量两次，对吗？

使用 **let** 减少了处理大量变量时可能发生的潜在命名冲突。当你想让一个全局变量显式地出现在窗口对象上时，可以使用**变量**(如果有必要，一定要仔细考虑)。

# 提升

在编译阶段，就在代码执行前的几微秒内，它会被扫描函数和变量声明。所有这些函数和变量声明都被添加到名为**词法环境**的 JavaScript 数据结构的内存中。以便在源代码中声明它们之前就可以使用它们。

有了这个概念的帮助，我们可以在我们定义它们的线之上使用函数:

```
mithrandir();  // "A wizard is never late"
mithrandir(){
  console.log('A wizard is never late');
}
```

所有的变量都被提升了。然而，虽然**变量**声明用*未定义*初始化，但是**让**和**常量**声明保持*未初始化。*

让我们看一个例子:

用 **var**

```
console.log(password); // undefined
var password = 'Speak, friend, and enter.';
```

用**让**

```
console.log(password); // undefined
let password = 'Speak, friend, and enter.'; // Uncaught ReferenceError: Cannot access 'password' before initialization"
```

# **关闭**

有一个访问内部作用域的提示，那就是使用闭包！

*闭包*是一个访问其内部作用域的函数，即使在其词法作用域之外执行。

通过一个基本示例学习闭包概念:

```
function ring() { let carrier = 'Frodo'; function gollum() { console.log(carrier); // "Frodo" } gollum();} ring(); 
```

我们有一个名为*载体*的变量,“Frodo”被分配给这个变量。正如所料，它甚至可以从内部函数*咕鲁*中访问:)

当执行函数 ring()时，它正在执行 gollum()函数，我们可以在 ring()函数范围之外访问*载体*变量。

咕鲁是这里的终结。

这个题目到此为止。感谢您的阅读。

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*