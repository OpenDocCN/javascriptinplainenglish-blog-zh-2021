# JavaScript 算法和数据结构挑战——Fizz Buzz

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-and-data-structure-challenge-fizz-buzz-5ef81800cb99?source=collection_archive---------13----------------------->

## JavaScript 中的 Fizz Buzz challenge 黑客团队的一个编程挑战的解决方案。

![](img/1762a123385c23699dae35732826c33b.png)

Photo by [Alex Kotliarskyi](https://unsplash.com/@frantic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在上一篇文章中，我们研究了如何实现冒泡排序算法挑战。如果你错过了，请点击下面的链接。

[](/algorithm-and-data-structure-challenge-implementing-bubble-sort-34403eecc87) [## 算法和数据结构挑战—实现冒泡排序

### JavaScript 中的冒泡排序挑战 freeCodeCamp 的一个面试准备问题的解决方案。

javascript.plainenglish.io](/algorithm-and-data-structure-challenge-implementing-bubble-sort-34403eecc87) 

在这篇文章中，我们将看看黑客联盟网站的另一个挑战，看看我们如何解决它。

## **挑战**

考虑以下问题:

编写一个短程序，在新的一行中打印从 1 到 100 的每个数字。

对于 3 的每个倍数，打印“Fizz ”,而不是数字。

对于 5 的每个倍数，打印“Buzz”而不是数字。

对于同时是 3 和 5 的倍数的数字，打印“FizzBuzz”而不是数字。

写一个解决方案(或减少一个现有的方案),使它尽可能少的字符。

## **解决方案**

这个挑战是初学者友好的，非常容易理解。

**小解说**

举个例子，我们得到一个数字，我们想通过某个测试。如果这个数能被 3 整除，我们就注销“嘶嘶”,如果这个数能被 5 整除，我们就注销“嘶嘶”,如果这个数能被 3 和 5 整除，我们就注销“嘶嘶”。

所以我们可以简单地遍历参数号，然后使用 if 语句将它传递给一些测试。

**举例:**

```
function(n){

 for (i=1; i<=n; i++) { if (i%15 === 0) { console.log (“FizzBuzz”)}else if (i%3 === 0) { console.log (“Fizz”); }else if (i%5 === 0) { console.log(“Buzz”);}else { console.log(i);}}
```

**关键要点:**

这个挑战可以帮助我们更好地理解上述领域。

*   循环的使用
*   if-else 语句的使用
*   逻辑和算术运算符的使用

## **最终想法**

我希望这篇文章对解决这个问题有所帮助。如果你喜欢它，不要犹豫与他人分享。

## 更多阅读:

[](/what-is-the-model-view-controller-mvc-d4d51b642565) [## 什么是模型视图控制器(MVC)？

### MVC 的初学者友好解释。

javascript.plainenglish.io](/what-is-the-model-view-controller-mvc-d4d51b642565) [](/the-fascinating-story-behind-the-birth-of-vue-js-a-documentary-97d353688c2) [## Vue.js 诞生背后的迷人故事

### 揭开创建 Vue.js 框架背后的故事。

javascript.plainenglish.io](/the-fascinating-story-behind-the-birth-of-vue-js-a-documentary-97d353688c2) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)