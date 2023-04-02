# JavaScript 算法:我的数字在这里看起来很大吗？

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-does-my-number-look-big-in-this-744d6f032c1e?source=collection_archive---------10----------------------->

## 确定给定整数是否为自恋数的函数

![](img/4ef8ed7bd7d72d5c164fb0b6904d741b.png)

Photo by [Marija Zaric](https://unsplash.com/@simplicity?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`narcissistic`的函数，它将接受一个整数`value`作为参数。

该函数的目标是确定给定的整数是否是一个自恋数。自恋数字是一个正数，它是它自己的数字的和，每个数字的幂都是给定基数的数字的幂。

示例:

```
153
1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 1531652
1^4 + 6^4 + 5^4 + 2^4 = 1 + 1296 + 625 + 16 = 1938
```

第一个数字，`153`，是自恋。因为这个数字有 3 个数字，所以每个数字都是 3 的乘方。将所有的数字进行立方求和后，总和等于`153`，即原始值。

第二个数字，`1652`，并不自恋。由于该数字有 4 个数字，所有数字的 4 次方之和不等于`1652`。

如果数字自恋，函数会返回`true`。如果没有，`false`。

创建函数时，我们首先创建三个变量:

```
let numStr = value + "";
let power = numStr.length;
let count = 0;
```

`numStr`将包含整数的字符串版本。我们这样做是为了遍历数字中的所有数字。

`power`将包含数字的幂或数字的长度。

`count`将包含我们将每个数字提升到 n 次方并将它们相加后的总和。

接下来，我们遍历`numStr`中的各个数字:

```
for (let num of numStr) {
    count += parseInt(num) ** power;
}
```

在循环内部，我们将每个数字转换成一个整数，这样我们就可以计算该数字的 n 次方，并将其加到`count`。

```
count += parseInt(num)**power;
```

循环完成后，我们返回布尔语句。如果`count`等于`value`(自恋)，如果不等于，函数将返回`true`和`false`。

```
return count == value;
```

就是这样。下面是该函数的其余部分:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-find-the-odd-int-4410a7e7f0a3) [## JavaScript 算法:寻找奇数整数

### 给定一个整数数组，找出出现奇数次的整数

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-find-the-odd-int-4410a7e7f0a3) [](/javascript-algorithm-simple-pig-latin-f4138eb91b69) [## JavaScript 算法:简单的猪拉丁

### 将字符串翻译成拉丁文

javascript.plainenglish.io](/javascript-algorithm-simple-pig-latin-f4138eb91b69) [](https://levelup.gitconnected.com/javascript-algorithm-unique-in-order-bba51ffbb1f5) [## JavaScript 算法:顺序唯一

### 返回唯一的项目列表，而不改变元素的原始顺序

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-unique-in-order-bba51ffbb1f5) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)