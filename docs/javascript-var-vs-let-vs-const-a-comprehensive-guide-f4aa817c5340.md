# JavaScript Var vs . Let vs . Const——综合指南

> 原文：<https://javascript.plainenglish.io/javascript-var-vs-let-vs-const-a-comprehensive-guide-f4aa817c5340?source=collection_archive---------8----------------------->

## 了解变量声明之间的区别，避免错误

![](img/6d0a3da9f6a677c5abd8ca095ac1ef35.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`**let**`和`**const**`相比以前的`**var**`有什么不同？

在 ES6 之前，`**var**`声明是必经之路。但是由于使用`**var**`存在问题，创建变量的改变是不可避免的。

在比较`**var**`与`**let**`和`**const**`之前，我们先来讨论一下`**var**`是什么，它有什么问题。

# JavaScript 中的变量

在 JavaScript 中，可以使用`**var**`关键字声明一个变量。

例如，让我们创建一个存储值 10 的数字变量:

```
**var** num = 10;
```

## 风险值的范围

在 JavaScript 中， **scope** 指的是可以使用变量的代码区域。

用`**var**`声明的变量的范围是:

*   **全局范围**如果声明在函数之外。
*   **函数作用域**在函数内部声明时。

为了理解这些是什么意思，我们来看一堆例子。

```
**var** num1 = 10;**function** example(){
    **var** num2 = 100;
}
```

*   这里，变量`num1`具有全局范围，因为它没有被函数包围。这意味着您可以在代码的任何地方访问变量`num1`。
*   变量`num2`不是全局范围的，因为它是在函数`example()`中定义的。这意味着除了函数之外，您不能从任何地方访问它

要了解这些作用域的含义，请看这段代码:

正如您所看到的，在函数`example()`之外记录`num2`是不可能的，并且会由于函数作用域而导致错误。

## 变量的重新声明

您可以重新声明用`**var**`创建的变量。

例如，这段代码创建了一个名为`number`的变量，然后用不同的值重新声明该变量:

```
**var** number = 100;
**var** number = 25;
```

这不会导致任何错误。

在特定情况下，这种行为可能是一个问题。让我们来看看这段代码:

```
**var** num = 10;**if**(**true**){
    **var** num = 99;
    console.log(num);
}console.log(num);
```

输出:

```
99
```

如您所见，if 语句永久地改变了变量`num`。即使在声明之外。

这可能会引起混淆，因为人们可能会认为 if 语句中的变量`num`与全局变量`num`被视为不同的`num`。

这是`**var**`引起的一个问题。

## 在 JavaScript 中提升

JavaScript 中的提升意味着在代码运行之前，变量和函数声明被移动到作用域的顶部。发生这种情况是因为 JavaScript 希望提前看到将要执行的代码，并为变量和函数预留空间。

提升使得在定义变量之前调用它成为可能。

例如:

```
console.log(greet);
**var** greet = "Hello"
```

结果是:

```
undefined
```

发生这种情况是因为吊装。实际上，上面这段代码是这样工作的:

```
**var** greet;console.log(greet);
greet = "Hello";
```

概括一下，使用`**var**`创建的所有变量都被提升到作用域的顶部，并被赋予一个值`**undefined**`。

吊装引入了另一个问题。让我们看一个例子:

结果:

```
Your name is James
```

这是令人困惑的。代码声明，如果没有定义`name`，它将创建一个变量`name`，并将`“James”`赋给它并返回。但是在上面的例子中，名字已经是`“Charlie”`开头了。因此，if-check 应该永远不会通过，函数`getName()`应该返回`“Charlie”`。

但这不是真的。由于吊装的原因，`name`与`**undefined**`在一条线上。这意味着条件`!name`实际上是`true`。

为了理解`name`为什么是`**undefined**`，我们先来看看上面的函数在引擎盖下由于吊装是什么样子的。注意变量`name`在`getName()`函数中的表现:

如您所知，提升会将所有声明移动到作用域的顶部。在`getName()`函数中，这意味着变量`name`在 if-check 之前被重新声明，并被赋值为`**undefined**`。这就是 if-check 通过并返回名称`“James”`的原因。

这真的很令人困惑，尤其是对于不知道起重的初学者。

让我们看看如何解决与使用`**var**`相关的问题。

# 让 JavaScript 进来

如今，在 JavaScript 中声明变量的首选方式是使用`**let**`。这是因为它与使用`**var**`相比有所改进。

## Let 有一个块范围

`**let**`变量有一个**块范围**。这意味着它只能在定义它的花括号中访问。

例如，访问块外的`**let**`变量会导致错误:

```
**if**(**true**){
    **let** num = 1;
}console.log(num);
```

输出:

```
**error: Uncaught ReferenceError: num is not defined**
```

`num`只能在 if 语句中访问。不能在外部访问它。

块作用域使您可以在不同的作用域中拥有两个同名的变量。

例如:

```
**let** num = 1;**if**(**true**){
    **let** num = 20;
    console.log(num);
}
```

输出:

```
20
```

现在，不是重新声明`num`，而是两个`num`变量在它们自己的范围内被视为不同的变量。

这使得`let`比`var`更好的选择:在使用`let`时，你不必担心之前是否使用过变量的名称。

## 重新声明一个字母是不可能

与`**var**`相反，`**let**`变量不能在其作用域内重新声明。

例如，这会导致一个错误:

```
**let** number = 100;
**let** number = 25;
```

输出:

```
**Identifier 'number' has already been declared.**
```

但是当然，您可以用这种方式将**的值更新为`**let**`的值:**

```
**let** num = 100;
num = 25;
```

## 左起重

每个声明都在 JavaScript 中被挂起。这也适用于`**let**`变量。吊装`**let**`与吊装`**var**`的区别在于:

*   一个`**var**`变量被提升，使得一个值`**undefined**`被分配给它
*   一个`**let**`变量根本没有用值初始化。

这意味着在定义变量之前，不能访问用`**let**`创建的变量:

```
console.log(greet);
**let** greet = "Hello"
```

输出:

```
**error: Uncaught ReferenceError: Cannot access 'greet' before initialization**
```

让我们回到你之前看到的`**var**`吊装的问题:

您可能还记得，在输出中没有看到`"Charlie”`，而是:

```
Your name is James
```

现在你已经了解了什么是`**let**`以及它如何使变量声明更加一致。你能猜到如何解决上述问题吗？

你可以用`**let**`代替`**var**`问题就没了。

让我们验证一下事实是否如此:

输出:

```
Your name is Charlie
```

现在 if-check 永远不会通过，因为由于`**let**`的提升，在 if 语句之前没有给它一个值`**undefined**`。相反，如您所料，JavaScript 使用在函数外部定义的`name` `“Charlie”`。

# JavaScript 中的常量

声明为`**const**`的变量在 JavaScript 中保持一个常量值。

const 和`**let**`唯一真正的区别是`**const**`是不可变的。这意味着一旦定义，你永远不能改变它的值。

```
**const** num = 1;
num = 20;
```

输出:

```
**error: Uncaught TypeError: Assignment to constant variable.**
```

有了这个约束，`**const**`必须在声明时初始化。

除了不可变之外，`**const**`的行为类似于`**let**`。为了使它完整，让我们看看这意味着什么。

## Const 有一个块范围

与`**let**`类似，`**const**`有 block 作用域。这意味着`**const**`变量只能在定义它的花括号中被访问。

例如:

```
**if**(**true**){
    **const** num = 10;
    console.log(num); // works
}console.log(num); // fails
```

此外，在不同的作用域中可以有许多同名的`**const**`变量，因为它们被视为不同的变量。

```
**const** num = 1;**if**(**true**){
    **const** num = 20;
    console.log(num);
}
```

输出:

```
20
```

## 建筑吊装

提升`**const**`和`**let**`的工作方式相同。它们没有预先用`**undefined**`的值初始化，相反，它们根本没有初始化。这使得在初始化它们之前无法调用它们。

例如:

```
console.log(greet);
**const** greet = "Hello"
```

输出:

```
**error: Uncaught ReferenceError: Cannot access 'greet' before initialization**
```

# 结论

在 JavaScript 中创建变量的老派方法是使用`**var**`。从 ES6 开始，使用`**let**`和`**const**`创建变量有了更一致的方法。

`**var**`和`**let**` / `**const**`的区别在于:

*   `**var**`声明是全局作用域或函数作用域，而`**let**`和`**const**`是块作用域。使用`**let**`或`**const**`你可以在它们自己的作用域中有多个同名的变量。
*   `**var**`变量可以更新，**在范围内重新声明**。`**let**`变量可以更新，但不能重新声明；`**const**`变量既不能更新也不能重新声明。
*   在 JavaScript 中，所有声明都被提升到作用域的顶部。但是当`**var**`变量用`**undefined**`初始化时，`**let**`和`**const**`变量不用任何值初始化。这在某些情况下避免了混淆。

# 进一步阅读

[](https://www.codingem.com/50-buzzwords-of-web-development-and-design-in-2021/) [## 2021 年网络开发和设计的 50 多个流行语

### 学习创业公司使用的网页开发和网页设计语言。这篇文章是关于…的很好的入门读物

www.codingem.com](https://www.codingem.com/50-buzzwords-of-web-development-and-design-in-2021/) 

# 参考

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript) [## JavaScript | MDN

### JavaScript (JS)是一种轻量级、解释型或即时编译的编程语言，具有一流的…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)