# 如何防止 JavaScript 中意外的变量突变

> 原文：<https://javascript.plainenglish.io/how-to-prevent-unexpected-variable-mutation-in-javascript-2612b898732c?source=collection_archive---------13----------------------->

## 有没有遇到过这样的问题，一个变量突然包含了你没有预料到的东西？有简单的方法来防止这种事情再次发生！

![](img/264fb5ac547e481a720b49af9989c2f3.png)

所以当你使用 JavaScript 时，你可以灵活地用任何东西覆盖任何变量。这可能是有用的，但也可能是痛苦的。这也是为什么许多 JavaScript 开发人员转向 TypeScript 的原因。(还有很多好处，但那是以后的事了)

所以看看下面的代码样本，你会期望发生什么。你希望会发生什么？

```
var a = 'test';
[50 lines of code]
var a = 1;
console.log(a);
```

因此，对于上面的示例，您可能希望`console.log`输出“test ”,因为这是您分配给它的。您可能忘记了变量的第二个声明，现在您很困惑为什么变量包含一个数字，而不是字符串`test`。这可能是个问题。

幸运的是，IDE 可以帮助您找到声明该变量的位置，但是情况可能比这复杂得多，并且需要您花费时间来调试这个问题。

那么，如何在第一时间防止这种情况发生呢？好了，是时候研究一下作为变量声明的`let`和`const`了。

# 转让 var 的好处

因此，首先我们将查看`let`声明。与`var`相比，`let`有几个好处，这会让你永远不会再使用`var`。让我们来看看上面的代码示例，但是用`let`替换了`var`。

```
let a = 'test';
[50 lines of code]
let a = 1;
console.log(a);
```

你可能会想，`console.log`会再输出`1`，但是再猜一次。这是您现在运行这段代码时得到的结果:

```
SyntaxError: Identifier 'a' has already been declared
```

这里发生的是`let`阻止你两次重新声明同一个变量。这将防止你意外地覆盖你已经声明的任何内容。

但是，这并不能防止变量被覆盖。因为，这还是有可能的:

```
let a = 'test';
[50 lines of code]
a = 1;
console.log(a);
```

这里我们仍然会有一个`1`的输出，并且不会有错误。这可能是您对代码的期望，在这种情况下，这是完全没问题的，但是如果变量应该保持不变，您可能希望防止这种情况。

那么如何预防这种情况呢？好了，是时候看看`const`了

# const 优于 let 的优势

查看`const`时，你可能已经注意到它的名字应该是`constant`。这正是它的用途。您在`const`中设置的任何内容都将保持不变。再拿同样的代码来说:

```
const a = 'test';
[50 lines of code]
a = 1;
console.log(a);
```

那么您将得到以下错误:

```
TypeError: Assignment to constant variable.
```

如果第二个赋值是一个字符串，而在我们的例子中没有显示数字，也会发生这种情况。

这将完全防止你用其他东西覆盖这个变量。老实说，你多久需要用一个不同的值覆盖一个变量？比你想象的要少得多。

# 结论

所以无论何时你声明了一个不需要改变的变量，使用`const`。如果你设计你的代码有一个变化的变量，使用`let`。一个很好的例子就是`for`循环

```
for (let i = 0; i < 10; i++)
```

或者当你像这样处理文本操作时

```
let text = "a.d.c";
text = text.replace('d','b');
console.log(text);
```

但是在上面的例子中，您可能已经考虑过只保留原来的文本，而在一个新的变量中设置新的文本。

```
const originalText = "a.d.c";
const newText = originalText.replace('d','b');
console.log(newText);
```

声明一个新变量不仅没有什么不好的地方(除了临时的几个字节的内存)，还使得文本可读性更好。

但是总结一下，并引用 [Evert Pot 在他的博客](https://evertpot.com/javascript-let-const/)

*   停止使用`var`。
*   默认使用`const`，无处不在。
*   如有必要，使用`let`

## 进一步阅读

*   [打开 MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
*   [MDN 上的常量](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)