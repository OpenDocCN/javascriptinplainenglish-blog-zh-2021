# JavaScript 挑战:寻找一个数的倍数

> 原文：<https://javascript.plainenglish.io/javascript-challenge-find-multiples-of-a-number-8aedce7f1c21?source=collection_archive---------6----------------------->

## 让我们用 JavaScript 来寻找一个数的倍数。

![](img/f2eabd58afec849946062bd303e63bc1.png)

Photo by [Anthony Riera](https://unsplash.com/@frenchriera?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一般来说，解决算法和编码挑战是提高开发人员解决问题技能的最佳方式。也是锻炼自己编码知识和技能的一种方式。无论你使用哪种语言或技术，基本原理都是一样的。

它是关于解决问题和创造最佳解决方案，而不是关于你使用什么工具。熟能生巧。这就是为什么如果你想提高并达到下一个水平，你总是需要学习和练习你的东西(尤其是基础)。

在本文中，我们将使用 JavaScript 来解决一个简单的编码难题，它允许我们找到一个数的倍数。所以让我们开始吧。

# 说明

在这个挑战中，你必须创建一个程序，返回整数的倍数，直到你达到我们指定的极限。

所以我们有一个名为`getMultiples()`的函数，它有两个参数:

*   整数(正数)。
*   和极限(正数)。

因此，该函数应该返回一个数组，其中包含小于参数`limit`的整数`integer`的所有倍数。

因此，如果传递的参数是`(5, 15)`，函数应该返回数组`[5, 10, 15]`，因为数字 5、10 和 15 是 5 到 15 的倍数。

```
function getMultiples(integer, limit) {
  //your code goes here.
}
```

现在，在滚动到解决方案之前，尝试自己解决挑战，然后将其与我的解决方案进行比较。

# 解决挑战

为了解决这个简单的挑战，我要做的第一件事是在函数内部创建一个空数组。这样我们就可以使用一个 for 循环遍历所有的倍数并将它们推到空数组中。

让我们创建函数和空数组:

```
function getMultiples(integer, limit) {
  **let multiples = [];**

}
```

之后，我们将创建一个 for 循环，允许我们遍历所有小于极限的倍数，并将它们推送到数组中。

下面是代码示例:

```
function getMultiples(integer, limit) {
  let multiples = [];

  **for(let i = integer; i<= limit; i= i+integer){
    multiples.push(i);
  }**
}
```

如你所见，只要`i`值小于 limit 参数，循环就一直把整数值加到前面的`i`上。允许我们获取`integer`的倍数，并将它们推送到数组中。

现在要完成这个挑战，我们只需要返回函数内部的数组。

以下是完整的解决方案:

```
function getMultiples(integer, limit) {
  let multiples = [];

  for(let i = integer; i<= limit; i= i+integer){
    multiples.push(i);
  } **return multiples;** }getMultiples(2, 8); //returns [2, 4, 6, 8]
getMultiples(5, 20); //returns [5, 10, 15, 20]
```

就这样，我们解决了挑战。我知道还有其他方法可以解决这个问题。但这种方法也不错。

# 结论

正如您在上面看到的，这是一个简单的 JavaScript 编码挑战的例子，您可以通过练习来提高您的技能和测试您的知识。算法和挑战是让你解决问题的技能更上一层楼的最佳方式。坚持练习就好。

所以感谢你阅读这篇文章。希望你觉得有用。

**更多阅读:**

[](/7-useful-css-cheat-sheets-to-improve-your-skills-66d7d3a7cc8) [## 7 个有用的 CSS 备忘单来提高你的技能

### 一个很棒的 CSS 备忘单列表，你可以作为一个 web 开发者使用。

javascript.plainenglish.io](/7-useful-css-cheat-sheets-to-improve-your-skills-66d7d3a7cc8) [](/6-powerful-javascript-console-methods-that-you-probably-dont-know-a20952bac33c) [## 你可能不知道的 6 个强大的 JavaScript 控制台方法

### JavaScript 中你应该知道的有用的控制台方法。

javascript.plainenglish.io](/6-powerful-javascript-console-methods-that-you-probably-dont-know-a20952bac33c) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)