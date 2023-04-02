# JavaScript 中 11 个必须使用的一行程序

> 原文：<https://javascript.plainenglish.io/11-must-use-one-liner-alternatives-in-javascript-577e900a5dc9?source=collection_archive---------10----------------------->

## 掌握您的 JavaScript 技能

![](img/5c579a124e6611d54828aa19a35049e2.png)

Photo by [Pablo Arroyo](https://unsplash.com/@pablogamedev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名熟练的开发人员，必须经常在旅途中磨练自己的技能。随着我们的成长，我们开始更好地理解任何复杂的问题，我们也倾向于用最简单的逻辑来解决它。所以，代码越少，越干净。

清理代码有助于更好地维护它，提高浏览器性能，并且被认为非常有效。尤其是随着 ES6 的引入，有如此多的功能可以使用箭头功能轻松完成。

因此，停止用复杂的方式编写代码，开始使用这些一行程序的替代方案，可以很容易地为您省去很多麻烦。

# 1.反转一根绳子

在最初的日子里，我使用 for 循环来反转一个字符串，这很容易包含至少 3-4 行代码。这就是我们如何用一行代码解决这个问题-

```
const reverse = str => str.split('').reverse().join('');reverse('hi there'); // ‘ereht ih’
```

# 2.获取随机布尔值

我们可以借助`Math.random()`得到一个随机布尔。`Math.random`帮助我们得到一个介于 0 和 1 之间的随机数。因此，当我们检查该值是小于还是大于 0.5 时，我们以 50%的概率得到一个无偏的随机真值或假值。

```
const randomBoolValue = () => Math.random() <= 0.5;console.log(randomBoolValue());
```

# 3.检查一个数字是偶数还是奇数

写一个带有 if 条件的函数来检查 mod 2 是否给出零，这绝对是老一套了。这是聪明的做法-

```
const isEven = num => num % 2 === 0;console.log(isEven(4)); //true
```

# 4.检查日期是否是周末

检查某一天是工作日还是周末只需使用一行代码就可以完成，如-

```
const isWeekend = (date) => [0, 6].indexOf(date.getDay()) !== -1;console.log(isWeekend(new Date(2021, 4, 14)));// false (Friday)console.log(isWeekend(new Date(2021, 4, 15)));// true (Saturday)
```

我们甚至可以检查某一天是否是工作日，就像-

```
const isWeekday = (date) => date.getDay() % 6 !== 0;console.log(isWeekday(new Date(2021, 0, 11)));// Result: true (Monday)console.log(isWeekday(new Date(2021, 0, 10)));// Result: false (Sunday)
```

# 5.检查一个元素当前是否在焦点上

`document.activeElement`属性可以用来检查 DOM 中的一个元素是否在焦点上，使用下面一行代码

```
const focusedElement = (elem) => (elem === document.activeElement);focusedElement(anyElement);
```

# 6.检查对象是否为空

即使一个对象是空的，如果和`{}`比较，它也只会返回`false`。

```
var a = {};a === {}; //false
```

下面的一行程序可以帮助我们完成这项工作

```
const isEmpty = obj => Reflect.ownKeys(obj).length === 0 && obj.constructor === Object;isEmpty(a); //true
```

# 7.在元素后插入一个 HTML 字符串

在 DOM 中插入任何内容并不总是要求我们识别要插入的元素，然后执行任何必须执行的操作，只需使用下面一行代码就可以完成

```
const insertHTMLAfter = (html, el) => el.insertAdjacentHTML(‘afterend’, html);insertHTMLAfter(‘<span> Just some text that has to be added </span>’, <any dom element object>);
```

# 8.打乱数组

显然，我们没有默认的方法来打乱一个数组，但是可以很容易地用 sort 和`Math.random`方法来完成

```
const shuffleArr = (arr) => arr.sort(() => 0.5 — Math.random());console.log(shuffleArr([1, 2, 3, 4]));// [3, 4, 1, 2]
```

# 9.检查数组是否为空

一个简单的一行程序来检查一个数组是否

```
const isEmpty = arr => Array.isArray(arr) && arr.length === 0;isEmpty([1, 2, 3]); //falseisEmpty([]); //true
```

# 10.滚动到页面顶部

当提供了坐标后，我们可以使用下面的代码片段滚动到页面的顶部

```
const goToTop = () => window.scrollTo(0, 0);goToTop();
```

# 11.获取数组中的唯一值

如果你在一个数组中有任何重复的值，并且只想要唯一的值，那么这里有一个最简单的方法。

```
const uniqueArray = (arr) => […new Set(arr)];console.log(uniqueArray([1, 2, 3, 1, 2, 3, 4, 5])); // [1, 2, 3, 4, 5]
```

# **结论**

希望这有所帮助。如果你知道任何一行代码让你的生活变得更简单，那么请留下你的评论！

保持安全，保持快乐！:)

*更多内容看*[***plain English . io***](http://plainenglish.io/)