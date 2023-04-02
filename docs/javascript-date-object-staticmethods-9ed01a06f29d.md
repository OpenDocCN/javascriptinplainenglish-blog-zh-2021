# JavaScript 日期对象——什么是静态方法以及如何使用它们？

> 原文：<https://javascript.plainenglish.io/javascript-date-object-staticmethods-9ed01a06f29d?source=collection_archive---------16----------------------->

## JavaScript 中日期对象的基础知识第 3 部分:使用静态方法

![](img/ed2945ea8f4df4d6f4aa210522d9f358.png)

这篇文章是我的免费 YouTube 系列关于网络开发基础知识的抄本。如果你更喜欢看而不是读，请随时访问我的频道“Dev Newbs”。

嗨，我的新手伙伴们！约会方法的另一集在这里。今天，我们将看看日期对象的静态方法。共有三种，我将逐一解释和展示。我们开始吧。

第一个静态方法被称为 now()，它返回自 1970 年 1 月 1 日 00:00:00 UTC 以来经过的毫秒数。返回值是一个原始整数值。

EcmaScript 规范的第 5 版中规定了这种方法，所以一些旧版本的浏览器仍然可能不支持它。虽然我相信你不会遇到这样的情况。但是如果您以某种方式这样做了，您可以简单地通过使用 getTime()的非静态方法来覆盖这个问题。

现在让我们看看这个静态方法的一些例子。

```
console.log(Date.now());
console.log(Date.now());
console.log(Date.now());
console.log(Date.now());
console.log(Date.now());// 1626156551132
// 1626156551133
// 1626156551133
// 1626156551133
// 1626156551133
```

有些浏览器(例如 Firefox)在使用 Date.now()方法时会降低时间精度。这意味着它通过将精确值四舍五入到一定的精度，提供了针对各种计时攻击和指纹识别的保护。

我检查了不同的浏览器，Chrome 没有提供这样的行为。您可以看到，您甚至可以多次获得相同的毫秒数——我认为这取决于处理器的当前负载。

第二个静态方法叫做 parse()，顾名思义，它的工作是解析日期的字符串表示。如果成功，它将返回自 1970 年 1 月 1 日 00:00:00 UTC 以来的毫秒数。如果解析因字符串未被识别或日期包含非法日期值而失败，则返回“NaN”常量。

这种方法在历史上并不十分可靠，在 EcmaScript 版本 5 之前，解析实现完全依赖于供应商。直到今天，它仍然不太统一，但至少大多数常见的格式在每个浏览器实现中都是可以解析的。官方的说法是，所有的实现都应该支持 ISO 8601 的简化格式，但幸运的是，可解析格式的集合比这要大。我将在示例中展示我能想到的所有案例。如前所述，返回值是表示自 UNIX 纪元以来经过的毫秒数。现在，对于这些例子…

```
// uses 00:00:00.000 in local time
console.log(Date.parse("2021-07-07"));
// 1625616000000// uses 00:00:00.000 in UTC/GMT
console.log(Date.parse("07 Jul 2021"));
// 1625608800000// these 2 use local time
console.log(Date.parse("2021-07-07T22:19:38"));
// 1625689178000console.log(Date.parse("Wed, 07 Jul 2021 22:19:38"));
// 1625689178000// these 2 use explicitly specified UTC/GMT
// parse() method can only handle GMT, not UTC or any other time zone shortcut
console.log(Date.parse("07 Jul 2021 20:19:38 GMT"));
// 1625689178000console.log(Date.parse("Wed, 07 Jul 2021 20:19:38 GMT"));
// 1625689178000// specifying UTC/GMT time zone by +00:00
console.log(Date.parse("2021-07-07T20:19:38.054+00:00"));
// 1625689178054// specifying CET time zone by +02:00
console.log(Date.parse("2021-07-07T22:19:38.054+02:00"));
// 1625689178054// Z - represents GMT/UTC in ISO 8601 format
console.log(Date.parse("2021-07-07T20:19:38.054Z"));
// 1625689178054
```

我把所有可以解析的格式分成三组。第一个只指定年、月和日，其余的使用默认值。有趣的是，第一种格式使用本地时间，而第二种格式使用 GMT/UTC。

第二组中的格式也指定了小时、分钟和秒，但没有提到毫秒。情况如下。如果没有明确指定 GMT 时区，则使用当地时区。观察语法分析的奇怪行为也很有趣。它处理快捷方式 GMT，但不能处理 UTC 或任何其他时区快捷方式，如 CET。

最后一组也指定毫秒。UTC 或者更确切地说是 GMT 时区可以用至少两种不同的方式来指定。我们可以使用标准和通用的“+00:00”，也可以使用快捷键“Z”。这就是静态方法 parse()的内容。

最后一个方法是 UTC()方法，它接受类似于 Date 构造函数的参数，但是将它们视为 UTC。它返回自 UNIX 纪元以来的毫秒数。

UTC()方法的行为与 Date 构造函数完全一样，即使在处理 0 到 99 范围内的年份值时也是如此。提示:它会像您键入 1900 到 1999 之间的值一样处理它们。

让我们看一些例子，之后我会告诉你更多关于这个方法的事情。

```
// this date is specified in local time (GMT+0100)
let endDate = new Date(2021,11,31,23,59,59,999);
console.log(endDate.getTime());
// 1640991599999console.log(endDate);
// Fri Dec 31 2021 23:59:59 GMT+0100 (stredoeurópsky štandardný čas)// this date is specified in UTC (GMT+0000)
let utcDate = Date.UTC(2021,11,31,23,59,59,999);
console.log(utcDate);
// 1640995199999console.log(new Date(utcDate));
// Sat Jan 01 2022 00:59:59 GMT+0100 (stredoeurópsky štandardný čas)// this date is specified in UTC (GMT+0000)
// 23 months - 12 months = 11 months
// year 2020 + 12 months = year 2021
let wrongUtcDate = Date.UTC(2020,23,31,23,59,59,999);
console.log(wrongUtcDate);
// 1640995199999console.log(new Date(wrongUtcDate));
// Sat Jan 01 2022 00:59:59 GMT+0100 (stredoeurópsky štandardný čas)
```

这个方法实际上与日期构造函数只有两点不同。首先，它使用世界时间而不是当地时间。第二个是它返回的数字是时间值，而不是日期对象。

如果任何参数由于某种原因超出范围，该方法会接受该值。因此，例如，如果您键入 23 作为月份，它会将年份增加 1，然后从值 23 中减去 12 个月，得到值 11，然后将该值用作月份位置的值。很酷，如果你问我。

但这是我今天为你准备的。所以恐怕我们今天就到此为止了。希望你喜欢。

一如既往，感谢您的不懈关注，我们将在下一次讨论我们需要的格式化日期对象的方法时再见。

*更多内容看*[***plain English . io***](http://plainenglish.io/)