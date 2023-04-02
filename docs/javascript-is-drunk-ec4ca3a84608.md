# JavaScript 醉了

> 原文：<https://javascript.plainenglish.io/javascript-is-drunk-ec4ca3a84608?source=collection_archive---------7----------------------->

## 弱类型编程语言的奇特之处

![](img/a4f2c3433f1c99619de2a7674abd785e.png)

Photo by [Jason Strull](https://unsplash.com/@jasonstrull?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是一种弱类型编程语言。换句话说，它对你的变量类型做出假设，因为你不能指定它们。

在强类型编程语言中，比如 Java，你必须指定你的变量类型。这允许编译器在运行前捕捉更多的错误，比如不允许将某种类型的值赋给另一种类型的变量。这保证了你得到的结果更有可能是你期望的结果。

## 那么 JavaScript 为什么不这么做呢？

简单的答案是 JavaScript 没有编译步骤，否则强类型语言会验证类型。这种语言是为浏览器在网站上编写脚本而设计的。这通过为开发人员做决策而减少了他们的工作，但代价是可能产生错误的结果。

![](img/8b49c76e81b5b07711c0c946a9a78f2e.png)

[https://knowyourmeme.com/memes/ive-won-but-at-what-cost](https://knowyourmeme.com/memes/ive-won-but-at-what-cost)

看看这个用 Java 写的代码片段。

```
public class HelloWorld { public static void main(String[] args) {
    String first = “1”;
    int second = 1;
    System.out.println(first — second);
  }
}// Output: error: bad operand types for binary operator '-'
// Java threw an error because it cannot subtract a string.
```

现在让我们用 JavaScript 做同样的事情。

```
var first = "1"
var second = 1
console.log(first - second)// Output: 0
// JavaScript implicitly converted "1" to 1, and computed 1 - 1.
```

如您所见，Java 抛出了一个错误，而 JavaScript 没有，代价是产生了一个潜在的意外结果。

让我们来看看 JavaScript 隐式类型转换的几种奇怪结果。我将解释 JavaScript 在做什么，甚至试图解释它为什么要这么做。

但是，就像你在感恩节喝醉的叔叔一样，有时我不太确定 JavaScript 为什么会这样做。

## 3 个奇怪的 JavaScript 隐式类型转换

> `“11” + 1 = "111"`但是`“11” — 1 = 10`

对于前者，JavaScript 将 1 转换为“1”，从而连接两个字符串。

对于后者，JavaScript 将“11”转换为 11。这可能是因为它不能减去字符串，所以它假定“11”是一个数字。

> `[] + {} = "[object Object]”`但是`{} + [] = 0`

我们已经非常深入地了解了 JavaScript 的奥秘，但是让我们来分析一下。

对于前者，JavaScript 将`[]`和`{}`都转换成字符串。这导致了连接`"" + "[object Object]”`。

对于后者，JavaScript 将`{}`解析为空代码块，然后将`+`读取为一元加运算符，`[]`为操作数。一元加号运算符将其操作数转换为数字。在这种情况下，`[]`转换为`0`。

> `("b" + "a" + + "a" + "a").toLowerCase() = "banana”`

什么鬼东西？

开玩笑的。我可以解释这个。

这是一元加号运算符的另一种情况。JavaScript 正在对`"b"`、`"a"`、`"NaN"`和`"a"`进行字符串串联，因为`+ "a" = NaN`。`"a"`到数字的隐式类型转换的结果是`NaN`，它代表“不是一个数字”，实际上是一个数字。

```
console.log(typeof(NaN))
// Output: "number"
```

## 这一切意味着什么？

表示是时候切换到[打字稿](https://www.typescriptlang.org/)了。

感谢您的阅读！在 Medium ( [Charlie Levine](https://medium.com/u/6da6b651e31a?source=post_page-----ec4ca3a84608--------------------------------) )上关注我，了解我的日常编程和技术相关文章。