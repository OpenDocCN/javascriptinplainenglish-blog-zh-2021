# JavaScript 中++x 和 x++有什么区别？

> 原文：<https://javascript.plainenglish.io/whats-the-difference-between-x-and-x-in-javascript-d7c8e52ae937?source=collection_archive---------4----------------------->

![](img/67fe9ba0d6fe3ae74042c7c7d135c293.png)

Photo by [Waren Brasse](https://unsplash.com/@wawa01?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，我们可以用两种方式增加数值变量的值。

我们可以把++放在变量的前面或后面。

他们看起来相似，但他们是不同的。

在本文中，我们将看看 JavaScript 中的`++x`和`x++`之间的区别。

`++x`和`x++`的区别在于`++x`增加变量并返回`x`的新值作为值。

例如，如果我们写:

```
let x = 1
console.log(++x)
console.log(x)
```

然后我们看到两个控制台日志 log 2。

另一方面，`x++`增加变量，但是它不返回新的值`x`作为值。

例如，如果我们有:

```
let x = 1
console.log(x++)
console.log(x)
```

然后我们看到第一个控制台日志记录 1，第二个控制台日志记录 2。

# 结论

尽管`++x`和`x++`看起来相似，但它们是不同的。

`++x`增加变量并返回`x`的新值作为值。

而`x++`增加变量，但不返回`x`的新值作为值。

*更多内容看* [***说白了. io***](http://plainenglish.io)