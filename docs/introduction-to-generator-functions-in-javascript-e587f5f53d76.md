# JavaScript 中的生成器函数简介

> 原文：<https://javascript.plainenglish.io/introduction-to-generator-functions-in-javascript-e587f5f53d76?source=collection_archive---------24----------------------->

![](img/01309f4e1e83b8d0c8e9bce821e302bd.png)

生成器是 JavaScript 中的一个高级概念，但是很容易理解。生成器是 JavaScript 中的特殊函数，它可以根据需要返回多个值，不像常规函数只能返回一个值。

与正常功能不同，发电机功能的执行可在中途**停止**并可恢复。

# 如何创建生成器函数

```
function* generatorFunction(){}
```

创建生成函数有一个特殊的语法，它与普通的函数语法没有太大的不同。

function 关键字后面的*使这个函数成为一个生成器函数。

# 如何使用上面创建的生成器函数

```
function* generatorFunction(){
  console.log("Start")
  yield 7;
  console.log("Midway")
  yield 8;
  console.log("Stop")
}const gen = generatorFunction();let result = gen.next();
console.log(result.value) // logs 7
result = gen.next();
console.log(result.value) // logs 8
```

这里介绍另一个关键词 yield。您可以将 yield 视为返回关键字，但对于生成器函数。让我们举一个例子

让我们看看这里发生了什么:

1.  我们定义一个生成函数，它首先产生(返回)数字 7，然后产生数字 8。我们还添加了几个控制台日志。
2.  我们在这里调用 generatorFunction 并将返回值存储在变量`gen`中
3.  通常，当使用普通函数时，你会期望变量`gen`保存值 7。
4.  但对于发电机来说，情况并非如此。`gen`变量不存储生成器生成的值，而是存储由`generatorFunction`返回的`Generator`对象
5.  `gen`对象有一个方法`next()`
6.  第一次调用`gen.next()`方法开始执行生成器函数，当它到达`yield`时，它在那里停止函数并返回一个具有两个属性`value`和`done`的对象。**值**是产生的值，而**完成**是一个布尔值，它告诉我们发生器功能是否完全执行完毕
7.  所以在上面的例子中，当第一次调用`gen.next()`时，生成器函数开始执行。“开始”被记录到控制台，然后发生器产生值 7。这时它停止函数并返回一个对象，这个对象(在本例中)将是`{ value : 7 , done : false }`。**值**是产出值，为 7。**完成**就是`false`因为发电机还没有完全执行；函数中还有一些代码行尚未执行。“7”被记录到控制台。
8.  `gen.next()`方法的下一次(第二次)调用从它之前停止的点恢复生成器函数。因此，“中途”被记录到控制台，然后生成器产生值 8。它在那里停止函数并返回`{ value: 8, done: false}`,因为产生的值是 8，函数还没有执行完。“8”被记录到控制台。
9.  “停止”不会被记录到控制台，因为我们再也不会呼叫`gen.next()`

# 笔记

*   在上面的例子中，如果我们第三次调用`gen.next()`，控制台上会记录“Stop ”,返回的对象是`{ value : undefined, done : true`。注意这次 done 属性是真的。这是因为生成器的所有代码都已经执行完了。而 value 属性是未定义的？这是因为生成器没有产生任何值。如果在此之后继续调用`gen.next()`，结果将始终是`{ value : undefined, done : true`
*   无法重新启动生成器对象。一旦它执行完毕，你就不能重启它了。如果你想再次运行一个生成器函数，通过调用`generatorFunction`创建一个新的`Generator`对象，并将其存储在一个新的变量中。然后你就可以处理这个变量了。
*   上述观点的例子

```
const newGen = generatorFunction();const newResult = newGen.next():console.log(newResult).value) // logs 7
```

*原发布于*[*https://parth 2412 . hash node . dev*](https://parth2412.hashnode.dev/introduction-to-generator-functions-in-javascript)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)