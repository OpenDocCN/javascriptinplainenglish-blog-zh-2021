# JavaScript 算法:将小时转换为秒

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-convert-hours-into-seconds-c2252ad3c171?source=collection_archive---------7----------------------->

## 将小时转换为秒的函数。

![](img/3beac0ab39f998c69027ac025af982f4.png)

Photo by [Fabrizio Verrecchia](https://unsplash.com/@fabrizioverrecchia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

今天，我们将编写一个名为`howManySeconds`的函数，它接受一个整数`hours`作为参数。

该函数的目标是输出给定小时数内的秒数。让我们看一个例子。

示例:

```
howManySeconds(2) ➞ 7200
```

在上面的例子中，你被给予`2`作为小时数。要将其转换为秒，您首先必须找到一小时中有多少分钟，然后计算这些分钟中有多少秒。一旦你得到给定小时内的秒数，函数就会输出结果。回到我们的例子，在`2`小时内有`7200`秒。

让我们把它变成代码。

首先，我们创建一个名为`seconds`的变量。这将是函数返回的变量。

你知道一小时有 60 分钟，一分钟有 60 秒。我们要做的是将`hours`乘以`60`，然后得到答案，再乘以`60`。然后我们可以返回`seconds`变量。

```
let seconds = (hours * 60) * 60;
return seconds;
```

另一种方法是去掉括号，将`60 * 60`乘以`3600`，然后写出`hours * 3600`。

```
let seconds = hours * 3600;
return seconds;
```

就这样。以下是完整的功能:

如果您认为这个算法有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://medium.com/javascript-in-plain-english/javascript-algorithm-convert-html-entities-99719d8ca118) [## JavaScript 算法:转换 HTML 实体

### 编写一个函数，将选定数量的字符转换成相应的 HTML 实体。

medium.com](https://medium.com/javascript-in-plain-english/javascript-algorithm-convert-html-entities-99719d8ca118) [](https://levelup.gitconnected.com/javascript-algorithm-search-and-replace-6895e17ccfd7) [## JavaScript 算法:搜索和替换

### 我们编写了一个函数，它将对字符串执行简单的搜索和替换操作。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-search-and-replace-6895e17ccfd7) [](https://codeburst.io/javascript-algorithm-chunky-monkey-337991491b24) [## JavaScript 算法:矮胖的猴子

### 我们编写了一个函数，通过将一维数组分解为子数组组来创建二维数组…

codeburst.io](https://codeburst.io/javascript-algorithm-chunky-monkey-337991491b24)