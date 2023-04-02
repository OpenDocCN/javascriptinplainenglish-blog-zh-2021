# JavaScript 2021:新特性

> 原文：<https://javascript.plainenglish.io/javascript-2021-new-features-429bc050f4e8?source=collection_archive---------0----------------------->

## 今天，我们将讨论 JavasScript 的一些非常有用的新特性，它们可以帮助我们通过编写更少的代码来实现更多的功能。

![](img/51d6d0642df8b4b12614712ec5550d44.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是一种简单易学的编程语言，适合初学者。这些年来，它进化得如此之快，几乎无处不在。我们在前端(React，Angular，或者 Vue.js)，后端(Node.js)，用 ElectronJS 创建桌面应用等都见过。

JavaScript 在 2021 年提供了一些新特性，这在很多方面帮助了开发者。2021 年 JavaScript 的一些新特性是:

## 1)新的逻辑运算符

JavaScript 向现有集合中添加了三个新的逻辑运算符。这三个运算符是，I) `&&=`，II) `||=`，& III) `??=`。让我们详细讨论这些运算符:

**a)** `**&&=**` **操作员:**

在深入解释之前，先看一下下面给出的示例代码:

```
let a = 1;
let b = 2;
a &&= b;
console.log(a) // output for variable 'a' would be 2.
```

行`a&&= b`类似于下面给出的代码块:

```
if(a) {
  a = b;
}
```

这个逻辑运算符是说，如果变量`a`有真值(因为它保存了一个非零值)，那么变量`a`应该被赋予变量`b`的值。这就是为什么当我们做`console.log(a)`时，变量`a`的值计算为 2 而不是 1。

**b)** `**||=**` **运算符:**

考虑下面给出的代码块:

```
let a = 1;
let b = 2;
a ||= b;
console.log(b); // output for variable 'a' would be 1.
```

该操作符与`&&=`操作符相反。在这种情况下，变量`a`将仅等于变量`b`，且仅当变量`a`具有假值时。上面的代码块等效于下面给出的代码:

```
if (!a) {
  a = b;
}
```

**c)** `**??=**` **运算符:**

该操作符检查一个值是**空**还是**未定义**。考虑下面的例子:

```
let a;
let b = 2;
a ??= 1;
console.log(a) // output for variable 'a' would be 1.// this code block is similar to the code given above.
// if(a === null || a === undefined) {
//   a = 1
// }
```

在给出的例子中，变量“a”的值评估为**未定义的**，因此`if`条件评估为`true`，并且“a”被赋值为 1。

## 2)字符串“replaceAll”方法

我们都曾使用 string `replace`方法用我们指定的元素替换字符串中的一个字符或单词。但是它有一个限制，这个方法只替换我们想要替换的字符或单词的第一次出现，字符串中其余的出现保持不变。要替换所有的字符或单词，我们必须使用正则表达式。

示例:

```
// without regex
let str = 'JS is everywhere. JS is amazing!';
console.log(str.replace('JS', 'JavaScript')); // the output would be 'JavaScript is everywhere. JS is amazing!'// with regex
let str = 'JS is everywhere. JS is amazing!';
console.log(str.replace(/JS/g, 'JavaScript')); // the output would be 'JavaScript is everywhere. JavaScript is amazing!'.
```

使用`replaceAll`方法，不再需要正则表达式。考虑下面的代码:

```
let str = 'JS is everywhere. JS is amazing!';
console.log(str.replaceAll('JS', 'JavaScript')); // the output would be 'JavaScript is everywhere. JavaScript is amazing!'.
```

方法`replaceAll`用我们指定的元素替换所有出现的指定字符或单词。

## 3)使用下划线作为整数的分隔符

整数是字符串、数组等数据类型中的一种。有时，整数变得如此之大，以至于几乎很难计算存在的元素的数量，或者计算出这个数字是一百万还是十亿。

