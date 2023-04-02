# JavaScript 中的数字分隔符是什么？

> 原文：<https://javascript.plainenglish.io/what-are-numeric-separators-in-javascript-d83b1a393318?source=collection_archive---------18----------------------->

![](img/e0a72e26760123514de7938d19147079.png)

作为开发人员，编写高性能代码是不够的。我们需要确保它也是可读的。语言中的 API 变化很少会带来可读性。数字分隔符就是这样一种罕见的变化。

# 为什么是数字分隔符？

阅读这篇文章需要几秒钟:

```
const number = 100000000;
```

数零的数量是没人想做的事情。这需要一定的脑力，但是直到现在也没有其他的写作方法。有了数字分隔符，我们现在可以使用下划线来分隔数字文字。

# 怎么会？

```
const number = 100_000_000;
```

分隔符的规则非常明显。数字不能以下划线开头或结尾，并且文本中不能有两个连续的下划线。

此外，它也可以应用于二进制，八进制和十六进制数！

```
const binary = 0b1_0000; // 16 const octal = 0o1_0_0_1; // 513 const hex = 0xA_B_C_0_0; // 703488
```

它也得到了广泛的支持。IE 是唯一不支持的浏览器。你可以在这里看到完整的列表[。](https://caniuse.com/mdn-javascript_grammar_numeric_separators)

让我们去，让我们的数字更容易阅读！

*原载于 2021 年 6 月 17 日*[*【https://www.wisdomgeek.com】*](https://www.wisdomgeek.com/development/web-development/javascript/numeric-separators-in-javascript/)*。*

*更多内容请看**[***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****