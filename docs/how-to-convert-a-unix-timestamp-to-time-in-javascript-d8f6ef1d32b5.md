# 如何在 JavaScript 中将 Unix 时间戳转换成时间？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-unix-timestamp-to-time-in-javascript-d8f6ef1d32b5?source=collection_archive---------3----------------------->

![](img/a59bb7a97f79440d04822b5e1123c1e6.png)

Photo by [Yan L](https://unsplash.com/@yl1980s?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须将 Unix 时间戳转换成更易于阅读的格式。

在本文中，我们将了解如何用 JavaScript 将 Unix 时间戳转换成可读性更好的格式。

# 使用日期构造函数及其实例方法

我们可以将 Unix 时间戳(以毫秒为单位)传递给`Date`构造函数来创建一个`Date`实例。

然后，我们可以使用它的实例方法获取日期的不同部分，并将其放入一个字符串中。

例如，我们可以写:

```
const unixTimestamp = 15493124560
const date = new Date(unixTimestamp * 1000);
const hours = date.getHours();
const minutes = "0" + date.getMinutes();
const seconds = "0" + date.getSeconds();
const formattedTime = `${hours}:${minutes.substr(-2)}:${seconds.substr(-2)}`;console.log(formattedTime);
```

我们在几秒钟内就有了`unixTimestamp`。

然后我们将其乘以 1000，并将其传递给`Date`构造函数。

接下来，我们调用`getHours`从`Date`实例中获取小时数。

我们调用`getMinutes`来得到会议记录。

然后我们调用`getSeconds`来获取秒数。

然后我们把它们放在`formattedTime`字符串中。

为了得到 2 位数的分和秒，我们用-2 调用`substr`来得到它们的最后 2 位数。

这将删除数字字符串中的任何前导零。

然后应该会看到`’5:42:40'`的结果。

要获得年、月和日，我们可以写:

```
const unixTimestamp = 1613330814
const date = new Date(unixTimestamp * 1000);
const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
const year = date.getFullYear();
const month = months[date.getMonth()];
const dt = date.getDate();
const hours = date.getHours();
const minutes = "0" + date.getMinutes();
const seconds = "0" + date.getSeconds();
const formattedTime = `${year}-${month}-${dt} ${hours}:${minutes.substr(-2)}:${seconds.substr(-2)}`;console.log(formattedTime);
```

我们有以秒为单位的 Unix 时间戳。

因此，在将它传递给`Date`构造函数之前，我们必须将它乘以 1000。

然后我们有一个包含月份缩写的`months`数组。

`getFullYear`返回一个`Date`实例的 4 位数年份。

`getMonth`返回`Date`实例的月份号，0 表示一月，1 表示二月，一直到 11 表示十二月。

`getDate`方法返回一个月中的某一天。

代码的其余部分是相同的。

那么`formattedDate`就是`'2021-Feb-14 11:26:54'`。

# `The toLocaleTimeString Method`

将日期格式化为可读字符串的另一种方法是使用`toLocaleTimeString`方法。

它将区域设置字符串作为其参数。

例如，我们可以写:

```
const str = new Date(1613331041675).toLocaleTimeString("en-US")
console.log(str)
```

我们将转换成毫秒的 Unix 时间戳传递给`Date`构造函数。

然后我们用`'en-US'`地点调用`toLocaleDateString`。

结果我们应该得到`‘11:30:41 AM’`。

# `The Intl.DateTimeFormat Constructor`

我们可以格式化日期的另一种方法是使用`Intl.DateTimeFormat`构造函数。

例如，我们可以写:

```
const dtFormat = new Intl.DateTimeFormat('en-US', {
  timeStyle: 'medium',
  timeZone: 'PST'
});
const str = dtFormat.format(new Date(1613331041675));
console.log(str)
```

我们将 locale 作为构造函数的第一个参数传入。

我们传递一些选项作为第二个参数。

`timeStyle`有当时的格式化风格。

`timeZone`设置返回时间的时区。

然后我们调用`format`返回一个带有时间的字符串。

结果我们得到了`‘11:30:41 AM’`。

# 结论

我们可以用自己的代码用 JavaScript 格式化 Unix 时间戳，或者使用本地方法和构造函数来格式化日期。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)