# JavaScript 算法:返回正数

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-return-positive-numbers-faacd7537b32?source=collection_archive---------4----------------------->

## 一个函数，它将返回在另一个数组中找到的正数数组。

![](img/07650efd603876a6c790907556194445.png)

Photo by [Nick Hillier](https://unsplash.com/@nhillier?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`getPositives`的函数，它将接受一个数组`ar`作为参数。

给你一个包含正数和负数的数组。该函数的目标是输出另一个数组，该数组只包含输入数组中的正数。

示例:

```
let numArr = [-5, 10, -3, 12, -9, 5, 90, 0, 1];
getPositives(numArr);// output: [10,12,5,90,0,1]
```

这里不多解释了。所有大于-1 的值都保留在输出数组中。

有几种方法可以编写这个函数，但是我们将集中讨论一种使用`filter()`方法的方法。

`filter()`方法所做的是创建一个新的数组，该数组包含数组中通过所提供的回调函数测试的所有元素。

数组*过滤掉*没有通过测试的数字。我们希望函数检查的测试是传递的值是否大于-1。所有小于 0 的数字都不会进入数组。

我们将把这个新数组放入一个名为`posArr`的变量中。

```
const posArr = ar.filter(num => num > -1);
```

我们在`filter()`方法中的测试函数相当于编写:

```
const posArr = ar.filter(function(num){
    return num > -1;
});
```

现在我们的数组只包含正数，我们将返回`posArr`。

```
return posArr;
```

下面是该函数的其余部分:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-validate-code-with-simple-regex-827bbbc066dd) [## JavaScript 算法:用简单的正则表达式验证代码

### 编写一个使用正则表达式验证数字代码的函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-validate-code-with-simple-regex-827bbbc066dd) [](https://levelup.gitconnected.com/javascript-algorithm-title-case-a-sentence-995da42238f0) [## JavaScript 算法:标题大小写一句话

### 我们写了一个将字符串转换成标题大小写的函数

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-title-case-a-sentence-995da42238f0) [](https://codeburst.io/javascript-algorithm-profile-lookup-821bcd88f290) [## JavaScript 算法:配置文件查找

### 我们编写了一个函数，它将遍历一个对象数组，如果确定的话，返回一个特定属性的值…

codeburst.io](https://codeburst.io/javascript-algorithm-profile-lookup-821bcd88f290)