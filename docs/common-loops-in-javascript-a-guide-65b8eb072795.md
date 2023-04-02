# JavaScript 中的常见循环:指南

> 原文：<https://javascript.plainenglish.io/common-loops-in-javascript-a-guide-65b8eb072795?source=collection_archive---------11----------------------->

## 让我们总结一下在 do…while，while 和 for 之间应该使用哪一个。

![](img/c91e58d75c839aa6cd9033b68843274c.png)

Image By [Henry & Co](https://www.pexels.com/@hngstrm?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

循环是我最喜欢的编程概念之一，这是我作为初学者学到的。这是避免代码重复的简单而有效的方法。如果你正在努力理解我们在 JavaScript 中看到的各种循环，那么这篇文章的确是为你准备的。😉

此外，我尽量保持它的通用性，以便任何人即使不懂 JavaScript 也能理解。所以，让我们直接开始吧！

# 循环有什么必要？

循环帮助我们避免代码重复。换句话说，它们允许我们将同一组指令执行指定的次数。通常，我们必须处理大量的数据，为此我们必须一次又一次地执行相同的任务。这项工作之所以会出现循环，是因为我们可以避免用我们懒惰的手一遍又一遍地输入相同的语句🥱.但是 JavaScript 中有很多种循环；你怎么知道在什么情况下使用哪一个？**我将在这篇文章中讨论三个常见的循环:do…while，while 和 for。**那么，让我们看看这些是什么，以及何时使用它们。

# 不同种类的循环

# 做…的同时

我选择先讨论这个循环，因为它看起来更接近我希望你们开始思考循环的方式。它的[语法](https://en.wikipedia.org/wiki/Syntax_(programming_languages))很简单，很容易理解

```
do {
  ...
} while (...)
```

要执行的指令放在关键字`do`后面的花括号`{}`中，而括号`()`包含每次重复这些指令之前要检查的条件。除非我们在和一个人说话，我们不能只说`"Print 'hello' 5 times"`。循环的工作方式是在每次重复任务之前检查一些条件。如果条件评估为`true`，则再次执行任务；否则，它退出循环。考虑这个将`Hello!`打印 5 次到控制台/终端的例子:

```
let index = 1;do {
  console.log('Hello!');
  index = index + 1;
} while(index <= 5)
```

注意上面代码片段中`index`变量的使用。首先，我们声明这个变量，并将整数值`1`赋给它。然后我们告诉计算机运行`do{}`块中的语句；然后评估条件`index <= 5`；如果为真，则再次运行这些语句，否则退出循环。

如果我们忘记在代码中包含第 5 行，循环将变得无限，因为`index`的值总是 1；因此，该条件将永远为真。因此，每次循环运行时都需要增加该值。当`index`的值等于 5 时，条件将变为假；因此，它将退出循环。

> *[*增量运算符*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Increment) *) (++)是一个速记运算符，允许我们将* `*index++*` *写成* `*index = index + 1*` *。另外还有一个* [*减量运算符*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Decrement) *( -)作为其对应物。找找看！👍**

# *在…期间*

*`while`回路与`do...while`完全相同。看看这两个循环的语法-*

```
*// do...while loop
do {
  ...
} while (...)// while loop
while (...) {
  ...
}*
```

*你能看出区别吗？`do...while`循环首先运行语句，然后检查条件；而`while`循环首先检查条件，然后运行语句。简而言之，前者检查下一次迭代的条件，而后者检查当前迭代的条件。*

*“我们应该使用这些循环中的哪一个”这个问题的答案相当固执己见。我个人不记得我使用`do...while` loop 的时间，除了在我学习的时候。在这种情况下，循环经常被使用。但是还有一种类型的循环是所有其他循环中最常见的——`for`循环。*

*在介绍`for`循环之前，我想让你了解一下编程中[作用域](https://developer.mozilla.org/en-US/docs/Glossary/Scope)的概念。**变量的作用域可以定义为可以访问该变量的语句范围。**以下面的片段为例-*

```
*1\. let name = 'Sapinder';
2\. 
3\. {
4\.   let name = 'Singh';
5\.   console.log(name);
6\. }
7\. 
8\. console.log(name);*
```

*您认为第 5 行和第 8 行将打印到控制台上吗？第一个`console.log`语句将打印`Singh`，但是第二个语句将打印`Sapinder`，因为保存值`Singh`的变量的范围被限制在内部块中。它不能在花括号外访问。因此，当编译器到达第 8 行时，它只知道保存值`Sapinder`的变量`name`。另外，请注意，我使用了`let`关键字而不是`var`，因为用`var`声明的变量总是*全局作用域的*，不管它在哪里声明。现在你知道了什么是作用域，让我们学习一下`for`循环。*

# *为*

*我喜欢把`for`循环看作是`while`循环的一个更简洁的版本。这两者几乎是一样的，除了一些我们稍后会看到的东西。首先，来看一个`for`循环的例子:*

```
*for(let index = 1; index <= 5; index++) {
  console.log('Hello!');
}*
```

*是啊！与下面的`while`循环相同:*

```
*let index = 1;while (index <= 5) {
  console.log('Hello!');
  index++;
}*
```

*变量的**初始化**、**条件**和**值的升级**，所有这些事情都可以在`for`循环中的一行代码中实现。此外，变量`index`被初始化为*块范围的*，不像在`while`循环的例子中。这是使用`for`循环的主要好处，因为它避免了任何全局级别的名称冲突。为了理解这两个循环之间的另一个区别，我想引入两个关键词-*

*   ***中断** —关键字`break`用于终止/退出循环。一遇到这个关键字，编译器就会终止循环。*
*   ***继续** —关键字`continue`用于跳过当前迭代中剩余的语句，并开始循环中的下一次迭代。*

*现在，考虑下面的例子，我想打印从 1 到 5 的数字，不包括数字 3:*

```
*for(let index = 1; index <= 5; index++) {
  if(index === 3) {
    continue;
  }
  console.log(index);
}*
```

*在这里，我说，“如果 index 等于 3，不要运行其余的语句；然后直接跳到下一个迭代。”因此，它不会将数字`3`打印到控制台。它将*继续*具有升级值`index`的循环，即`4`。现在，让我们使用`while`循环来实现相同的方法:*

```
*let index = 1;while(index <= 5) {
  if(index === 3) {
    continue;
  }
  console.log(index); index++; // upgrading needs to be done here in the end, unlike in `for` loop
}*
```

*你认为这个解决办法行得通吗？你能发现这个漏洞吗？这是一个*无限循环*，因为一旦`index`的值达到`3`，它将跳过包括`index++`在内的其余语句。因此，它的值永远不会升级到超过`3`；并且循环无限地继续运行。*

*使用`for`循环可以很容易地处理这种情况，因为循环的升级表达式是在最开始指定的；并且总是在每次迭代结束时执行。但是，如果我们将这个升级表达式从循环的第一行移到循环结束之前，如下面的例子所示，我们将再次遇到无限循环问题。*

```
*for(let index = 1; index <=5;) {
  if(index === 3) {
    continue;
  }
  console.log(index);
  /* This will cause the same issue of infinite loop */
  index++;
}*
```

*因此，总结一下，我认为`for`和`while`循环可以互换使用，除了一些情况，与另一个循环相比，我们使用`while`循环更容易导致错误。JavaScript 中也有其他类型的循环，比如- `for in`、`for of`等。，但是它们实际上比上面讨论的要简单得多，不需要包含在本文中。*

*结束这一切，如果你喜欢我的写作风格，你可以关注我，永远不会错过我未来的任何帖子。你也可以在 [Twitter](https://twitter.com/sapinder_dev) 、 [Github](https://github.com/sapinder-pal) 和 [LinkedIn](https://linkedin.com/in/sapinder-singh) 上查看我。*

*和平！🤞*

**更多内容请看*[***plain English . io***](http://plainenglish.io/)*