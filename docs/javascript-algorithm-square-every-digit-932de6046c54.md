# JavaScript 算法:平方每个数字

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-square-every-digit-932de6046c54?source=collection_archive---------7----------------------->

## 将一个数字的每一个数字平方，然后连接起来

![](img/a6f1f18764b6c3a94946dc10763e2560.png)

Photo by [Bernard Hermant](https://unsplash.com/@bernardhermant?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`squareDigits`的函数，它接受一个整数`num`作为参数。

给你一个整数。该函数的目标是从该数字中取出每个数字，并对其求平方。对每个数字求平方后，将这些数字连接起来，并将整个值作为一个整数返回。

示例:

```
9119
// output: 811181
```

在上面的例子中，我们首先平方每个数字:

```
9^2 = 81
1^2 = 1
1^2 = 1
9^2 = 81
```

在我们对每个数字求平方后，我们将结果连接在一起。这给了我们`811181`。

我们要做的第一件事是将数字转换成字符串。这将允许我们将`num`分割成单独的字符或数字。我们将字符串赋给一个名为`numStr`的变量。

```
let numStr = num + "";
```

我们创建另一个名为`total`的变量。这个变量将包含我们串联平方数字后的数字。这个变量将是一个字符串，因为你不能连接一个数字(你最终会把它们加在一起)。

```
let total = "";
```

接下来，我们将循环通过`numStr`:

```
for(let i in numStr){    
    total += (parseInt(numStr[i])**2 + "");  
}
```

从括号内的内容开始，我们使用`parseInt()`将每个数字转换成一个整数。然后我们把它平方。

```
parseInt(numStr[i])**2
```

然后，我们通过将数字连接到一个空字符串，将它转换回字符串。

```
parseInt(numStr[i])**2 + ""
```

我们将该语句放在括号中，让 JavaScript 知道我们想要将平方数字连接到`total`。

```
total += (parseInt(numStr[i])**2 + "");
```

在我们循环完我们号码的所有数字后，我们返回`total`。在这之前，我们先把它转换成一个整数。

```
return parseInt(total);
```

仅此而已。下面是完整的函数:

如果您觉得这个算法有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-simple-string-reversal-df44d83c9a5a) [## JavaScript 算法:简单的字符串反转

### 反转两个给定索引之间的字符串部分

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-simple-string-reversal-df44d83c9a5a) [](/javascript-algorithm-word-count-d759738c974c) [## JavaScript 算法:字数

### 创建一个函数，返回文本中的字数。

javascript.plainenglish.io](/javascript-algorithm-word-count-d759738c974c) [](/javascript-algorithm-less-than-100-9bdff6d4d6a9) [## JavaScript 算法:100 以内？

### 写一个函数，检查两个数之和是否小于 100。

javascript.plainenglish.io](/javascript-algorithm-less-than-100-9bdff6d4d6a9) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)