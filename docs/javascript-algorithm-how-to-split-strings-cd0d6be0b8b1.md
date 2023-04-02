# JavaScript 算法:如何拆分字符串

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-how-to-split-strings-cd0d6be0b8b1?source=collection_archive---------11----------------------->

## 将一个字符串拆分成数组中的两个字符。

![](img/0b5da1e15398239eca7c0c9eae0da919.png)

Photo by [Tania Melnyczuk](https://unsplash.com/@alphabetania?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`solution`的函数，它接受一个字符串`str`作为参数。

给你一个包含 x 个字符的字符串。该函数的目标是将字符串分成两个字符对，并返回数组。如果字符串包含奇数个字符，那么它应该用下划线`_`替换最后一对字符中缺失的第二个字符。

如果字符串为空或类似于`undefined`的 falsy 值，则返回一个空数组。

示例:

```
solution("abcdef") 
// output: ["ab", "cd", "ef"]solution("abcdefg")
// output: ["ab", "cd", "ef", "g_"]solution("")
// output: []
```

在第一个示例中，字符串包含偶数个字符，因此被分成两个字符对。

对于第二个示例，字符串包含奇数个字符，因此当字符串被分成两对时，最后一对包含一个下划线以完成该对。

第三个示例包含一个空字符串，因此该函数将返回一个空数组。

为了开始这个函数，我们创建一个名为`newStr`的变量，并分配一个空字符串:

```
let newStr = "";
```

当我们遇到一个有奇数个字符的字符串时，我们会在字符串后面加一个下划线。结果将被分配给`newStr`。

接下来，我们创建一个 if 语句来检查字符串是否包含真值。如果`str`最终是一个 falsy，我们将默认结束函数并返回一个空数组。

```
if(str.length){
    //stuff here
}else{
    return [];
}
```

在第一个 if 语句中，函数将检查字符串是否有奇数个字符。如果是这样，如上所述，我们将在`str`上连接一个下划线，并将新字符串赋给`newStr`。

```
if (str.length % 2 === 1) {
    newStr = str + '_';
}
```

我们在这个模块中要做的最后一件事是使用字符串方法`match()`将我们的字符串分成两个一组。`match()`方法检索字符串与正则表达式匹配的结果。

我们将使用正则表达式将字符串分成两部分:

```
/.{2}/g
```

在正则表达式中，量词(花括号中的数字)一次匹配一个字符串中的两个字符。

`match()`方法返回一个数组，所以我们所要做的就是将它与`newStr`变量一起使用，并返回匹配的数组。

```
return newStr.match(/.{2}/g)
```

在 if 语句的`else`块中，我们将返回在`str`输入中找到的匹配。该字符串已经有偶数个字符，所以这里没有什么可改变的。

```
return str.match(/.{2}/g)
```

仅此而已。下面是完整的函数:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-find-the-parity-outlier-666e350883ec) [## JavaScript 算法:寻找奇偶异常值

### 找出奇数(或偶数)

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-find-the-parity-outlier-666e350883ec) [](/javascript-algorithm-simple-pig-latin-f4138eb91b69) [## JavaScript 算法:简单的猪拉丁

### 将字符串翻译成拉丁文

javascript.plainenglish.io](/javascript-algorithm-simple-pig-latin-f4138eb91b69) [](/javascript-algorithm-convert-string-characters-into-ascii-bb53ae928331) [## JavaScript 算法:将字符串转换成 ASCII

### 创建一个函数，该函数将返回一个包含字符串中每个字符的 ASCII 码的数组。

javascript.plainenglish.io](/javascript-algorithm-convert-string-characters-into-ascii-bb53ae928331) 

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*