通过引入这个特性，我们可以提高整数的可读性。我们可以使用下划线来分隔数字，而无需将数据类型转换为字符串。示例:

```
let number = 1_000_000_000; // one billion
console.log(number) // 1000000000 (the number would remain an integer)
```

## 4) 'Promise.any()'

如果你不知道什么是`promises` JavaScript，那你就先看这里的。

`Promise.any()`是一个新特性，它接受几个可重复的承诺，并返回最先实现的承诺。一个例子会让你明白:

```
const p1 = new Promise(resolve => setTimeout(resolve, 500, 'First'));
const p2 = new Promise(resolve => setTimeout(resolve, 800, 'Second'));
const p3 = Promsie.reject(1);const promises = [p1, p2, p3];Promise.any(promises)
.then(result => {
   console.log(result);
}) // the result would be 'First' because that's the promise, that is fulfilled first.
.catch(e => {
    console.log(e);
})
```

万一没有一个承诺实现，那么我们将得到一个`AggregateError`。为了处理`AggregateError`，我们将在`then`语句之后定义一个`catch`语句。如果你不知道`then` & `catch`块是什么，可以在这里了解一下[。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)

## 5)弱引用和终结符

`WeakRef`是‘弱引用’的简称。`WeakRef`允许持有一个对象的弱引用。被持有的弱引用被称为“目标”。弱引用不会阻止垃圾收集器回收该对象。

垃圾收集是一种收集不再需要的变量的方法，因此可以释放计算机的内存。要了解有关垃圾收集的更多信息，请单击此处的链接。

***注意:*** `*WeakRef*` *只应在特定情况下使用，尽可能避免使用。*

下面我们通过一个例子来理解:

```
const weakRefFunc = () => {
    const obj = new WeakRef({
       name: 'JavaScript'
    });
    console.log(obj.deref().name);
}
const test = () => {
    new Promise(resolve => {
     setTimeout(() => {
       weakRefFunc();
        resolve();
      }, 3000)
    })
    new Promise(resolve => {
     setTimeout(() => {
       weakRefFunc();
        resolve();
      }, 5000)
    })
}
test();
```

`deref`方法返回被持有的目标，如果目标被垃圾回收，则返回**未定义的**。

在这个例子中，变量`obj`是被持有的弱引用。

第一次在`test`函数中调用`weakrefFunc`时，可以保证‘JavaScript’会被打印出来，但是第二次调用时，不能保证‘JavaScript’会被打印出来，因为变量`obj`可能会因为作为弱引用而被垃圾收集。

**最终确定者**

终结器通常与`WeakRef`一起使用，但也可以单独使用。终结器告知对象何时被垃圾回收。让我们通过一个例子来理解这一点:

→首先，我们将使用`FinalizationRegistry`方法创建一个终结器。

```
const registerFinalizer = new FinalizationRegistry(data => console.log(data));const obj = {'name': 'JavaScript'};
registerFinalizer.register(obj, 'obj is collected now!')
```

现在，变量`registerFinalizer`是一个包含我们将要使用的`register`方法的对象。

`registerFinalizer.register`带 2 个参数。第一个是垃圾收集要监视的对象，第二个是当对象被垃圾收集时我们希望显示给控制台的消息。

现在，当变量`obj`将被垃圾收集器收集时，会出现一条消息“obj 现在被收集了！”会被打印到控制台上。

# 结论

总的来说，JavaScript 是一门非常值得学习的语言，其中一个主要原因是它无处不在。我发现上面讨论的这些新特性非常有用。JavaScript 2021 的特性非常惊人，我预计明年也会如此。

希望你学到了新的东西。如果你喜欢这篇文章，最近我写了一篇关于如何在 Google sheets 中使用 Node.js 的文章。你可以在这里看到那个帖子。感谢大家抽出时间阅读这篇文章。

*更多内容请看*[***plain English . io***](http://plainenglish.io)