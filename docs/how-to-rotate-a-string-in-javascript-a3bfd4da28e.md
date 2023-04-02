# 如何在 JavaScript 中旋转字符串

> 原文：<https://javascript.plainenglish.io/how-to-rotate-a-string-in-javascript-a3bfd4da28e?source=collection_archive---------4----------------------->

## 定义算法，使用切片字符串方法，模操作符等等。

![](img/65969e374626ac77cc570cdd7e4de045.png)

Photo by [Mikael Kristenson](https://unsplash.com/@mikael_k?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/rotate-tool?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

本文描述了如何编写一个简单的字符串旋转算法。它还处理特殊字符采用两个代码单元的情况。

要了解如何计算新字符串，请查看几个示例。

*   将字符串`ABCDE`向左旋转`1`字符导致`BCDEA`
*   尝试将同一文本旋转 2 个字符会导致`CDEAB`。

重要的是要注意当试图旋转的字符数大于字符串大小时会发生什么。例如，通过`6`字符旋转得到`BCDEA`，通过`7`字符旋转得到`CDEAB`

# 向左旋转

现在让我们尝试实现这样一个算法，并将其封装在一个函数中。

```
function rotate(text, noOfChars = 0){
  return text;
}
```

首先，我们需要检测要旋转的字符数。当`noOfChars`小于字符串的大小时，我们得到这个值，但是当文本的大小小于`noOfChars`时，我们需要检测这个数字。

当您查看结果时，将一串`5`字符旋转`6`字符与旋转`1`字符是一样的。按`7`字符旋转与按`2`字符旋转相同。要旋转的字符数实际上是给定数字和字符串大小之间的模。

```
6 % 5 === 1
7 % 5 === 2
```

当您检查可用于提取部分字符串的方法时，您可以在`subtring`、`substr`和`slice`之间进行选择。我会选择`slice`，但同样的行为可以在他们中的任何一个身上实现。

`slice(start, end)`方法返回字符串的一部分，从给定的`start`索引开始，在`end`索引之前结束。从`0`索引开始提取部分字符串时，指定的字符数基本上就是结束索引。

```
"ABCDE".slice(0, 1)
//'A'"ABCDE".slice(0, 2)
//'AB'
```

第二个参数是可选的。未指定时，`slice`提取所有字符，直到字符串结束。

```
"ABCDE".slice(1)
//'BCDE'"ABCDE".slice(2)
//'CDE'
```

这是我们算法的样子。

```
function rotate(text, noOfChars = 0){
  const n = noOfChars % text.length;
  return text.slice(n) + text.slice(0, n); 
}rotate("ABCDE", 1)
//BCDEArotate("ABCDE", 2)
//CDEAB
```

如果我们使用模板字面语法来写，也许会更清楚。

```
function rotate(text, noOfChars = 0){
  const n = noOfChars % text.length;
  const part1 = text.slice(0, n);
  const part2 = text.slice(n);
  return `${part2}${part1}`;
}
```

# 向右旋转

将文本`ABCDE`向右旋转`1`字符导致`EABCD`

由`2`人物旋转出`DEABC`。

按`3`字符旋转导致`CDEAB`。

通过`4`字符旋转给出`BCDEA`。

按`5`字符旋转没有改变，它给出的结果与输入文本`ABCDE`中的结果相同。

按`6`字符旋转与按`1`字符旋转相同。它给出了`EABCD`。

请注意，向右旋转文本与向左旋转文本效果相同，但字符数不同。

*   用`1`向左旋转与用`4`向右旋转的结果相同。
*   通过`2`字符向左旋转与通过`3`字符向右旋转相同。
*   用`3`向左旋转返回`DEABC`，与用`2`向右旋转相同。
*   用`4`向左旋转产生`EABCD`，用`1`向右旋转也一样

通过`n`字符向右旋转与通过`textSize — n`字符向左旋转相同。

```
function rotateRight(text, noOfChars = 0){
  const n = noOfChars % text.length;
  return rotate(text, text.length - n);
}rotateRight("ABCDE", 1)
//EABCDrotateRight("ABCDE", 2)
//DEABC
```

# 处理采用两个代码单元的字符

遗憾的是，之前的解决方案在处理像表情符号这样采用两个代码单元的角色时不起作用。检查下一个电话。

```
rotate("😐ABC", 1)
//'�ABC�'
```

一种可能的解决方案是将字符串转换为字符数组，旋转该数组，然后将结果转换回新字符串。这是下一个函数要做的。

```
function rotate(text, noOfChars = 0){
  const chars = Array.from(text);
  const n = noOfChars % chars.length;
  const newArr = chars.slice(n).concat(chars.slice(0, n));
  return newArr.join("");
}rotate("😐ABC", 1)
//'ABC😐'
```

`Array.from`实用程序可以将一个字符串转换成一个字符数组。

数组方法与字符串方法的工作原理相似。它将数组的部分内容提取到新的中，该新的包含给定开始和结束索引之间的元素。

array 方法将两个数组连接成一个新的数组，这个新数组按顺序包含两个数组中的元素。

用空字符串调用的`join`数组方法将新的字符数组转换回新的字符串。

# 关键注意事项

*   `slice`方法返回一个新字符串，从给定的起始索引开始，在结束索引之前结束。
*   当我们需要旋转一个字符串，旋转的次数大于字符数时，我们需要用它除以文本的大小，并使用余数。这可以通过模运算符(`%`)来完成。
*   通过`n`字符向右旋转字符串与通过`size — n`字符向左旋转相同。
*   当处理包含两个代码单元的字符的字符串时，我们可能需要将其转换为字符数组，处理该数组，然后将结果转换回字符串。

感谢阅读。

你也可以查看[如何在大数组中寻找元素](https://medium.com/programming-essentials/how-to-find-elements-in-large-arrays-6f337a00b216)。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)