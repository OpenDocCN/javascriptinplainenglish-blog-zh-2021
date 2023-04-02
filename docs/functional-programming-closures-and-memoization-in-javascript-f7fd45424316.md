# 函数式编程:JavaScript 中的闭包和记忆化

> 原文：<https://javascript.plainenglish.io/functional-programming-closures-and-memoization-in-javascript-f7fd45424316?source=collection_archive---------2----------------------->

这篇文章的目的是解释如何在 JavaScript 中实现闭包和记忆化。当我编码时，我学得更好，如果你像我一样，那么你一定会喜欢这篇文章。

![](img/a905ef15124e34f9dff4c6b8c9a4852f.png)

Photo by [Irvan Smith](https://unsplash.com/@mr_vero?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

现在，在我们进入主题之前，让我们总结一下我们所知道的函数式编程——什么是闭包，当我们使用术语记忆化时，我们实际上指的是什么？

> **功能编程**

函数式编程是一种 ***声明式*** 类型的编程风格。这是一种编程范式，在这种范式中，我们试图以纯数学函数的方式绑定一切。它的主要焦点是“解决什么”,而命令式风格的主要焦点是“如何解决”。

函数式编程基于 Lambda 演算。它的基本工作原理是，函数在 JavaScript 中被视为一等公民。函数也可以是高阶函数。高阶函数是将其他函数作为参数并返回另一个函数的函数。

> **关闭**

即使在父函数已经执行之后，当子函数保持父作用域的环境时，就会创建闭包。这是 MDN 网站上的更多内容。

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) [## 关闭

### 闭包是捆绑在一起(封闭的)的函数与对其周围状态的引用的组合

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) 

> **记忆化**

记忆化是缓存的一种特殊形式。缓存是一种通过在内存中保存非常具体的信息来加速程序的方法。

让我们用一个例子来证明它:

让我们创建一个简单的函数，将 80 加到一个数上并返回它。

```
function addTo80(num) {
   return num + 80;
}console.log(addTo80(5));            // Computes and returns 85
console.log(addTo80(5));            // Computes and returns 85
console.log(addTo80(5));            // Computes and returns 85Output:
85
85
85
```

上述程序将计算相同的函数 3 次，并返回结果。现在，这是一个非常简单的函数，执行起来可能不会占用太多内存和时间。但是请考虑一个更复杂的函数，它一次又一次地执行相同的任务。例如，使用递归找到斐波纳契数列[的第 100 个元素。这就是记忆化真正有效的地方，它可以节省大量的计算时间。](https://en.wikipedia.org/wiki/Fibonacci_number)

对上面的例子进行改进，让我们创建另一个函数 memoizedAddto80()并获取一个缓存对象，该对象在计算出特定参数的值后保存数据(在内存中)。让我们看看实际情况:

```
function addTo80(num) {
   return num + 80;
}let cache = {};
function memoizedAddTo80(num) {
  if (num in cache) {
    return cache[num]; 
  } else {
    console.log('Calculating...');
    cache[num] = num + 80;
    return cache[num];
  }
}// Computes and stores 85 in cache
console.log(memoizedAddTo80(5));// Returns memoized data from memory
console.log(memoizedAddTo80(5));// Returns memoized data from memory
console.log(memoizedAddTo80(5));// Output:
Calculating...
85
85
85
```

上面的代码片段会将结果计算一次为 85，然后将其存储在缓存对象中，如下所示:

```
cache: {
   5: 85
}
```

现在，下一次调用 memoizedAddTo80(5)时，它将在内存中查找并直接返回它，因为它之前已经被计算过了。与再次执行相同的操作相比，这个操作真的很快。

等等，这里有几个你可能会想到的问题:

1.  创建一个可以在应用程序中的任何地方更改的全局对象缓存，我们没有污染全局名称空间吗？
2.  *哪里在使用封闭？*

是的，你猜对了！我们确实污染了全局名称空间，而且闭包仍然没有运行。

让我们重构代码来实现和解决上面列出的两个问题:

```
function addTo80(num) {
   return num + 80;
}function memoizedAddTo80() {
 let cache = {};
 return function(num) {
    if (num in cache) {
      return cache[num]; 
    } else {
      console.log('Calculating...');
      cache[num] = num + 80;
      return cache[num];
    } 
  }
}const memoized = memoizedAddTo80();// Computes and stores 85 in cache
console.log(memoized(5));// Returns memoized data from memory
console.log(memoized(5));// Returns memoized data from memory
console.log(memoized(5));// Output:
Calculating...
85
85
85
```

现在，这一次我们将全局对象缓存移到 memoizedAddTo80()函数中，以防止全局名称空间污染。问题 1 解决。现在谈谈问题 2。

还记得闭包吗？

> 即使在父函数已经执行之后，当子函数保持父作用域的环境时，就会创建闭包。

从 memoizedAddTo80()函数内部，我们返回另一个函数，它跟踪父函数中使用的缓存对象。这是行动中的终结。内部函数可以访问外部函数的属性(缓存对象)的状态。

```
return function(num) {
    if (num in cache) {
      return cache[num]; 
    } else {
      console.log('Calculating...');
      cache[num] = num + 80;
      return cache[num];
    } 
  }
```

现在，这个内部函数可以被调用任意多次，它将只执行一次，并且在调用多次时返回内存化的数据。

以下是所有内容的演示:

[](https://replit.com/@akashkriplani/Closures-and-Memoization#index.js) [## 闭包和记忆

### akashkriplani 的 Node.js repl

replit.com](https://replit.com/@akashkriplani/Closures-and-Memoization#index.js) 

***又有了。我希望这篇文章对你有用。感谢您的阅读。请随时提供您的意见、建议和任何其他可能有帮助的反馈。***

[*更多内容尽在 plainenglish.io*](https://javascript.plainenglish.io/)