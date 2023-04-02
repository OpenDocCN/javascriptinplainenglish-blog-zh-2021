# JavaScript Date 对象:格式化日期字符串的方法

> 原文：<https://javascript.plainenglish.io/javascript-date-object-methods-to-format-the-date-string-6b4c56f4cf2f?source=collection_archive---------21----------------------->

## JavaScript 中日期对象的基础知识第 4 部分:使用格式方法

![](img/1dd18a4a5f92af69c87284db969f8cf9.png)

这篇文章是我的免费 YouTube 系列关于网络开发基础知识的抄本。如果你更喜欢看而不是读，请随时访问我的频道“Dev Newbs”。

你好，戴夫·纽斯！今天我为你准备了一些特别的东西。我们今天要来玩一下日期对象的输出格式。有 6 种方法焦急地等着你去了解它们。所以我们不要停留太久，让我们开始吧！

今天的第一个方法是方法 toString()。它返回一个表示指定日期对象的字符串。ECMA-262 中规定了返回字符串的格式，如下所示:

*   3 个字母的英文星期名称
*   3 个字母的英文月份名称
*   月份中的两位数天
*   四位数年份
*   一天中的两位数小时
*   2 位数的小时分钟
*   分钟的 2 位数秒 b b
*   固定字符串“GMT”
*   时区偏移符号
*   两位数小时时差
*   2 位数分钟偏移
*   或者，它可以包含括号内的本地时区的全名或缩写

列表中的每个值都用一个空格与其他值分隔开。

```
// FORMAT: Www Mmm dd yyyy HH:mm:ss GMT ±9999 (timezone name or abbreviation)
console.log(new Date());
console.log(new Date().toString());// Thu Jul 15 2021 09:52:55 GMT+0200 (stredoeurópsky letný čas)
// Thu Jul 15 2021 09:52:55 GMT+0200 (stredoeurópsky letný čas)
```

您可能已经在输出中看到了日期对象的这种格式。事实上，如果您曾经将 console.log 与 Date 对象变量一起使用，您一定会看到它。当日期要表示为文本值时，或者当日期用于字符串连接时，会自动调用 toString()方法。

接下来的方法名称相似，但结果略有不同。它的名字是 toUTCString()，我肯定你知道它与前一个的至少一个不同之处…对。此方法使用 UTC 时区将日期转换为字符串。

toUTCString()返回的值是以下形式的字符串:

*   星期几，由三个字母和一个固定的逗号字符组成
*   一个月中的某一天，如有必要，以两位数字加前导零表示
*   月，三个字母
*   年份，如有必要，以四位数或更多位数加前导零表示
*   小时，如有必要，以两位数字加前导零表示
*   分钟，如有必要，以两位数字加前导零表示
*   秒，如有必要，以两位数字加前导零表示

```
// FORMAT: Www, dd Mmm yyyy hh:mm:ss GMT
console.log(new Date().toUTCString());// Thu, 15 Jul 2021 07:52:55 GMT
```

每个值后面都有一个空格作为分隔符。字符串的结尾由固定字符串“GMT”标记。当然，正如我之前提到的……如果你愿意，时区可以是 UTC 或 GMT。

第三个方法是 toISOString()，这个方法返回一个简化的扩展 ISO 格式(ISO 8601)的字符串，它总是 24 或 27 个字符长。

```
// FORMAT: YYYY-MM-DDTHH:mm:ss.sssZ or ±YYYYYY-MM-DDTHH:mm:ss.sssZ
console.log(new Date().toISOString());// 2021-07-15T07:52:55.966Z
```

时区始终为零 UTC 偏移量，这由后缀“Z”表示。这意味着日期是根据世界时间格式化的。

第四个方法被称为 toJSON()，它再次返回 Date 对象的字符串表示。我们感兴趣的是，这个方法使用了前一个方法— toISOString()。所以结果是完全相同的格式。该方法通常用于在 JSON 序列化期间序列化日期对象。

```
// FORMAT: same is toISOString() method
console.log(new Date().toJSON());// 2021-07-15T07:52:55.967Z
```

今天的第五个方法叫做 toDateString()。需要记住的唯一重要的事情是，它以英文返回 date 对象的日期部分，格式如下，用空格分隔:

*   星期名称的前三个字母
*   月份名称的前三个字母
*   一个月中的第几天，如有必要，在左边填充一个零
*   (至少)四位数年份，必要时在左边用零填充

```
// FORMAT: Www Mmm dd yyyy
console.log(new Date().toDateString());// Thu Jul 15 2021
```

返回值正好是 Date 对象的前半部分—星期几、月中的天、年中的月和年。

第六个也是最后一个方法是方法 toTimeString()。该方法以英文的可读形式返回 Date 对象的时间部分。

结构如下:

*   2 位数的小时分钟
*   两位数的分钟秒
*   固定字符串“GMT”
*   时区偏移符号
*   两位数小时时差
*   2 位数分钟偏移
*   或者，它可以包含括号内的本地时区的全名或缩写

列表中的每个值都用一个空格与其他值分隔开。

```
// FORMAT: HH:mm:ss GMT ±9999 (timezone name or abbreviation)
console.log(new Date().toTimeString());// 09:52:55 GMT+0200 (stredoeurópsky letný čas)
```

这个方法和前一个方法实际上是今天的第一个方法——toString()方法的一半。因为如果您将它们组合在一起，您会得到相同的结果，就好像您从一开始就使用 toString()一样。

好吧。对于当时来说，这就是正确的格式化方法。我开玩笑的——这太过分了。所以今天就到此为止吧。我们都挺过来了，所以就算是胜利吧。

一如既往，感谢您的关注，我们很快会在日期对象方法的最后一集再见。我把最好的留到了最后。在那之前…

*更多内容看*[***plain English . io***](http://plainenglish.io/)