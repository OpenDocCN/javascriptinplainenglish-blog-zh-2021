# 如何在 JavaScript 中将字符串转换成日期对象？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-string-to-a-date-object-in-javascript-58effc92440a?source=collection_archive---------4----------------------->

![](img/23a9ab0c42f5d0425f2cb4f27b40fe4b.png)

Photo by [Amber Kipp](https://unsplash.com/@sadmax?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们有一个日期字符串，我们想在 JavaScript 中将其转换成日期对象。

在本文中，我们将研究如何在 JavaScript 中将日期字符串转换为日期对象。

# 提取日期字符串的各个部分，并将它们传递给日期构造函数

从日期字符串创建 JavaScript 日期对象的一种方法是从日期字符串中提取日期部分，并将它们全部传递给`Date`构造函数。

例如，我们可以写:

```
const [year, month, day] = '2020-04-03'.split('-');
const date = new Date(year, month - 1, day);
console.log(date.toDateString());
```

我们用`'-'`调用日期字符串上的`split`来用破折号分割日期字符串。

然后我们从分离的字符串数组中析构`year`、`month`和`day`。

接下来，我们将所有这些传递给`Date`构造函数。

我们必须从`month`中减去 1，因为`Date`构造函数接受的月份值是从 0 到 11，其中 0 代表 1 月，11 代表 12 月。

然后我们从`toDateString`方法中得到`‘Fri Apr 03 2020’`。

我们还可以将一个日期放入一个 ISO 日期字符串中，并将其传递给`Date`构造函数。

例如，我们可以写:

```
const st = "26.04.2020";
const pattern = /(\d{2})\.(\d{2})\.(\d{4})/;
const date = new Date(st.replace(pattern, '$3-$2-$1'));
console.log(date)
```

我们用`pattern` regex 对象获取日期字符串的各个部分。

然后我们调用`st`串上的`replace`并移动带有`$`占位符的部件。

`\d`提取数字。

花括号中的数字是要提取的位数。

`$1`是第一个提取的部分，即`'26'`

`$2`是第二个提取部分，即`'04'`

而`$3`是第三个提取的部分，也就是`'2020'`。

构造函数将创建一个 UTC 日期。

所以我们得到字符串形式的`date`是`'Sat Apr 25 2020 17:00:00 GMT-0700 (Pacific Daylight Time)’`。

# moment.js

我们可以将一个日期字符串传入 moment.js' `moment`函数，将其转换成我们可以操作的对象。

例如，我们可以写:

```
const momentDate = moment("12-25-2020", "MM-DD-YYYY");
```

使用第二个参数中指定的日期字符串格式创建一个时刻日期对象。

我们可以使用`isValid`方法来检查有效日期:

```
const isValid = moment("abc").isValid()
console.log(isValid)
```

`isValid`应该是`false`，因为`'abc'`不是一个有效的日期。

我们可以用`toDate`将一个时刻日期对象转换成一个本地 JavaScript `Date`实例:

```
const date = moment("12-25-2020", "MM-DD-YYYY").toDate();
console.log(date)
```

# 结论

要将日期字符串转换成 JavaScript 日期对象，我们可以自己提取日期字符串的各个部分，并将其放入`Date`构造函数中。

或者我们可以使用像 moment.js 这样的第三方库来帮助我们简化这项工作。

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) *。*