# JavaScript 亮点——数组循环和字符串

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-array-loops-and-strings-f81f539299f?source=collection_archive---------14----------------------->

![](img/bbbd301af1d8fddabb2403c1984e14de.png)

Photo by [Eddie Tsy](https://unsplash.com/@eddietsy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 遍历一个数组

我们可以通过使用数组的`length`属性作为结束条件来循环遍历数组。

例如，我们可以写:

```
let matchFound = false;
for (let i = 0; i < cleanestCities.length; i++) {
  if (city === cleanestCities[i]) {
    matchFound = true;
    console.log("It's one of the cleanest cities");
  }
}
```

我们得到结束条件的`cleanestCities`数组的`length`属性。

我们从 0 到`cleanestCities.length — 1`循环。这样，我们从开始到结束循环通过项目，而不用为结束条件设置比较固定数值。

如果我们想提前停止一个循环，我们可以使用`break`关键字。

例如，我们可以写:

```
for (let i = 0; i < cleanestCities.length; i++) {
  if (city === cleanestCities[i]) {
    console.log("It's one of the cleanest cities");
    break;
  }
}
```

如果`city`等于`clesnestCities[i]`，那么我们用`break`结束循环。

我们可以在代码中嵌套循环。例如，我们可以写:

```
let firstNames = ['james', 'mary', 'alex'];
let lastNames = ['jones', 'wong', 'green'];
let fullNames = [];
for (let i = 0; i < firstNames.length; i++) {
  for (let j = 0; j < lastNames.length; j++) {
    fullNames.push(`${firstNames[i]} ${ lastNames[j]}`);
  }
}
```

我们在另一个`for`循环中有一个`for`循环。

外部循环遍历`firstNames`数组。

在每次迭代中，运行内部循环来遍历`lastNames`数组。

在内部循环中，我们将`firstNames[i]`和`lastNames[j]`的组合推入`fullNames`数组。

结果是将`firstNames`和`lastNames`条目的所有组合添加到`fullNames`数组中。

我们可以有尽可能多的嵌套层次。然而，嵌套越多，代码就越难阅读。

# 改变大小写

我们可以用`toUpperCase`和`toLowerCase`方法改变字符串的大小写。

将一个字符串的字母全部改为大写。

而`toLowerCase`将一个字符串的字母全部改为小写。

例如，我们可以写:

```
"Santa Fe".toLowerCase()
```

然后我们得到:

```
"santa fe"
```

已退回。

如果我们写下:

```
"Santa Fe".toUpperCase()
```

我们得到了:

```
"SANTA FE"
```

# 字符串长度和部分

我们可以用`length`属性得到一个字符串的字符数。

例如，我们可以写:

```
"Santa Fe".length
```

已经有 8 个回来了。

要获得字符串的各个部分，我们可以使用`slice`方法。

它获取我们想要提取的开始和结束索引。

结束索引本身被排除在外。

例如，如果我们写:

```
"Santa Fe".slice(2, 4)
```

然后我们有`“nt”`返回。

# 查找字符串段

我们可以用`indexOf`方法找到字符串段。如果字符串在我们调用`indexOf`的字符串中，它将返回我们作为参数传入的字符串的起始索引。

例如，我们可以写:

```
"Santa Fe".indexOf('Fe')
```

则返回 6，因为“F”字符在索引 6 中。

# 结论

数组中可以有嵌套循环。此外，我们可以用 JavaScript 字符串方法找到字符串段并获得长度。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**