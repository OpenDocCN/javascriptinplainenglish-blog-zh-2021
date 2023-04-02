# JavaScript 中的部分应用

> 原文：<https://javascript.plainenglish.io/partial-applications-in-javascript-4ee3c2a47cfb?source=collection_archive---------14----------------------->

![](img/f60fce8820de8dc321d3b943c68cbcb9.png)

随着 Redux JavaScript 库、Reason 语法和工具链的引入，循环库函数式编程在 JavaScript 中变得越来越重要。

函数式编程简单地描述了通过应用和组合函数构建的程序。

源于函数式编程的一个重要概念是*部分应用*，其中值被固定到函数的一些参数，而函数没有被完全评估。

局部应用是由*到*一个函数完成的事情；当一个函数被调用时，它的一部分是从外部应用的——这个功能不是内置在函数本身中的。按照这个逻辑，任何接受参数的函数都可以部分应用。

## 部分应用示例

如同大多数(如果不是全部的话)编程一样，部分应用程序在上下文中更容易理解。下面我们有一个简单的 JavaScript 函数:

```
const sumFiveNumbers = (a, b, c, d, e) => a + b + c + d + e;
```

通常，要调用这个函数，我们需要提供五个参数:

```
const resultOne = sumFiveNumbers(3, 4, 5, 10, 1); console.log(resultOne); //23
```

如上所示，该控制台记录功能的评估结果为 **23** 。现在， **sumFiveNumbers** 的一个部分应用示例可以是:

```
const partiallyAppliedSumFiveNumbers = sumFiveNumbers.bind(null, 6, 4); 
```

**sumFiveNumbers** 期望五个参数，但是借助**。bind()** 我们能够在只提供两个(或者比预期的五个少的任意数量的参数)参数的情况下调用这个相同的函数。这里**。bind()** 允许我们传入第一个参数( **null** )作为返回函数的上下文，然后传入这个返回函数的参数列表的值( **6** 和 **4** )。

所以在这个例子中， **6** 是分配给 **a** 的值， **4** 是分配给 **b** 的值(属于 **sumFiveNumbers** 函数)。

我们正在围绕这些参数创建一个*闭包*，并返回一个已经知道这些值的新函数，并且正在等待另外 3 个参数:

```
const resultTwo = partiallyAppliedSumFiveNumbers(2, 4, 1);console.log(resultTwo); //17
```

在第二次调用**partiallyAppliedSumFiveNumbers**时，我们提供剩余的三个参数值，允许 **sumFiveNumbers** 计算并返回结果( **17** )。

要考虑的另一个概念是，部分应用的功能可以部分应用多次。例如，在本例中，我们可以用一个(或两个)参数而不是剩余的三个参数来调用**partiallyAppliedSumFiveNumbers**，在这种情况下，函数在计算之前仍然会等待剩余的参数——

```
const anotherPartiallyAppliedSumFiveNumbers = partiallyAppliedSumFiveNumbers.bind(null, 2); 
```

上面我们再次*将返回函数的上下文*绑定到 **null** 并提供了 **2** 的单个参数。现在 **sumFiveNumbers** 函数正在等待另外两个参数来评估。

```
const resultThree = anotherPartiallyAppliedSumFiveNumbers(4, 1); console.log(resultThree); //17
```

我们现在已经提供了 **sumFiveNumbers** 所需要的所有参数，并且该函数能够进行求值，从而得到 **17** 的和。

## 闭包——局部应用的一个基本概念

部分应用程序由于闭包的概念而工作。

内部函数(**partial appliedsumfiftnumbers**和**other partial appliedsumfiftnumbers**)可以访问父函数(**sum fiftnumbers**用于两个局部函数，以及**partial appliedsumfiftnumbers**用于**other partial appliedsumfiftnumbers**)的所有参数值，即使在父函数返回之后也是如此。

这是一个*闭包—* 每当一个函数返回另一个函数时，这个返回的函数就可以访问在父函数范围内初始化的任何变量。

## 结论

部分应用程序允许您修复函数的参数——提供从更一般的函数中派生具有特定行为的新函数的能力。