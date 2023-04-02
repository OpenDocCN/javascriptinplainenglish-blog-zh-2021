# JavaScript 中断和继续语句

> 原文：<https://javascript.plainenglish.io/javascript-break-and-continue-statements-661d645a537d?source=collection_archive---------19----------------------->

![](img/1e93f0e8ec8eaba5f4c9deab78558deb.png)

Photo by [Joshua Aragon](https://unsplash.com/@goshua13?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

使用 JavaScript 已经有一段时间了，有时您会发现当满足某个条件时需要中断循环，或者因为这样或那样的原因从当前迭代跳到下一个迭代。这些情况可以通过使用以下语句来解决:

1.  break 语句
2.  连续语句

这些语句对于代码中的某些逻辑非常有用，尤其是在想要避免长时间中断循环或跳过迭代时。让我们看看如何使用它们。

# break 语句

`break`语句用于终止循环并退出循环。然后，接下来将执行循环代码块之后的代码(如果有)。它通常用在条件语句中，当条件满足时，由于某种原因，它会停止循环并退出。如何做是通过简单地写`break`。

语法:

```
break;
```

示例:

```
for (let i = 0; i < 8; i++) {
    if (i === 4) { break; }
    console.log("Iteration i: " + i);
}// Output:
Iteration i: 0
Iteration i: 1
Iteration i: 2
Iteration i: 3
```

如果没有`break`语句，输出通常如下所示:

```
// Output:
Iteration i: 0
Iteration i: 1
Iteration i: 2
Iteration i: 3
Iteration i: 4
Iteration i: 5
Iteration i: 6
Iteration i: 7
```

因此，概括一下，基于上面的例子，我们可以看到，当条件满足时，运行`break`语句，结果，它立即终止循环。

这个语句也可以用在类似条件语句的`switch`语句中。然而，对于本文，我们将只看一下循环的使用。

# 连续语句

`continue`语句用于跳过循环的迭代。这个语句也一样，可以用在`switch`语句中。

`continue`语句主要是在满足特定条件的情况下中断循环的一次迭代，并继续循环的下一次迭代。怎么写的和`break`语句差不多。

语法:

```
continue;
```

示例:

```
for (let i = 0; i < 8; i++) {
    if (i === 4) { continue; }
    console.log("Iteration i: " + i);
}// Output:
Iteration i: 0
Iteration i: 1
Iteration i: 2
Iteration i: 3
Iteration i: 5
Iteration i: 6
Iteration i: 7
```

使用上面的例子，我们可以看到迭代 4 被跳过了，因为我们写了当它是 4 时，我们将继续下一次迭代。因此，它的回合被跳过而不被打印出来。

## 结论

这两个说法暂时就这么多了。它们只是在您的代码中可能经常使用的有用基础。

希望这篇文章对你有帮助。如果你认为这篇文章是有帮助的，并且可以帮助其他人，请分享给他们阅读。也欢迎你的想法和评论！

感谢阅读~

*阅读更多尽在*[***plain English . io***](https://plainenglish.io/)