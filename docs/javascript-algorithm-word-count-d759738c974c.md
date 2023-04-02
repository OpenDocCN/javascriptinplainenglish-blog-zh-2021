# JavaScript 算法:字数

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-word-count-d759738c974c?source=collection_archive---------4----------------------->

## 创建一个函数，返回文本中的字数。

![](img/e0132801eee04b2fe2c4aef4bec853e5.png)

Photo by [Siora Photography](https://unsplash.com/@siora18?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`countWords`的函数，它将接受一个字符串`text`作为参数。

该函数的目标是返回该文本字符串中有多少个单词。

示例:

```
countWords("JavaScript!!!    ");
// output: 1countWords("I had 3 slices of bread");
// output: 6countWords("    JavaScript is cool   Core   ");
// output: 4countWords("I like to learn JavaScript with codeguppy");
// output: 7
```

该函数应该忽略任何非字母数字字符作为字数的一部分。包含连字符的单词也应算作一个单词。

我们做的第一件事是创建一个名为`removeChar`的变量。在这个变量中，我们删除了文本和标点符号中多余的空格。为此，我们结合使用正则表达式和`replace()`方法。

```
let removeChar = text.replace(/[^A-Za-z]\s+/g, " ");
```

`replace()`方法中的正则表达式`/[^A-Za-z]\s+/g`接受所有非字母数字字符，并用单个空格替换它们。详细地说:

`/[regular expression]/g`:不再停留在第一个匹配上，而是在文本中寻找所有可能的匹配。

`[^A-Za-z]`:匹配任何不是 a-z 和 A-Z 的字符。

`\s`:匹配空白字符。

`+`:匹配一个或多个前面的标记(在上面的例子中是空格)。

去掉所有这些字符后，统计`text`中的单词数就更容易了。

接下来我们要做的是创建一个名为`newWord`的新变量，并将修改后的文本分割成一个单词数组。

```
let newWord = removeChar.trim().split(" ");
```

在最后一个语句中，我们用一个空格替换所有非字母数字字符的原因是，如果我们不替换它，像`"I eat bread"`这样的文本输入将变成`"Ieatbread"`。我们还用一个空格来替换它，以便于在数组中将数组拆分成单独的单词。

`trim()`方法是删除字符串两端的任何空格。对于任何可能在字符串开头或结尾有任何非字母数字字符的文本，`replace()`方法将用空格替换这些字符。当我们分割数组时，我们不希望额外的空白被添加到数组中，所以在这种情况下，我们将它修剪掉。

现在我们的数组包含了字符串中所有可数的单词，我们只需要数组的长度，因为它也是字符串的字数。

我们返回数组长度。

```
return newWord.length;
```

下面是完整的函数:

如果你觉得这个算法有帮助，看看我的其他 JavaScript 算法解决方案:

[](https://levelup.gitconnected.com/javascript-algorithm-set-alarm-54a7abd094d7) [## JavaScript 算法:设置警报

### 我们将编写一个函数，它将根据你是否有工作来决定是否值得设置闹钟，并且…

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-set-alarm-54a7abd094d7) [](https://levelup.gitconnected.com/javascript-algorithm-seek-and-destroy-36888783f35f) [## JavaScript 算法:寻找和破坏

### 我们编写了一个函数，它将从一个数组中删除与所提供的参数具有相同值的所有元素。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-seek-and-destroy-36888783f35f) [](https://js.plainenglish.io/javascript-algorithm-zero-fuel-7e73be4fe91d) [## JavaScript 算法:零燃料

### 我们写了一个函数，它将决定你减少的燃料量是否足以让你到达最近的加油站…

js .平原英语. io](https://js.plainenglish.io/javascript-algorithm-zero-fuel-7e73be4fe91d) 

*查看更多内容请点击*[***plain English . io***](https://plainenglish.io/)