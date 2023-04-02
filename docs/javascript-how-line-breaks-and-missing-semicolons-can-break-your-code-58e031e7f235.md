# JavaScript:换行符和缺少分号是如何破坏代码的

> 原文：<https://javascript.plainenglish.io/javascript-how-line-breaks-and-missing-semicolons-can-break-your-code-58e031e7f235?source=collection_archive---------4----------------------->

## JavaScript 中自动插入分号的规则和例外

![](img/54c2c4a7b4b4a680330b6407e71c6d5e.png)

Image Courtesy — [Merriam-Webster](https://www.merriam-webster.com/words-at-play/a-guide-to-using-semicolons)

在许多编程语言中，使用分号来结束语句是必须的，但是在 JavaScript 中，它是可选的。如果语句写在单独的行中，可以省略分号。在这种情况下，JavaScript 会隐式添加分号。但是在理解何时在源代码中显式添加分号时应该非常小心，以免破坏代码并导致意外结果。

在本文中，我们将通过例子看到分号自动插入的各种规则和例外。

# 自动分号插入

大多数 ECMAScript 语句和声明必须以分号结束。这样的分号可能总是明确地出现在源文本中。然而，为了方便起见，在某些情况下，这样的分号可以从源文本中省略。描述这些情况的方法是，在这些情况下，分号会自动插入源代码标记流。- ECMAScript 语言规范。

简而言之，JavaScript 编译器会在语句末尾的源代码中添加一个缺少的分号。然而，这个规则也有例外。每当有换行符时，JavaScript 并不总是添加分号。

让我们看一些例子。

## 示例 1

```
let a = 4
[1,2,3].map((arr) => {return arr*3})
```

你认为会有什么结果？它实际上会抛出一个错误。`Uncaught TypeError: Cannot read property ‘map’ of undefined`

在这种情况下，JavaScript 实际上将代码解释为

```
let a = 4[1,2,3].map((arr) => {return arr*3})
```

当代码从左到右被解析而没有分号，并且遇到`[`时，它被解释为前面语句的延续。

为了得到正确的结果，

```
let a = 4;//use a semicolon 
[1,2,3].map((arr) => {return arr*3}) //[3,6,9]
```

令人惊讶的是，下面的作品！

```
let a
[1,2,3].map((arr) => {return arr*3}) //[3,6,9]
```

这是因为变量声明(带有`let, var, const`)本身是完整的语句，JavaScript 编译器总是终止它们。

## 示例 2

```
let a = 4
(3+4).toString()
```

上面的代码也抛出了一个错误。`Uncaught TypeError: 4 is not a function`

解释与`[`相同。JavaScript 编译器将代码解释为

```
let a = 4(3+4).toString()
```

终止第一条语句会给出正确的结果。

```
let a = 4; //use a semicolon
(3+4).toString() //"7"
```

任何以`(`开头的语句，比如命题、表达式(逻辑、算术等等。，)属于这种例外。

```
var s = 23
(function add(a,b){return a + b})(2,3) //Uncaught TypeError: 23 is not a functionvar a,b
a = 4, b = 7
( a > b ) ? alert(a) : alert(b) //Uncaught TypeError: 7 is not a function
```

在语句给出正确结果之前终止该行。

## 示例 3

```
var a = 1+1
+"3" * 5
alert(a) //17
```

在上面的代码中，第二行被解释为第一行的延续。

```
var a = 1+1+"3"*5
```

添加分号会得到预期的结果。

```
var a = 1+1;
+"3" * 5
alert(a) //2
```

与`[`、`(`相同的例外适用于`+`、 `—`、`/`、```

尽管很少出现以`+`、`-`、`/`开头的语句。但是对于以`[`、`(`开头的语句来说，这种情况并不少见，最好是正确处理终止。

甚至可以接受以一个`;`开始语句，以确保该语句被解释为一个新语句，而不是前一个语句的延续。

```
var s = 23
;(function add(a,b){return a + b})(2,3) //5
```

## 实例 4

```
function a(){
  var x = 5
  return
  {
     x
  }
}a(); //undefined
```

为什么`return`值没有正确返回？

这是因为，每当 JavaScript 遇到`return`语句，并且它后面有一个换行符，JavaScript 会自动插入一个分号。

这意味着，无论何时使用`return`语句，`return`关键字之后的标识符必须在同一行。举个例子，

```
return 
true
```

这实际上被解释为，

```
return; true;
```

因此不返回值。

因此，在前面的例子中，`{`应该在同一行的`return`关键字之后开始。

```
function a(){
  var x = 5
  return{
     x
  }
}a(); //{x:5}
```

“无行终止符”规则适用于:

*   后缀表达式(`++`和`--`)
*   `continue`
*   `break`
*   `return`
*   `yield`，`yield*`
*   `module`
*   `throw`

由此给 ECMAScript 程序员的实用建议是:

后缀`**++**`或`**--**`操作符应该与其操作数出现在同一行。

`**return**`或`**throw**`语句中的[表达式](https://tc39.es/ecma262/#prod-Expression)或`**yield**`表达式中的[赋值表达式](https://tc39.es/ecma262/#prod-AssignmentExpression)应该与`**return**`、`**throw**`或`**yield**`标记在同一行开始。

`**break**`或`**continue**`语句中的[标签标识符](https://tc39.es/ecma262/#prod-LabelIdentifier)应与`**break**`或`**continue**`标记在同一行。

- ECMAScript 语言规范

# 结论

我们已经看到了自动分号插入的规则和例外的各种例子。总结一下，

*   如果您的语句以`[`、`(`、`+`、`-`、`/`、```开头，请确保语句前面有分号，以免出错。
*   同时使用`return`、`continue`、`break`等。，确保关键字后的标识符在同一行。

就是这样。希望这篇文章有用！

## 参考资料:

*   [https://tc39 . es/ECMA 262/# sec-rules-of-automatic-分号插入](https://tc39.es/ecma262/#sec-rules-of-automatic-semicolon-insertion)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Lexical _ grammar # automatic _ 分号 _insertion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#automatic_semicolon_insertion)