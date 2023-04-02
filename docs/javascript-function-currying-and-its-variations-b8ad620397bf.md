# JavaScript——函数曲线及其变体

> 原文：<https://javascript.plainenglish.io/javascript-function-currying-and-its-variations-b8ad620397bf?source=collection_archive---------7----------------------->

![](img/73cf0079865d31737e378e62438731a0.png)

## **功能电流定义:**

*“curry ing”是一个函数编程的过程，在这个过程中，我们可以将一个有多个参数的函数转换成一系列嵌套的函数。它返回一个新的函数，该函数预期内联下一个参数。”*

让我们从一个简单的例子开始，我们将编写一个函数，将两个数字相加并返回总和。

```
function add(a, b){
   return a + b;
}
let output = add(10,20);
console.log(output) // output will be 30
```

正如大多数人所知，上面是一个简单的函数，它接受 2 个参数，将其相加并返回总和。当我们提前知道两个参数并想计算其和时，这个函数就可以了。

如果我们有一个场景，其中两个参数在代码块的两个不同的地方是已知的，该怎么办？一旦这两个数字都可用，我们就调用 add 函数？有很少的方法可以解决这个问题，我们可以使用 JavaScript bind 来达到同样的目的，但是最优选的方法是使用**来讨好**。

让我们修改上面的例子，使其在程序的两个不同部分接受两个参数。

```
function add(a){
  return function(b){
    return a + b;
  }
}let fnCall = add(10);
console.log(fnCall(20)); //output will be 30
```

仔细观察上面的代码片段，我们有一个外部函数 add，它接受一个参数，当您调用它时，它将返回一个接受另一个参数的函数。通过 JavaScript 闭包属性，内部函数将可以访问传递给 add 函数的变量“a”。如果您不知道什么是结束，请阅读我关于它的文章([JavaScript clo 高利贷——棘手的采访主题](https://mevasanth.medium.com/javascript-clousures-tricky-interview-topic-3e129435083e))

现在每当我们得到第二个参数，我们就调用内部函数，其引用出现在变量 fnCall 上，因此上面代码的输出将是 **30** 。

现在让我们看看它的一个小偏差，这是在面试中经常被问到的问题。

写一个加两个数字的函数，函数调用应该是这样的——**add(10)(20)。**

不要惊慌，这也是函数 currying，在一段时间内调用两个嵌套的函数。代码片段如下所示。

```
function add(a){
  return function(b){
    return a + b;
  }
}let output = add(10)(20);
console.log(output); //output will be 30
```

## **功能趋利的主要用例是什么？**

1.  正如您已经看到的，当函数所需的参数在代码中的不同位置可用时，我们可以使用函数 currying。
2.  最适合执行与数学函数相关的数学运算，这涉及到像 **f(g(x)) (** 我将在**下面为它写一个例子)。**
3.  函数 currying 也可以扩展到接受无限个参数(显然直到内存中有空间可供计算)。当我们必须执行一个特定的任务时，这很有帮助，不管传递给函数的参数是什么，然后我们可以使用函数 currying。(下面有一个相同的例子)

## **使用函数 currying 编写数学函数**

```
const f = x => x + x
const g = y => y * ylet output =  f(g(10))
console.log(output) //output will be 200
```

在上面的代码块中，我们编写了两个名为**“f”、“g”的函数。**当我们编写函数调用 f(g(10))时，我们将值 10 传递给函数 g()，该函数将传递的参数相乘，因此值将是 10*10 = 100。

这个 100 作为参数传递给函数 f()，传递的值加在函数 f()内部，所以输出是 100 + 100 = **200。**根据您执行的数学计算，这可以嵌套到任何层次结构中。

注意:对于那些想知道 **const g = y = > y * y** 如何将 y 的值相乘并返回的人，这是 arrow 函数的默认行为，当你没有指定括号时，值被计算并返回。如果您添加了花括号，则应该手动返回该值。

## **扩展 currying 以在函数中添加无限个数字**

让我们扩展上面的函数 add，这样它可以接受无限个参数，将它们相加并返回总和。

**对于 ex 函数调用应该是这样的:**

`add(10)(20)(30)()`

`add(10)(20)(30)(40)(50)(60)()`

`add(10)(20)()`等。

## **这是 JavaScript 面试中最常见也是最棘手的面试问题之一。**

在所有这些不同的函数调用的情况下，你的 currying 函数应该能够计算总和。当你看到这个问题时，你的思维应该是递归的，这里函数调用的分隔符是最后一个空括号，在递归术语中，这是基本情况。

函数 currying 中没有内置的属性来处理这种情况，我们需要结合 currying 和递归的概念来解决这个问题。工作代码片段如下。

```
function add(a){
  return function(b){
    if(b){
      return add(a+b)
    }else{
      return a
    }
  }
}
let output1 = add(10)(20)();
let output2 = add(10)(20)(30)(40)();
console.log(output1); //output will be 30
console.log(output2); //output will be 100
```

在上面的递归代码中，我们一直运行这个函数，直到我们遇到一个空括号，如果不是，那么我们将计算这个和，并把它存储在变量 a 中，变量 a 在最后返回。

## **给读者的困惑**

现在你知道了如何一起使用递归和 currying。现在一些高明的面试官会问你一个类似下面的问题。

编写一个函数 add，它在被调用时给出总和，如下所示，

`add(10)(20)`

`add(10,20)`

正如你所观察到的，第一个是你如何调用 currying 函数，第二个是你如何调用一个普通的函数，所以你写的函数应该两种方式都有。

这个问题我不回答，给你个提示。使用 JavaScript arguments 属性，它将为您提供传递给函数的一组参数，并在条件中使用它来区分函数是像 currying 还是像 normal function 一样被调用。

**同一作者的其他有趣文章**

1.  [JavaScript 中的一切都是对象吗？](https://mevasanth.medium.com/how-everything-is-object-in-javascript-a4164d7e6a2d)
2.  [JavaScript 吊装:访谈热点](https://mevasanth.medium.com/hoisting-in-javascript-hot-topic-for-interview-43b463a6a77?source=follow_footer---------0----------------------------)
3.  [JavaScript 中的记忆化——采访热门话题](https://mevasanth.medium.com/memoization-in-javascript-hot-topic-for-interview-815475544ab0)

点击[此处](https://mevasanth.medium.com/)查看作者所有文章。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)