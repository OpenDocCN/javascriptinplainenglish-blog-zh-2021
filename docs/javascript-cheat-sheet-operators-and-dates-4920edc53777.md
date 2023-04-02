# JavaScript 备忘单—运算符和日期

> 原文：<https://javascript.plainenglish.io/javascript-cheat-sheet-operators-and-dates-4920edc53777?source=collection_archive---------20----------------------->

![](img/7acf847432089c92df5c297b3828b4c0.png)

Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是 web 编程中最流行的编程语言之一。

在本文中，我们将了解现代 JavaScript 的基本语法。

# 经营者

我们可以用 JavaScript 做算术。

我们用`+`加，用`-`减:

```
let a = b + c - d;
```

我们用`*`乘，用`/`除:

```
let a = b * (c / d);
```

我们用`/`得到一个数除以另一个数的余数:

```
let x = 100 % 48;
```

我们用`++`递增:

```
a++;
```

我们用`--`递减:

```
b--;
```

# 类型 of

我们可以用`typeof`获得原始值和对象的类型:

```
typeof a
```

它主要用于原始值，因为它为所有对象返回`'object'`。

# 分配

我们用`=`给一个变量赋值:

```
let x = 10
```

右边的表达式被赋给左边的变量。

`a +=b`是`a = a + b`的简称。我们也可以用`-`、`*`和`/`来代替`+`。

# 比较

我们用`===`来比较平等:

```
a === b
```

我们用`!==`检查不平等:

```
a !== b
```

我们用以下公式检查`a`是否大于`b`:

```
a > b
```

我们检查`a`是否小于`b`,用:

```
a < b
```

我们可以检查小于或等于:

```
a <= b
```

我们检查是否大于或等于:

```
a >= b
```

逻辑与是`&&`:

```
a && b
```

与逻辑或为`||`:

```
a || b
```

# 日期

我们可以用`Date`构造函数创建日期对象:

```
let d = new Date("2017-06-23");
```

如果我们省略月和日，那么它被设置为 1 月 1 日:

```
let d = new Date("2017");
```

我们可以添加小时、分钟和秒:

```
let d = new Date("2017-06-23T12:00:00-09:45");
```

人类可读的日期也有效:

```
let d1 = new Date("June 23 2017");
let d2 = new Date("Jun 23 2017 07:45:00 GMT+0100 (Tokyo Time)");
```

日期对象带有让我们从中获取各种值的方法。

我们通过书写来称呼它们:

```
let d = new Date();
let a = d.getDay();
```

获取星期几

以数字形式获取一个月中的某一天。

得到 4 位数的年份。

得到小时数。

`getMilliseconds()`获取毫秒。

`getMinutes()`得到会议记录。

`getMonth()`大半夜的。

`getSeconds()`秒变秒。

`getTime()`获取自 1970 年 1 月 1 日以来的毫秒数。

我们也可以用一些 setter 方法来设置值。

为了称呼他们，我们写道:

```
let d = new Date();
d.setDate(d.getDate() + 7);
```

`setDay()`设置星期几

`setDate()`将一个月中的某一天设置为数字。

`setFullYear()`设定 4 位数年份。

`setHours()`设置小时。

`setMilliseconds()`设置毫秒。

`setMinutes()`设置分钟。

`setMonth()`设置月份。

`setSeconds()`设置秒数。

`setTime()`设置时间戳。

# 结论

JavaScript 附带了各种操作符和`Date`构造函数，让我们可以创建、获取和设置日期。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)