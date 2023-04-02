# JavaScript 算法:检测 Pangram

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-detect-pangram-9d57ca713d0d?source=collection_archive---------3----------------------->

## 一个程序，如果一个字符串是一个盘符，返回 true，否则返回 false

![](img/4bdd042e81f29614a73ad3f04e72e8a4.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`isPangram`的函数，它接受一个名为`string`的字符串作为参数。

在这个函数中，给你一个字符串，函数的目标是如果这个字符串是一个 pangram 就输出`true`，如果不是就输出`false`。盘符是一个包含字母表中每个字母至少一次的句子。

示例:

```
"The quick brown fox jumps over the lazy dog." // true
"This is not a pangram." // false
```

我们要做的第一件事是小写我们的字符串，并把它放在一个名为`strArr`的变量中。如果所有的字母都是小写的，检查字符串中的所有字母会更容易。

```
let strArr = string.toLowerCase();
let alphabet = 'abcdefghijklmnopqrstuvwxyz'.split('');
```

接下来，我们创建另一个名为`alphabet`的变量，它将保存一个包含英文字母的数组。

我们创建一个 for 循环和循环 through`alphabet`。

```
for (let i = 0; i < alphabet.length; i++) {
    if (strArr.indexOf(alphabet[i]) < 0) {
        return false;
    }
}
```

当我们在`alphabet`数组中循环时，如果在`strArr`中没有找到某个字符(`indexOf`方法返回`-1`)，循环将结束，函数将返回`false`。

如果循环设法到达末尾，这意味着字母表中的每个字符都在字符串中找到。此时，该函数将返回`true`。

```
return true;
```

就是这样。下面是该函数的其余部分:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-complementary-dna-3ad421071110) [## JavaScript 算法:互补 DNA

### 输出 DNA 序列中每个碱基的碱基对

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-complementary-dna-3ad421071110) [](/javascript-algorithm-does-my-number-look-big-in-this-744d6f032c1e) [## JavaScript 算法:我的数字在这里看起来很大吗？

### 确定给定整数是否为自恋数的函数

javascript.plainenglish.io](/javascript-algorithm-does-my-number-look-big-in-this-744d6f032c1e) [](https://levelup.gitconnected.com/javascript-algorithm-find-the-odd-int-4410a7e7f0a3) [## JavaScript 算法:寻找奇数整数

### 给定一个整数数组，找出出现奇数次的整数

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-find-the-odd-int-4410a7e7f0a3) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)