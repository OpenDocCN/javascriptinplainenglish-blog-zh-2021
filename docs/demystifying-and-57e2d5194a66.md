# 揭开 JavaScript 中“==”和“===”的神秘面纱

> 原文：<https://javascript.plainenglish.io/demystifying-and-57e2d5194a66?source=collection_archive---------22----------------------->

![](img/d94de22ce1da9226a1e4b495653bc5d9.png)

每个 JavaScript 开发人员在职业生涯中最常遇到的一个面试问题就是:*“*`*==*`*和* `*===*` *有什么区别？”嗯，我想大多数读到这里的人可能已经得出了最常见的答案*

> “==”比较值，“===”比较值和类型。

如果我说这不是正确的答案呢🙈。让我们深入了解一下幕后发生的事情。根据 ECMA 脚本规范，`==`和`===`都会检查变量的类型。如果类型相同，`==`和`===`工作完全相同，它们根据值返回`true`或`false`。当变量的类型不匹配时，两者是不同的。😳

当类型不同时，`==`进行隐式强制，而`===`直接返回`false`。隐式强制无非是将变量从一种类型转换为另一种类型。

根据 ECMAScript 规范，每当 JavaScript 遇到一个`==`操作符，就会调用一个名为`IsLooselyEqual ( x, y )`的抽象操作。类似地，当它遇到一个`===`操作符时，就会执行一个叫做`IsStrictlyEqual ( x, y )`的抽象操作。我知道这可能太多了，一时难以消化，但是让我们在一些代码片段的帮助下试着理解这两个操作。我们不会涵盖操作的所有情况，而是会尝试处理一些我们通常会遇到的常见场景。

# 案例 1:

```
var stringOne = '1';
var numberOne = 1;if (stringOne == numberOne) {
  console.log("IsLooselyEqual(x,y) is invoked");
}
```

在上面的代码片段中，我们有两个变量——类型分别为`string`和`number`的`stringOne`和`numberOne`。之后我们有一个条件语句，在这里我们使用`==`操作符检查`stringOne`和`numberOne`是否相等。一旦 JavaScript 遇到`==`操作符，它就应用`IsLooselyEqual(x,y)`抽象操作。根据该操作，完成以下步骤。

1.  检查`stringOne`和`numberOne`的类型是否相同。如果相同，则通过应用`IsStrictlyEqual(x, y)` [(实际算法的第二步)](https://tc39.es/ecma262/#sec-islooselyequal)抽象运算返回值，其中`x`分别为`stringOne`和`y`为`numberOne`。
2.  如果类型不相同，则检查`stringOne`的类型是否为`String`类型，以及`numberOne`的类型是否为`Number`类型[(实际算法的步骤 6)](https://tc39.es/ecma262/#sec-islooselyequal)。因为它是真的，所以它通过应用`ToNumber(x)`抽象操作将`stringOne`变量转换为`Number`类型。`ToNumber(x)`是另一个将变量转换成`Number Type`变量的抽象操作。在这种情况下，`stringOne`将是`x`，应用`ToNumber(x)`操作将是`ToNumber(stringOne)`，其中`stringOne`将基于此的[从`String`类型转换为`Number`类型。之后，它通过再次应用`IsLooselyEqual(x, y)`抽象运算返回值，此时`x`和`y`属于同一类型。](https://tc39.es/ecma262/#sec-tonumber)
3.  由于两者属于同一类型，它通过应用`IsStrictlyEqual(x,y)`抽象运算返回值。
4.  `[IsStrictlyEqual(x,y)](https://tc39.es/ecma262/#sec-isstrictlyequal)`检查`x`和`y`的类型是否相同。如果类型相同，检查`x`和`y`的值。如果值也相同，那么操作将返回一个`true`，否则将返回一个`false`。

# 案例二:

```
var arrayOne = ['1'];
var numberOne = 1;if (arrayOne == numberOne) {
  console.log("IsLooselyEqual(x,y) is invoked");
}
```

在上面的代码片段中，我们有两个类型分别为`object`和`number`的变量`arrayOne`和`numberOne`。之后我们有一个条件语句，在这里我们使用`==`操作符检查`arrayOne`和`numberOne`是否相等。JavaScript 一遇到`==`操作符，就会应用`IsLooselyEqual(x,y)`抽象操作。根据该操作，完成以下步骤。

1.  检查`arrayOne`和`numberOne`的类型是否相同。如果相同，则应用`IsStrictlyEqual(x, y)`抽象运算返回值，其中`x`分别为`arrayOne`和`y`分别为`numberOne`。
2.  如果类型不相同，则检查`arrayOne`的类型是否为`Object`类型，以及`numberOne`的类型是否为`String, Number etc`类型[(实际算法的步骤 12)](https://tc39.es/ecma262/#sec-islooselyequal)。因为这是真的，所以它通过应用`ToPrimitive()`抽象操作将`Object`类型变量转换为`Primitive`类型。简而言之，该操作试图将`Object`类型转换为`Primitive`类型，该类型可以是`String`或`Number`类型[(top primitive)](https://tc39.es/ecma262/#sec-toprimitive)。
3.  然后通过传递`x`和`y`应用`IsLooselyEqual(x, y)`操作返回值，并重复相同的步骤，直到`x`和`y`的类型相等或者当`IsLooselyEqual(x, y)`操作返回`false`时。

# 案例三:

```
var objectOne = [];
var booleanOne = true;if(objectOne) {
  console.log("This check whether array is empty or not won't work !!")
}
```

在上面的代码片段中，我们有两个类型分别为`object`和`boolean`的变量`objectOne`和`booleanOne`。之后，我们有一个条件语句，在这里我们检查`objectOne`是否是`true`。JavaScript 一遇到这种情况，就会应用一个新的抽象操作`ToBoolean(x)`。该操作根据 [(ToBoolean)](https://tc39.es/ecma262/#sec-toboolean) 中的参考表将变量转换为`Boolean`类型。

基于这个表，因为我们的变量是类型`Object`的，所以不管数组是否为空，它都会返回给我们`true`。这是我们在比较`Object`类型时需要其他参数的主要原因。在我们的例子中，因为我们清楚地知道它是一个数组对象，我们可以使用`length`属性。现在我们可以用下面的方法重构上面的代码来检查是否为空。

到目前为止，我希望您已经理解了 JavaScript 如何处理`==`和`===`操作符以及它们实际上不同时的情况。上述情况只是许多情况中的几个。如果你真的有兴趣深入挖掘，我会推荐你浏览一下 [ECMA 规范](https://tc39.es/ecma262/#sec-islooselyequal)，在那里你会找到`IsLooselyEqual(x,y)`和`IsStrictlyEqual(x,y)`抽象操作的完整实现。我也鼓励你读这本书，如果你还没有- [你不知道由](https://github.com/getify/You-Dont-Know-JS/tree/1st-ed)[凯尔·辛普森](https://www.linkedin.com/in/getify/)写的 JS 。

# 谢谢你

希望你喜欢这篇关于`==`和`===`操作符以及 JavaScript 中如何进行比较的文章。现在，你可以利用这些知识在即将到来的面试中真正解决上述问题😜。请在下面的评论区告诉我你的想法。如果你觉得这篇文章是有用的，请展示你的爱，并与你能最大限度利用这篇文章的伙伴们分享。

请随时通过 Twitter、LinkedIn 或电子邮件与我联系。乐意尽一切可能提供帮助。😊

直到我们再次见面，Mallu Dev 结束👋干杯！🥂

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)