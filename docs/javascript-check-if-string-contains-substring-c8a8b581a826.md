# JavaScript:检查字符串是否包含子字符串

> 原文：<https://javascript.plainenglish.io/javascript-check-if-string-contains-substring-c8a8b581a826?source=collection_archive---------2----------------------->

可能有一段时间，当你搜索字符串这样的功能。包含()。好吧，JavaScript 里没有这个特性。因此，实现这一目标的最佳方式是什么？

![](img/b5f2244e3443168d089a3dacb16d0f8c.png)

# EcmaScript-6

如果您使用的是最新版本的 JavaScript，对于开发来说，您可以在字符串原型中自由使用 **includes** 函数。

**ECMAScript 6 推出**

```
const string = "foo";
const substring = "oo";

console.log(string.includes(substring)); // true
```

includes 在字符串上执行**区分大小写的**搜索。

作为开发人员，您需要注意 includes 何时被使用。旧的浏览器，尤其是 Internet Explorer 不支持 String.prototype.includes。这意味着，您必须在代码中有一个回退机制来处理这些环境。

# EcmaScript-5

indexOf 可用于判断字符串是否包含子串。如果子字符串不在字符串中，indexOf 方法将返回-1。它经常在数组中使用，同样的情况也适用于字符串。

```
var string = "foo";
var substring = "oo";

console.log(string.indexOf(substring) !== -1); // true
```

indexOf 对字符串进行区分大小写的搜索。

# 时间复杂度

无论使用 includes 还是 indexOf，这两种简单算法的时间复杂度都是 O(m * n)，其中 m 是父字符串的长度，n 是子字符串的长度。

如果你的目标是一个时间复杂度更低的解决方案，你需要使用不同的算法。

# Knuth-Morris-Pratt 算法别名 KMP 算法

首先，KMP 算法的时间复杂度为 O(m+n)。这要快得多，也比幼稚的好得多。

KMP 算法采用线性方法来检查子串是否存在于字符串中。这是我的 KMP 算法版本。

```
function kmpSearch(pattern, text) {
  if (pattern.length == 0)
    return 0; // Immediate match
  var j = 0; // Number of chars matched in pattern
  for (var i = 0; i < text.length; i++) {
    if (text.charAt(i) != pattern.charAt(j)){
      j = 0; // Fall back in the pattern
    }
    if (text.charAt(i) == pattern.charAt(j)) {
      j++; // Next char matched, increment position
      if (j == pattern.length)
        return i - (j - 1);
    }
  }
  return -1; // Not found
}
```

我们上面做的事情很简单。让我们一步一步地解读这个流程:

1.  如果模式是空字符串，则可以返回 true，因为。
2.  逐个字符地遍历字符串
3.  **如果文本中的当前字符不等于模式中的当前字符，将模式的指针重置到第 0 个索引**
4.  继续遍历文本
5.  **如果文本中的当前字符等于模式中的当前字符，则增加模式中当前字符的位置**
6.  **如果指针长度和模式长度匹配，返回文本中模式的起始索引**
7.  如果从未找到该模式，则返回-1

如果您正在寻找一种线性算法来检查文本中是否存在子字符串，那么 KMP 算法绝对是您的首选解决方案。

# 结论

现在，我们已经掌握了如何检查子串是否存在于字符串中。到目前为止，只有这三种传统的、最常用的方法来检查模式是否在字符串中找到。当然，KMP 算法并不局限于 JavaScript。它可以用任何编程语言实现。它是字符串模式检查的线性算法。

如果你喜欢我的话，请跟随并继续学习。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)