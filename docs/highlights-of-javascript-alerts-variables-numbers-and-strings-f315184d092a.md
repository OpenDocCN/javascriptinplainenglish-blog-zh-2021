# JavaScript 的亮点——警报、变量、数字和字符串

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-alerts-variables-numbers-and-strings-f315184d092a?source=collection_archive---------14----------------------->

![](img/ed65f460cc429eea629fe7691eff5cde.png)

Photo by [Sheri Hooley](https://unsplash.com/@sherihoo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 警报

`alert`函数显示一个警告框，其中包含一些我们传入的文本。

文本来自字符串参数。

例如，可以写:

```
alert("hello world!");
```

并且将显示“hello world”。

它是一个全局函数，所以它是`window`的一个属性。`window.alert`与`alert`相同。

简短形式可以包含在我们的代码中。

# 变量和字符串

字符串是 JavaScript 代码的基本元素。它们存储文本数据。

具有给定名称的变量只能声明一次。

它们可以存储在变量中。变量是我们选择并赋值的名字，这样我们可以存储它们以备后用。

例如，我们可以写:

```
let name = "james";
```

来储存名字。

我们可以将一个用`let`声明的变量设置为一个新值。

例如，我们可以写:

```
let name = "james";
name = "mark";
```

那么`name`的值将是`"mark"`。

我们可以声明一个变量，而不定义它。

例如，我们可以写:

```
let name;
name = "james";
```

我们可以用用`let`声明的变量做到这一点。

变量可以用不在保留关键字列表中的任何名称来声明。

该列表位于[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Lexical _ grammar # Keywords](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)。

变量不用引号括起来，文本字符串用引号括起来。

JavaScript 字符串可以用单引号或双引号括起来。

它们也可以用反斜杠括起来。

如果它们用反斜杠括起来，那么它们必须嵌入变量。

例如，我们可以写:

```
let firstName = 'james';
let lastName = 'smith';
let name = `${firstName} ${lastName}`;
```

我们将`firstName`和`lastName`的值插入到字符串中。所以`name`应该是`'james smith'`。

这是一个模板文字。我们可以在字符串中放入任何表达式。

这是将各种表达式组合成一个字符串的非常方便的方法。

现在我们可以分配变量，我们可以将变量传递到`alert`中，而不是传递整个字符串。

例如，我们可以写:

```
let text = "hello world!"
alert(text);
```

我们将`text`作为参数传递给`alert`来显示警告。

在定义了`text`之后，我们可以在任何地方引用它。

# 变量和数字

数字是 JavaScript 的另一种基本数据类型。

我们也可以把它们赋给变量。

例如，我们可以写:

```
let length = 100;
```

这使得在其上进行操作变得容易。例如，我们可以给`length`加上一个数字:

```
length + 10
```

那么`length`和 10 之和就是 110。

我们知道`length`不是一个变量，因为它没有用引号括起来。

只有数字可以用作变量名，所以 JavaScript 知道它是一个数字。

我们可以通过把 10 赋给一个变量来代替 10。

例如，我们可以写:

```
let length = 100;
let additionalLength = 10;
let totalLength = length + additionaLength;
```

我们将`additionalLength`变量添加到`length`中，并将总和赋给`totalLength`变量。

# 结论

我们可以创建变量来存储数字和字符串，并在警报中使用它们。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**