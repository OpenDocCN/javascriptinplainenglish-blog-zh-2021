# JavaScript 日期对象集方法

> 原文：<https://javascript.plainenglish.io/basics-of-javascript-the-date-object-part-2-set-methods-cbd4eaea6015?source=collection_archive---------21----------------------->

## JavaScript 基础知识—JavaScript 第 2 部分:设置方法中的日期对象

![](img/35c6855ff8e8ae07c1bcd6ec036bfe90.png)

这篇文章是我的免费 YouTube 系列关于网络开发基础知识的抄本。如果你更喜欢看而不是读，请随时访问我的频道“Dev Newbs”。

各位开发人员好，欢迎来到日期对象方法的第二部分。上一次，我们讨论了 GET 方法。今天，我们将讨论 SET 方法。很刺激，对吧？我将解释 7 对 SET 方法，其中第一对是非 UTC 方法，或者如果你愿意的话，也可以是本地时区方法，另一对是 UTC 方法。

剩下的方法是 toSetTime，它不区分时区。让我们开始吧。

第一对 SET 方法是 setFullYear()和 setUTCFullYear()，它们允许我们在第一种情况下根据本地时间，在第二种情况下根据 UTC 时间来设置日期的年分数。返回值是新的时间戳。让我们看看它的实际效果。

```
let newYear = new Date(2022, 0, 1, 0, 59, 14, 587);
console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)console.log(newYear.getTime());
// 1640995154587
```

首先，我们输出变量 newYear 来查看其中 Date 对象的值。这与前一篇文章中的日期和时间相同。午夜刚过几分钟。我以字符串格式显示日期值和毫秒数，这样我们可以更好地看到当我们稍后更改日期的某个部分时会发生什么。

```
// setFullYear()
console.log(newYear.setFullYear(2021));
// 1609459154587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setUTCFullYear()
console.log(newYear.setUTCFullYear(2021));
// 1640995154587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)
```

目前，我所在的年份部分等于当地时间值 2022。然而，当我使用 setFullYear()方法时，我会像输出建议的那样将其更改为 2021。注意与原始值相比已经改变的毫秒时间戳。等于少了 365 天——或者通俗地说——少了一年。

到目前为止，这是非常符合逻辑和容易理解的。然而，在 setUTCFullYear()的情况下，您可能会开始摇头，认为有些事情不对劲。但是请耐心听我说，你会发现尽管这种改变有点违背直觉，但它也是正确的。

当我们使用 setUTCFullYear()方法将 year 设置为值 2021 时，与使用 setFullYear()方法相比，我们将获得一个未来一年的 Date 对象。这是为什么呢？

原因很简单—通过使用 setUTCFullYear()方法，我们告诉 Javascript 首先重写日期，就好像我们的本地时区是 UTC 一样。这意味着我们得到世界协调时 2020 年 12 月 31 日。只是现在，我们用 2021 年的新值替换 2020 年的旧值。所以我们得到了新的日期 2021 年 12 月 31 日。但是当新日期的输出出现时，使用我们自己的本地时区，我们以 2022 年 1 月 1 日 CET 的日期结束。如你所见，这有点复杂，但是如果你仔细想想，这个方法就像它应该的那样工作。

其他方法完全相同，只是它们处理的是日期的不同部分。特别是月、日和小时。让我们看看他们的行动。

```
console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)console.log(newYear.getTime());
// 1640995154587// 0-based numbering of months
// 0 -> January, 1 -> February, ..., 11 -> December// setMonth()
console.log(newYear.setMonth(1));
// 1643673554587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setUTCMonth()
console.log(newYear.setUTCMonth(1));
// 1646351954587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setDate()
console.log(newYear.setDate(1));
// 1646092754587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setUTCDate()
console.log(newYear.setUTCDate(1));
// 1643759954587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setHours()
console.log(newYear.setHours(23));
// 1643842754587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setUTCHours()
console.log(newYear.setUTCHours(23));
// 1643846354587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)
```

让我们首先输出我们的旧变量 newYear。它的当前值是 2022 年 1 月 1 日，午夜过后几分钟。当然是 CET 时区。

