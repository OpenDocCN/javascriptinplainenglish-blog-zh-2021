# 如何在 JavaScript 中从二进制转换成文本

> 原文：<https://javascript.plainenglish.io/how-to-convert-from-binary-to-text-in-javascript-3e881c7fd8c7?source=collection_archive---------2----------------------->

## 让我们使用 JavaScript 将二进制转换成文本

![](img/7ad9af476dfc2d25d4918d191c6de94f.png)

Photo by H[eylagostechie](https://unsplash.com/@heylagostechie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

像任何其他编程语言一样，JavaScript 允许您将二进制代码转换为人类可以理解的普通文本。这是一个小问题，您可以使用 JavaScript 的力量来解决。因为有些情况下你需要将二进制转换成文本。

在本文中，我们将使用一些 JavaScript 技术将二进制转换成文本。所以让我们开始吧。

# 问题解释

问题很明显。我们有一个字符串形式的二进制代码，我们需要把它翻译成单词。

我解决这个问题的方法是首先将二进制转换成十进制，然后将十进制值转换成字符(文本)。

这就是我们的方法，因为没有办法直接从二进制转换成文本。

# 解决问题

我们有一个名为`binaryToText`的函数，它带有一个名为`binary`的参数(我们传递给函数的二进制代码)。我们将把二进制字符串作为参数传递给这个函数。

这里有一个例子:

```
function **binaryToText**(binary) {
 //Your code here.}binaryToText("01001011 0011010 0011100");
```

正如我所说，我们首先需要从二进制转换成十进制。为此，我们首先必须使用`split()`方法将二进制字符串转换成一个数组。

我们将使用`split(‘ ‘)`并向它传递一个空白字符串，以便得到一个由空白分隔的字符串数组。

这里有一个例子:

```
function binaryToText(binary) {
 //Convert the binary into an array of binary strings separated by whitespace.
 **binary = binary.split(' ');**}
```

现在我们需要使用 map 方法来遍历数组`binary`的所有二进制字符串。我们将获取数组`binary`中的每个二进制元素，并使用方法`parseInt()`将其转换为小数。

因此，为了转换成小数，我们使用方法`parseInt()`，我们将二进制元素作为第一个参数传递给它，将数字 2 作为第二个参数传递给它。

然后我们还会用`[String.fromCharCode()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode)`的方法把小数转换成字符(文本)。

请看下面的完整示例:

```
function binaryToText(binary) {
//Convert the binary into an array of binary strings separated by whitespace.
 **binary = binary.split(' ');**//convert from binary to decimals, then to characters. 
**return** binary.**map**(elem => **String.fromCharCode**(**parseInt(elem, 2)**)).join("");
}binaryToText**("**01001001 00100000 01101100 01101111 01110110 01100101 00100000 01001010 01100001 01110110 01100001 01010011 01100011 01110010 01101001 01110000 01110100"**);** //returns I love JavaScriptbinaryToText**("**01010100 01101000 01100001 01110100 00100111 01110011 00100000 01100111 01101111 01101111 01100100"**);** //returns That's good
```

结果，我们得到一个字符数组，因为 map 方法返回一个新的数组。

我们使用方法`join("")`将字符数组转换成一个字符串(句子)。

就这样，现在你可以把任何二进制代码作为字符串传递给上面的函数，它会把它转换成文本。

# 结论

如你所见，这是我解决这个问题的方法。如果你知道其他更好的解决方法，请告诉我。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/6-underrated-html-tags-that-you-probably-dont-know-9997525bad69) [## 你可能不知道的 6 个被低估的 HTML 标签

### 没人谈论的不受欢迎的 HTML 标签。

javascript.plainenglish.io](/6-underrated-html-tags-that-you-probably-dont-know-9997525bad69) 

*更多内容看*[***plain English . io***](https://plainenglish.io/)