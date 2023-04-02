# JavaScript 算法:简单的猪拉丁

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-simple-pig-latin-f4138eb91b69?source=collection_archive---------2----------------------->

## 将字符串翻译成拉丁文

![](img/4a30a564cac4bd87887a7dfa8f3801e8.png)

Photo by [Kenneth Schipper Vera](https://unsplash.com/@kennethsv?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`pigIt`的函数，它将接受一个字符串`str`作为参数。

给你一个字符串，函数的目标是把字符串翻译成拉丁文。要翻译字符串，请执行以下操作:

1.  将单词的第一个字母移到单词的末尾。
2.  在单词的末尾加上“ay”。

就是这样。如果这个单词只有一个字母，跳过第一步，只在末尾加一个“ay”。如果字符串是标点符号或数字，请保持原样。保持单词的大小写不变。

示例:

```
pigIt('Pig latin is cool'); \\ *igPay atinlay siay oolcay* pigIt('Hello world !'); \\ *elloHay orldway !*
```

首先，我们将把字符串分成一个数组，每个单词都是它自己的数组元素。我们将该数组分配给`strArr`。

```
let strArr = str.split(' ');
```

接下来，我们将创建一个名为`pigLatin`的空数组。这是我们将每个单词翻译成 Pig Latin 后追加到的数组。

```
let pigLatin = [];
```

接下来，我们将使用`for…of`循环遍历`strArr`数组。

```
for (let word of strArr) {
    if ((/([a-zA-Z])/).test(word)) {
        pigLatin.push(word.substring(1) + word[0] + "ay");
    } else {
        pigLatin.push(word);
    }
}
```

在循环的第一行，我们使用正则表达式和`test()`方法来检查当前元素是否以字母字符开始。如果方法返回`false`，那意味着这个字符要么是一个标点符号，要么是一个数字。我们想不去管它，直接把它附加到`pigLatin`数组中。

如果方法返回`true`，那就是我们把字符串翻译成 Pig Latin 的时候。

```
word.substring(1) + word[0] + "ay"
```

我们首先使用`substring()`方法从第二个字符开始提取字符串中的所有字符。这就省略了字符串的第一个字母。

然后我们将字符串的第一个字符连接到末尾，然后在其后添加`“ay”`。

我们将翻译后的字符串添加到`pigLatin`数组中。

最后，在将数组转换回字符串后，我们返回`pigLatin`数组。

```
return pigLatin.join(" ");
```

下面是完整的函数:

如果你觉得这个算法有帮助，看看我的其他 JavaScript 算法解决方案:

[](/javascript-algorithm-merge-two-arrays-e88e002e1554) [## JavaScript 算法:合并两个数组

### 用 JavaScript 编写合并两个数组的两种方法

javascript.plainenglish.io](/javascript-algorithm-merge-two-arrays-e88e002e1554) [](https://levelup.gitconnected.com/javascript-algorithm-unique-in-order-bba51ffbb1f5) [## JavaScript 算法:顺序唯一

### 返回唯一的项目列表，而不改变元素的原始顺序

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-unique-in-order-bba51ffbb1f5) [](https://levelup.gitconnected.com/javascript-algorithm-seek-and-destroy-36888783f35f) [## JavaScript 算法:寻找和破坏

### 我们编写了一个函数，它将从一个数组中删除与所提供的参数具有相同值的所有元素。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-seek-and-destroy-36888783f35f) 

*更多内容看* [***说白了. io***](http://plainenglish.io)