我们首先用方法 setMonth()设置一个新的月份值，提供值 1，这是二月的索引值。此方法根据本地时间为指定日期设置月份。毫不奇怪，新的日期是二月而不是一月。到目前为止一切顺利。现在我们使用 setUTCMonth()方法，该方法根据世界时设置指定日期的月份。因此，我们当前的日期 2 月 1 日，在欧洲中部时间午夜后几分钟，变成了世界协调时午夜前几分钟的 1 月 31 日。现在，该方法将月份位置的值替换为值 1，即二月。新的 UTC 日期是 2022 年 2 月 31 日。但是等等，没有 2 月 31 日。实际上 2022 年 2 月只有 28 天。但是不要担心，因为对于日期对象来说，这些数字只是偏移量。Javascript 只是将不存在的 3 天额外天数算作下一个有效月份(即三月)的天数。所以我们得到的是世界协调时 2022 年 3 月 3 日。午夜前几分钟。现在我们只需要将它转换成 CET，这样我们就可以将它与我们得到的实际结果进行比较。因此，我们将时间向前移动一小时，得到 2022 年 3 月 4 日，欧洲中部时间午夜后几分钟。正如您在输出中看到的，它是匹配的。

我们可以用日期和时间做同样精确的日期魔术，但是我想在这一点上，你理解这个过程。因此，如果您愿意，现在可以停止这篇文章，尝试将相同的逻辑应用到 setDate()和 setHours()的示例中。我会等的。

为了保持一致，我将提供这两对方法的定义。尽管我确信在这一点上，你很清楚他们在做什么。

一对 setDate()和 setUTCDate()方法根据第一种情况下的本地时间和第二种情况下的 UTC 时间来更改给定 Date 实例中的日期。它们都返回表示新的 changed Date 对象的毫秒数。

方法 setHours()和 setUTCHours()根据方法的非 UTC 版本中的本地时间和方法的 UTC 版本中的通用时间来设置指定日期的小时。同样，这两种方法都返回表示新的更改日期对象值的毫秒数。

然后，我们有另外三对 UTC/非 UTC 方法，分别处理设置分钟、秒和毫秒。由于时区是按整小时移动的，这两个版本的方法做的事情完全一样。它们将各自的日期部分设置为一个新值。如果你愿意，这里有几个无聊的例子可以看看。

```
// setMinutes()
console.log(newYear.setMinutes(55));
// 1643846114587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setUTCMinutes()
console.log(newYear.setUTCMinutes(55));
// 1643846114587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setSeconds()
console.log(newYear.setSeconds(18));
// 1643846118587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setUTCSeconds()
console.log(newYear.setUTCSeconds(18));
// 1643846118587console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setMilliseconds()
console.log(newYear.setMilliseconds(147));
// 1643846118147console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)// setUTCMilliseconds()
console.log(newYear.setUTCMilliseconds(147));
// 1643846118147console.log(newYear);
// Thu Feb 03 2022 00:55:18 GMT+0100 (stredoeurópsky štandardný čas)
```

就像前面的方法一样，这些方法的结果是自 UNIX Epoch 或新时间戳以来的毫秒数，如果您想这样称呼它的话。

就像 GET 方法一样，您只能设置从给定时间间隔到特定日期部分的特定值。这真的很容易。分钟和秒钟的范围是从 0 到 59。对于毫秒来说，它稍微多一点——从 0 到 999。

我想向您展示的最后一个方法是 setTime()，它接受毫秒数作为输入参数，并基于该值，将 Date 对象设置为自 1970 年 1 月 1 日 00:00:00 UTC 以来以毫秒数表示的时间。

```
// set number of milliseconds since 1st January 1970
let moment = new Date();
console.log(moment.getTime());
// 1626068925087console.log(moment);
// Mon Jul 12 2021 07:48:45 GMT+0200 (stredoeurópsky letný čas)console.log(moment.setTime(1625669000160));
// 1625669000160console.log(moment);
// Wed Jul 07 2021 16:43:20 GMT+0200 (stredoeurópsky letný čas)
```

我创建了一个名为 moment 的新日期对象变量。我将它的值输出到控制台，这样我们就可以看到它代表了什么日期。然后我给这个变量赋一个新的不同的值。当然，这是一个毫秒数，但稍微小一点。当我再次输出新值时，您可以看到我更改了日期，所以它变得有点像过去。仅此而已。没什么更多的了。你可以设定任何你想要的日期，而不需要追踪时区之类的麻烦。只要您知道自 Unix Epoch 以来的毫秒数，或者您有一个 Unix 时间戳，然后您需要将它乘以 1000 以从秒中得到毫秒。你已经准备好了。

好了，这些是 Date 对象的 SET 方法，这是 Date Javascript 基础知识系列的第 2 部分的结尾。我知道很多，但你可以承认。这很有趣，你终于理解了 Javascript 的日期魔力，不是吗？我也是这么想的。

一如既往，感谢您的关注。我很快会带着日期对象系列的第三部分回来。

*更多内容看*[***plain English . io***](http://plainenglish.io/)