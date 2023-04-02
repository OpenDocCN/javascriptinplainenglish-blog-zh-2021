# JavaScript 算法:计算字符串中数字的总和

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-calculate-sum-of-numbers-in-a-string-dd007da460b7?source=collection_archive---------2----------------------->

## 计算以逗号分隔的字符串形式接收的数字总和。

![](img/7ee2762aeefaeadedfb2e73629e938eb.png)

Photo by [Ashkan Forouzani](https://unsplash.com/@ashkfor121?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`sumStr`的函数，它将接受字符串`str`作为参数。该字符串将包含由逗号分隔的整数和浮点数的组合。

该函数的目标是计算字符串中所有数字的和。

示例:

```
sumStr("1.5, 2.3, 3.1, 4, 5.5, 6, 7, 8, 9, 10.9");//output: 57.3
```

在处理字符串中的数字之前，我们将首先在逗号处分割字符串，并将其转换为数组。我们把这个数组分配给一个叫做`strArr`的变量。

```
let strArr = str.split(",");
```

接下来，我们将使用`reduce()`方法计算数组中所有数字的和。由于数字最初是字符串，我们需要使用`parseFloat()`将所有内容转换成数字。这就是为什么我们的 reducer 回调函数可以计算总和。

我们将总和分配给一个名为`sum`的变量。

```
let sum = strArr.reduce(function(*total*, *num*){
    return parseFloat(total) + parseFloat(num);
});
```

既然我们已经拿到了总数，我们就可以退回去了。

```
return sum;
```

以下是完整的功能:

如果您认为这个算法有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-convert-minutes-into-seconds-4d4a0d750b6c) [## JavaScript 算法:将分钟转换为秒

### 一个关于如何将分钟转换成秒的简短函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-convert-minutes-into-seconds-4d4a0d750b6c) [](https://js.plainenglish.io/javascript-algorithm-word-count-d759738c974c) [## JavaScript 算法:字数统计

### 创建一个函数，返回文本中的字数。

js.plainenglish.io](https://js.plainenglish.io/javascript-algorithm-word-count-d759738c974c) 

*多读* [***浅显易懂***](https://plainenglish.io/)