# JavaScript 的奇怪部分:使用日期

> 原文：<https://javascript.plainenglish.io/weird-parts-of-javascript-working-with-date-c002f98be30c?source=collection_archive---------9----------------------->

![](img/ad3ced516eb269779a78428a08155912.png)

Photo by [JOSHUA COLEMAN](https://unsplash.com/@joshstyle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用 JavaScript 从来都不容易。你总是需要不断学习和探索新的 APIs 规范。最困难的事情之一是和*日期*一起工作。你总是努力寻找一个合适的方法，或者最终像 [momentjs](https://momentjs.com/) 一样引入外部库。在本文中，我将解释如何使用普通的 JavaScript 创建一个简单的实用程序库来满足您的所有需求。

## **目录:**

1.  创建一个简单的可导出模块
2.  创建日期
3.  获取日、月、年
4.  设置日、月、年
5.  格式化日期
6.  无效日期

## 1.创建一个简单的可导出模块

在继续之前，让我们创建一个可导出的模块。根据使用的框架，导出方法可能会有所不同。下面，我提到了几个如何将方法导出为模块的例子。

**Node.js:**

```
//date.js
exports.isValid = (date) => {
  // TODO:
};
```

**与 Webpack 反应:**

```
//date.js
export const isValid = (date) => {
  // TODO:
};
```

**打字稿:**

```
//date.ts
export const isValid = (date: Date) => {
  // TODO:
};
```

## 2.创建日期

**Date** 类提供了多种创建对象的方法。要获取当前日期对象，可以使用不带任何参数的`new Date()`、 **Date** 构造函数。创建 Date 对象的另一种方法是在构造函数中使用数字值(new Date(num))。这里， **num** 表示从 1970 年 1 月 1 日 00:00:00 开始的毫秒数。

**获取当前日期:**

**以毫秒为单位获取当前时间戳:**

**简单的 hacks 到目前为止构造器:**

**注:** *因为一个月根据年的类型可以是 28、29、30、31 天。同一时间的时区随着当地日期的不同而不同。因此，在一个月内处理一个日期有点棘手。在下面的 setters 示例中，我已经解释了几个使用 months 的技巧。*

## 3.获取日、月、年

从日期对象中获取日、月或年非常简单。date 对象中有许多 getter 方法。

**例如:**

**注:**几个最大的混淆是 **getDay** 和 **getMonth** 。这两个都是从 **0** 开始的。意思是，*一月*的月份和*星期日*的日子分别表示为 ***0*** 。这是第一次很困惑。要使用月和日，您可以创建一个枚举/常量映射。

**简单的 hacks to Date getters:**

有了新的`Date.toLocaleString`方法，现在很容易获得字符串形式的日/月。您可以传递 locale 作为*“en-US”*和其他选项来格式化日期字符串。

```
console.log(today(), today().toLocaleString("en-US", { weekday: "long" })); 
console.log(today(), today().toLocaleString("en-US", { month: "long" }));
```

你也可以使用析构数组一次获得信息。

如果您想将日/月/小时/分钟格式化或前缀为零，您可以通过传递选项“2 位数”来实现。您也可以显示月份的全名。

*更多选项，可以阅读* [*这篇*](https://www.w3schools.com/jsref/jsref_tolocalestring.asp) *文章。*

## 4.设置日、月、年

从日期对象设置日、月或年非常简单。与 getter 一样，date 对象中也有许多 setter 方法。

**设置者列表:**[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Date/Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/Date)

要了解更多关于加/减日期的信息，请阅读下面提到的**堆栈溢出**链接。

*   [https://stack overflow . com/questions/2706125/JavaScript-function-to-add-x-months-to-a-date/36331522 # 36331522](https://stackoverflow.com/questions/2706125/javascript-function-to-add-x-months-to-a-date/36331522#36331522)
*   [https://stack overflow . com/questions/5645058/how-to-a-date-to-a-date-JavaScript/13633692 # 13633692](https://stackoverflow.com/questions/5645058/how-to-add-months-to-a-date-in-javascript/13633692#13633692)
*   [https://stack overflow . com/questions/2706125/JavaScript-function-to-add-x-months-to-a-date](https://stackoverflow.com/questions/2706125/javascript-function-to-add-x-months-to-a-date)

![](img/a14be6af68ff7832fa76cf510c13c7b1.png)

## 5.格式化日期

Date 对象支持多种默认的标准格式方法。你可以使用像 **toUTCString** 、 **toISOString** 、 **toLocaleString** 这样的方法来获得一个格式化的日期字符串。但是，Date 对象不支持标准的自定义格式方法。Intl 支持许多助手方法来处理日期格式。

**注意:** *Intl* 并非所有浏览器都支持。您可能需要根据需要填充多种方法。

与 *toLocaleString* 相同，您也可以在 *DateTimeFormat* 构造函数中传递选项和区域设置。

了解更多关于*datetime format*:[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Intl/datetime format](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat)

**简单的自定义格式方法:**

编写一个格式函数是非常复杂的。它通过解析日期对象、提取值和压缩日期字符串来发展。作为本文的一部分，我们就不深入了。然而，基于上述有用的实用方法，我们可以使用替换命令创建一个简单的格式函数。

**注意:**如上所述，这种格式方法没有经过生产支持测试。这只是为了演示如何编写一个简单的格式函数。您可以考虑更复杂的定义来创建格式函数。

## 6.无效日期

**无效日期**是一个空间日期对象。每当用无效的日期值创建日期对象时。它没有抛出错误，而是创建了一个具有特殊值**无效日期**的对象。这个特殊的物体非常令人困惑。这不会在对其执行的大多数操作中引发任何错误。这会导致许多生产问题。为了避免这样的问题，您可以创建一个 **isValid** 函数。

## 结论

javascript 有很大的灵活性。然而，这种灵活性造成了许多困惑和混乱。如果你知道这些窍门，它可以显著提高你的工作效率。也是在项目中学习、尝试和测试的好方法。多写代码，多复习。

*如果你正在寻找更多有用的方法，请查看* [*30 秒打字稿/*](https://decipher.dev/30-seconds-of-typescript/)

![](img/6ac9c2421251730072c3755c89822b75.png)

## 一些有用的技巧

*   不使用 *now/getTime* 方法获取时间戳

```
console.log(+new Date());
//same as
console.log(new Date().getTime());
```

*   Getter than 并且等于

**阅读更多:**[https://deciper . dev/30-seconds-of-typescript/docs/issame date](https://decipher.dev/30-seconds-of-typescript/docs/isSameDate)

*   按日期对数组排序

*   人性化持续时间

**阅读更多:**[https://deciper . dev/30-seconds-of-typescript/docs/format duration](https://decipher.dev/30-seconds-of-typescript/docs/formatDuration)

# 参考

*   [https://decipher.dev/30-seconds-of-typescript](https://decipher.dev/30-seconds-of-typescript)
*   [https://stackoverflow.com/questions/tagged/javascript+date](https://stackoverflow.com/questions/tagged/javascript+date)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Intl/datetime format](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
*   【https://www.w3schools.com/jsref/jsref_obj_date.asp 

*最初发布于*[*https://blog . decipe . dev*](https://blog.decipher.dev/how-to-work-with-date-or-javascript-weird-parts)*。*

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费周报在这里*](http://newsletter.plainenglish.io/) *。*