# JavaScript 中最常用的字符串方法

> 原文：<https://javascript.plainenglish.io/most-commonly-used-string-methods-in-javascript-d24d5dd7073b?source=collection_archive---------10----------------------->

## JavaScript 备忘单 2021

最新 JavaScript 编码面试问题 2021

![](img/e918648bbd964999d4454fcfae5aad87.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我总是喜欢像报纸这样能在较短时间内提供足够信息的东西。在这里，我为日常前端开发创建了一些技巧。

这是一篇介绍 JavaScript 中不同字符串方法的新文章。这些技巧可以被认为是最终将帮助你在 2021 年跨过 JavaScript 编码面试这条河的小石头。

> 我知道小石头没多大作用，但如果我们有成千上万块这样的石头，它们就有作用了。这就是为什么我明天会带来新的石头。敬请关注。😉

# 获取字符串值

## 切片()

它通过获取开始和结束位置来提取字符串的一部分，并返回新的字符串。

```
let str = 'atit,p,patel';const str1 = str.slice(7, 12); // Returns patel
```

## 子字符串()

它的工作方式与`slice` 完全相同，但不能采用负索引。

```
const str2 = str.substring(7, 12); // Returns patel
```

## substr()

第二个参数取提取部分的长度，而不是此处的结束位置。

```
let str = 'atit,p,patel';const str3 = str.substr(0, 4); // Returns atit
```

# 替换内容

## 替换()

此方法将用新值替换指定的值。

```
let str = 'atit,p,patel';const str4 = str.replace('patel','modi'); //atit,p,modi
```

# 转换为大写和小写

可以将内容转换成大写或小写。

```
let str = 'atit,P,patel';
const str5 = str.toUpperCase();//ATIT,P,PATELconst str6 = str.toLowerCase();//atit,p,patel
```

# 连接字符串

## 模板文字

可用于连接字符串。

```
const t1 ='atit';const t2 = 'patel';const join1 = `${t1} ${t2}`;//atit patel
```

## concat()

连接两个或多个字符串:

```
const t1 ='atit';const t2 = 'patel';const join2 = t1.concat(" ",t2);//atit patel
```

# 删除空格

## 修剪()

它删除字符串两边的空格。

```
const tr = " atit    ";console.log(tr.trim());//atit
```

# 填料

`padStart`和`padEnd`在字符串的开头和结尾添加填充。

```
let text = "3";text.padStart(4,0) // Returns 0003let text = "3";text.padEnd(4,0) // Returns 3000
```

# 提取字符串字符

## charAt()

这个方法给出了特定索引处的字符。

```
let text = “atit patel”;
text.charAt(0) // Returns a
```

# 属性访问

我们可以使用索引来访问字符串中的任何字符。

```
let text = “atit patel”;
text[0] // Returns a
```

# 将字符串转换为数组

## 拆分()

split on 将根据传递的符号将字符串转换为数组。

```
const test = "a,t,i,t"console.log(test.split(","));//["a", "t", "i", "t"]
```

## 范围

spread 可以通过拆分每个字符将任意字符串转换为数组。

```
const t1= "atit"console.log([...t1]);//["a", "t", "i", "t"]
```

***你可以在这里看到例子。***

[https://stackblitz.com/edit/js-1dso4m](https://stackblitz.com/edit/js-1dso4m)

# 延伸阅读:

[](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [## 2021 年你应该知道的 JavaScript 顶级优化技术

### 使用现代速记技术、技巧和诀窍优化您的 JavaScript 代码。

javascript.plainenglish.io](/33-javascript-useful-shorthands-cheat-list-2021-e08b46a1a688) [](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [## 新引入的 JavaScript 特性可以提升您的知识

### 利用 ES2021 的新功能优化您的 JavaScript 代码。

javascript.plainenglish.io](/latest-javascript-features-you-should-know-in-2021-7712232c00ae) [](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) [## 你必须为下一次角度面试准备的 100 个问题(1-10)

### 最常见的角度面试问题 2021

javascript.plainenglish.io](/top-100-questions-you-must-prepare-for-your-next-angular-interview-1-10-3e13d5fefab9) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)