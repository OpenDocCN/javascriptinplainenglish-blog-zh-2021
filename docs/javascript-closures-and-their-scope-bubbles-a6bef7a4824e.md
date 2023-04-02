# JavaScript 闭包及其范围气泡

> 原文：<https://javascript.plainenglish.io/javascript-closures-and-their-scope-bubbles-a6bef7a4824e?source=collection_archive---------20----------------------->

## JavaScript 闭包的初学者友好指南。

![](img/d6b02d4addbca31b41c8f2e27e60243d.png)

Photo by [Marc Sendra Martorell](https://unsplash.com/@marcsm?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/bubbles?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当我第一次开始深入学习 JavaScript 时，闭包的概念对我来说是比较难的概念之一。虽然我读了很多关于它的东西，但直到我开始在工作中使用它，我才真正理解它。

如果您是闭包的新手，让我们从这里开始:闭包本质上是一个对象，它具有一个或多个与对象周围环境捆绑在一起的函数。环境通常包括闭包需要的变量，这些变量不能在程序的主范围内直接访问。

在本文中，我们将看一个简单的闭包，然后看看它是如何使用的。

# 一个例子

一个闭包通常驻留在一个更大的函数中，这个更大的函数中的环境充当闭包的环境“气泡”换句话说，闭包的[范围](https://www.w3schools.com/js/js_scope.asp)是由这个更大的函数划分的。

下面是一个函数及其周围范围气泡的例子。

An example of a simple closure

因为这四个函数是附加在一个对象上的，所以我们也可以称之为*方法。*当我们在代码中找到这些方法之一时—

```
let num = counter.get();
```

—我们访问函数*加上*它的周围环境，这就是闭包。所以你可以说上面的代码片段提供了四种不同的闭包。

让我们看一下代码片段中的几个关键行。

在第 1 行，`counter`变量被设置为等于一个立即调用的函数表达式(life)——我们所说的“气泡”。由于第 20 行末尾的括号，当程序开始时，生命就开始了。

```
let counter = (function() { // code hidden for clarity})(); // <-- the parenthesis make the function start immediately
```

这个生命返回一个具有四种功能的对象:

*   `get`，它简单地获取`count`值。
*   `set`，它将`count`值设置为我们想要的任何值。
*   `increment,`它将现有值增加作为参数传入的数量。如果没有传入任何值，它会将该值递增 1。
*   `reset`方法将`count`值重置为零。

由于这些方法都需要那个`count`变量，JavaScript 引擎足够聪明，能够意识到`count`变量的重要性——所以引擎的垃圾收集器不会删除它。

这些方法是用户访问`count`值的唯一方式。这样，闭包的使用使得`count`值的行为类似于 Java 等更传统的面向对象语言中的私有变量。私有变量不能在它们所在的对象之外直接访问，因此需要方法来检索或更新它们的值。这使得它们更难被无意中弄乱。

# 演示

在下面的演示中，您将看到实际操作中的封口。所有四个都被使用，结果打印出三个值。

# 调用闭包的方法

下面是调用闭包的每个方法的`init`函数。看看它是如何工作的，看看您是否能理解是什么决定了要打印的三个值。

让我们回顾一下发生了什么。首先，我们首先获取要打印的 HTML 元素的引用。

```
let span1 = document.querySelector('#test1 span');
let span2 = document.querySelector('#test2 span');
let span3 = document.querySelector('#test3 span');
```

然后我们使用`counter`对象将`count`的值`set`转换为`10`。

```
counter.set(10);
```

然后我们`get`值`count`，将其存储在`val1`中，并将`10`的结果值打印到第一个`<span>`元素。

```
let val1 = counter.get();span1.textContent = val1;
```

接下来，我们通过`2`得到`increment`的`count`值。我们再次`get`修改后的值，现在是`12`，并打印出来。

```
counter.increment(2);
let val2 = counter.get();
span2.textContent = val2;
```

然后我们将值`reset`给`0`并不带参数调用`increment`，因此值增加了`1`。

```
counter.reset();
counter.increment();
```

在这之后，我们最后一次`get`这个值，现在是`1,`并打印它。

```
let val3 = counter.get();
span3.textContent = val3;
```

如果你试图在生活之外直接调用`count`，你将一事无成——你必须使用这些方法来检索和更新`count`。

# 外卖食品

由于能够理解它们，我发现闭包非常有用，尤其是当我有多个相关变量，而我不想污染全局名称空间的时候。当编写复杂的程序时，您可以构建多个函数表达式，每个表达式都作为自己的作用域气泡，具有自己不同的目的、方法和私有变量。这种用内置闭包创建立即调用函数表达式的方式也被称为[模块设计模式](/data-hiding-with-javascript-module-pattern-62b71520bddd)。

# 后续步骤

如果您有兴趣学习更多关于 JavaScript 中闭包的知识，请尝试以下方法:

*   下次你写程序的时候，试着用上面的风格创建一个带有闭包的表达式来代替其他的解决方案，比如全局变量。
*   探索现有的方法，比如`setTimeout`，如何使用闭包。
*   将闭包与 JavaScript 类进行比较，评估哪一个更适合特定的用例。
*   如果你申请的是一个开发人员的职位，寻找那些关注闭包的面试问题，并练习回答它们。

我希望这篇快速的帖子能让你对闭包有一个坚实的概念。感谢阅读！

# 在别处

下面是另外两篇关于 JavaScript 的文章，可能对你有所帮助。

[](/how-to-create-a-timestamp-from-a-date-object-in-javascript-760d58a3511f) [## 如何用 JavaScript 创建时间戳

### 让我们解包一个日期对象并提取我们需要的信息。

javascript.plainenglish.io](/how-to-create-a-timestamp-from-a-date-object-in-javascript-760d58a3511f) [](/from-camel-case-to-dash-syntax-in-javascript-c685206ee682) [## JavaScript 中从骆驼大小写到破折号的语法

### 仔细看看一个概念丰富的代码片段。

javascript.plainenglish.io](/from-camel-case-to-dash-syntax-in-javascript-c685206ee682) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)