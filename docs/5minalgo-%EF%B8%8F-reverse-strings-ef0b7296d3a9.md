# 3minAlgo⚡️:反向弦

> 原文：<https://javascript.plainenglish.io/5minalgo-%EF%B8%8F-reverse-strings-ef0b7296d3a9?source=collection_archive---------12----------------------->

![](img/ac889b2f28680a9774e33e9d23339a47.png)

Photo by [Clark Van Der Beken](https://unsplash.com/@snaps_by_clark?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/maze?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 解决反向字符串算法问题的四(4)种替代方法

下面是你的任务:给定一个字符串，返回一个字符顺序相反的新字符串。

```
*Example:* *reverse(‘cooper’) === ‘repooc’
  reverse(‘birthday’) === ‘yadhtrib’
  reverse(‘Hello!’) === ‘!olleH’*
```

🔹注意，**给定的** **输入**和**期望输出**都是**的** **字符串**。

## ✏️描绘出了这个过程

1.  将字符串转换成数组
2.  在数组上调用 reverse
3.  加入数组后面的介绍字符串
4.  返回结果！

## 解决方案 1

```
function reverse(str) {           // ex. "apple"
   let array = str.split('');     // array=["a", "p", "p", "l", "e"]
       array.reverse();           // array=["e", "l", "p", "p", "a"]
   return array.join('');         // => "elppa"
}
```

解决方案#1 可行，但是我们可以跳过创建数组，直接将方法应用到 str 本身:

## 解决方案 2

```
function reverse(str) {
   *return str
     .split('')
     .reverse()
     .join('');
}*
```

看起来更干净，对吗？它可以写在一行中——我只是为了可读性而把它分解了。

🔹🔹如果你的面试官说**你不允许使用相反的**方法怎么办？？**🚫**

*我们换个方式试试:*

1.  设置 for 循环
2.  抓取并将每个元素推到空字符串的前面。(不要忘记先创建一个空字符串！)
3.  返回反转的字符串。

## 解决方案 3。使用“for…of”

```
function reverse(str) { let reversedStr = '';
  *  for (let character of str) {
      reversedStr = character + reversedStr;
    }
 return reversedStr;
}*
```

我真的很喜欢这个解决方案，因为它既可读又高效。然而，使用强大的**还有另一种解决方案。减少**的方法。这个问题实际上花了我更长的时间来消化，因为我不得不在网上再次复习语法。我知道。reduce 对处理数字很有帮助，但如果使用正确，它对处理字符串也很有用。

## 解决方案 4。使用。减少()⚡️

```
function reverse(str) { return str
     .split('')
     .reduce((previousValue, currentValue) => 
        currentValue + previousValue, '')}
```

请随意在您的 VSCodes 上运行代码并使用它们。如果您有任何问题和/或您提出了更多替代解决方案，请告诉我！！👋🏻