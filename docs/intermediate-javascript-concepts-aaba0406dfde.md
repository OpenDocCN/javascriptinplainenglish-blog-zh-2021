# 中级 JavaScript 概念

> 原文：<https://javascript.plainenglish.io/intermediate-javascript-concepts-aaba0406dfde?source=collection_archive---------9----------------------->

## 功能、提升、范围和关闭

## 你每天都看到它们，但你知道它们是什么吗？

# 1.功能

JavaScript 中的函数是一组接受一些输入、执行特定任务并返回一些输出的语句。

当使用函数时，你首先必须**定义**函数，包括命名它并说明它做什么动作。然后，它实际上让那些动作发生，你必须**调用**这个函数。

定义函数主要有两种方式:**函数声明**和**函数表达式**。(注意:还有一种叫做[函数构造器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/Function)的东西，尽管它不太常用。)

![](img/fb6ddbb2dfd8911aa4802f5125c1204f.png)

Photo by [Neal E. Johnson](https://unsplash.com/@neal_johnson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 函数声明

函数声明，也称为函数定义或函数语句，是定义函数的一种方式。它的结构如下:

```
function name(input) {
  statements;
}
```

函数的名字是`name`。`input`是函数的*参数*，它被括在括号中。在花括号里面的是`statements`，它完成一个特定的任务。`statements`经常返回值，或者一个*输出*。一个函数不需要接受任何参数，所以`input`是可选的。`statements`本身也是可选的(尽管这意味着你会有一个空函数，不做任何事情)。

例如，假设我们想要使用一个函数声明来定义一个函数，该函数声明接受一个数字，并返回给定的数字乘以 2:

```
function double(number) {
  return number * 2;
}
```

在本例中，`number`仅通过**值**传递给函数；换句话说，这个函数不会在更大的全局上下文中改变`number`。为了说明这意味着什么，让我们在上述函数的前后插入几个控制台日志:

```
// declaring a variable called `count` and setting it equal to 3
let count = 3;
console.log(count); // 3// declaring a function called `double` which returns an inputted number times 2
function double(number) {
  return number * 2;
}// declaring a variable called `result` is set equal to calling the function `double` and passing the number `count` as the input
let result = double(count);
console.log(result); // 6console.log(count); // 3
```

当我们调用函数`double()`并传入`count`时，我们并没有改变`count`本身的值——它仍然等于`3`。

然而，这只适用于 JavaScript 中的*原语参数*。如果您将一个*非原始参数*传递给一个函数(比如一个数组或对象)，并且该函数以某种方式改变了该对象，那么该对象也会在函数之外被改变。例如:

```
let fruits = ["apple", "banana", "orange"];function removeLastElement(array) {
  array.pop();
  return array;
}removeLastElement(fruits);console.log(fruits); // ["apple", "banana"]
```

上面的例子使用了`[.pop()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)` [方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)，它移除了数组的最后一个元素。通过将`fruits`对象作为参数传入`removeLastElement()`，移除了`fruits`的最后一个元素，并返回了更新后的数组。当处理非原始值时，记住将它们传递给函数可能会改变它们的值，这一点很重要。

## 函数表达式和箭头函数

定义函数的另一种方法是使用函数表达式。函数表达式和函数声明的主要区别在于，对于函数表达式，函数名是可选的。如果不包含函数名，就有一个**匿名函数**。函数表达式的结构如下:

```
function name(input) {
    statements;
}
```

请注意，这与函数声明的结构完全相同。下面是一个匿名函数的例子，意思是它没有名字。该函数被设置为等于一个名为`triple`的变量:

```
const triple = function (number) {
  return number * 3;
};
```

函数表达式经常被写成**箭头函数**。箭头函数被认为是函数表达式的精简版本，通常用于“清理”代码。让我们把上面的函数变成一个箭头函数:

```
// Standard function expression
function (number) {
  return number * 3;
};// Arrow function
number => number * 3;
```

箭头函数改变了什么？单词`function`和`return`被删除，参数`number`周围没有括号，花括号被一个箭头`=>`代替，所有内容都在一行上。

但是，这些规则会因箭头功能的不同而有所不同。如果函数只有一个参数，那么就不要用括号把它括起来。如果它有**零个或 2+** 个参数，那么就用括号把它括起来。如果函数只有**一个语句**，那么你就没有花括号或者单词`return`。如果函数有**多个语句**，那么你就有**两个**括号和一个`return`单词。让我们来看一个例子:

```
// One parameter, one statement
number => number * 3; // AB// Zero parameters, one statement (these are often used in callback functions)
() => x * 2;// Two parameters, one statement
(a, b) => a - b;// Two parameters, multiple statements:
(a, b) => {
  let tax = 0.05;
  return (a + b) * tax;
};
```

根据函数的不同，箭头函数有很多变化的语法。然而，记住什么时候在输入中使用括号并不重要，重要的是要知道箭头函数通常是什么样子，以及在哪里可以找到关于它的更多资源。随着时间的推移和实践，您将不再需要查阅文档。编程的许多方面都是如此:与其试图记住如何编写和使用它的具体方法的每一个小细节，不如认识到一些东西并知道去哪里获取更多信息。每个程序员都使用谷歌并查阅文档，不管他们已经做了多久。

## 调用函数

仅仅因为你定义了一个函数，并不意味着这个函数已经被执行了。当你定义一个函数时，你说它叫什么，它应该做什么。当你调用一个函数时，它实际上被执行了。

要调用一个函数，需要引用函数名，并传递与参数对应的参数。要调用上面定义的函数`triple()`，我们需要引用它的名字，并传入一个数字作为参数:

```
triple(5);
```

# 2.提升

**JavaScript 中的提升**意味着变量声明和函数声明被带到代码的顶部。

这是一个很难理解的概念，所以看一个例子会有所帮助。让我们使用函数声明创建一个函数，并将其命名为`numberSquared`。`numberSquared()`将接受一个输入的数字，然后控制台记录该值的平方。然后，在函数之后，我们可以调用它，我们会传入数字`5`。

```
function numberSquared(num) {
  console.log(num * num);
}numberSquared(5);
```

上面代码的结果是`25`。

现在，如果我们在声明函数之前调用函数*，会发生什么？*

```
numberSquared(5);function numberSquared(num) {
  console.log(num * num);
}
```

同样，上面代码的结果是`25`。这是因为在编译代码时，函数声明被放在了最前面。

请记住，只提升函数声明，而不提升函数表达式。

# 3.范围和结束

JavaScript 中的**范围**是当前“可见”或“可访问”的内容。根据 [MDN 文档](https://developer.mozilla.org/en-US/docs/Glossary/Scope)，“如果一个变量或其他表达式不在‘当前作用域’内，那么它就不可用。”

就函数而言，函数中声明的变量只能在函数中访问。这被称为**关闭**。

要查看不同作用域的示例，让我们看看以下内容:

```
const weather = "rainy";function myNameAndTheWeather() {
  const name = "Alisa"; console.log(name);
  console.log(weather);
}myNameAndTheWeather();console.log(weather);
console.log(name);
```

如果我们运行这个程序会发生什么？输出如下所示:

```
Alisa
rainy
rainy
[ReferenceError: name is not defined]
```

为了理解为什么会有这些结果，让我们回顾一下代码说了什么，以及当我们运行它时会发生什么。首先，变量`weather`被初始化并被设置为等于`"rainy"`。然后，使用函数声明，定义了函数`myNameAndTheWeather()`。在`myNameAndTheWeather()`内部，变量`name`被初始化并设置为等于`"Alisa"`，`name`被控制台记录，`weather`被控制台记录。然后，在函数之外，调用`myNameAndTheWeather()`。然后，`weather`被控制台记录。最后，`name`被控制台记录。

当我们运行这个程序时，首先发生的是函数`myNameAndTheWeather()`被调用。`name`是在函数中定义的，在**局部作用域**中，所以函数能够控制台记录它。`weather`是在函数之外定义的，在**全局作用域**中，所以函数也可以访问它。换句话说，函数可以访问在它自己的局部作用域(一个闭包)和全局作用域中声明的变量。因此，`Alisa`和`rainy`被记录到控制台。

执行`myNameAndTheWeather()`后，程序转到下一行，该行表示将`weather`记录到控制台。`weather`是一个可访问的变量，因此程序控制台记录其值。最后，程序尝试控制台记录变量`name`。然而，`name`是在函数`myNameAndTheWeather()`中定义*的。它有一个局部作用域，这意味着我们不能从函数外部访问它。因此，会返回一个引用错误。*

如果您对 JavaScript 中的函数、作用域和提升有任何问题或其他想法，请在评论中告诉我。

## 资源

*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Guide/Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
*   [https://developer . Mozilla . org/en-US/docs/web/JavaScript/Reference/Operators/function](https://developer.mozilla.org/en-US/docs/web/JavaScript/Reference/Operators/function)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow _ Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
*   https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
*   【https://developer.mozilla.org/en-US/docs/Glossary/Scope 