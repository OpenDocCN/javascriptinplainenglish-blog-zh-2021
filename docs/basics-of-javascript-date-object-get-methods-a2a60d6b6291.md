# JavaScript 基础—日期对象第 1 部分:GET 方法

> 原文：<https://javascript.plainenglish.io/basics-of-javascript-date-object-get-methods-a2a60d6b6291?source=collection_archive---------21----------------------->

![](img/4f8151b433629422f01dc35aef3a9a57.png)

这篇文章是我的免费 YouTube 系列关于网络开发基础知识的抄本。如果你更喜欢看而不是读，请随时访问我的频道“Dev Newbs”。

你好，dev newbs，欢迎回到“JavaScript 基础”系列的另一篇文章。这次我们处理的是日期对象。

因为每一个方法都没有太多的内容，所以单独的文章会很短很无聊，我决定将这个系列分成 5 部分。每一部分都将包含逻辑上相关的方法，一起学习它们是有意义的，因为很有可能你也会一起使用它们。

我将介绍 8 对方法，它们为我们提供了日期的特定部分。其余 3 种方法与每对方法之间的差异相关。但稍后会详细介绍。

先说年份。第一对方法是 getFullYear()和 getUTCFullYear()。

我们今天要讲的 8 对中的每一对都有 UTC 方法和非 UTC 或本地时间方法，如果你愿意的话。这两种方法之间的唯一区别是，该方法的 UTC 版本基于协调通用时间返回日期的一部分。非 UTC 方法返回基于您当地时区的分数。

例如，我所在的时区在冬季比 UCT 早一个小时，在夏季早两个小时。区别是因为我们在夏天仍然使用夏令时。我的时区被称为中欧时间或简称 CET。

被决定用作协调世界时的时区具有 GMT 的本地名称，GMT 是格林威治标准时间的缩写。所以如果你听到 GMT，它的字面意思和 UCT 一样，反之亦然。

但是回到我们的第一对方法。这两种方法都返回所提供日期的年份分数。如果您所在的时区是 GMT，那么这两种方法都会得到相同的结果。然而，我，生活在不同的时区，和我在世界的大部分地区，有时会得到不同的结果。

一个很好的例子是新年的早晨。虽然我可能已经在 2022 年的新年了——尽管只差几分钟，但仍会有人在格林威治时间(UTC)时区等待午夜倒计时。迷惑？别担心，我会在示例中演示给你看。

```
let newYear22 = new Date(2022, 0, 1, 0, 59, 14, 587);
// Sat Jan 01 2022 00:59:14 GMT+0100 (stredoeurópsky štandardný čas)
```

让我们用一个新的 Date 对象来表示新年的早晨，午夜后 59 分钟。请记住，我提供的值是绑定到我的时区的—这意味着 CET，比 UCT 早一个小时(或者 GMT，如果你愿意的话)。

当我使用 getFullYear()方法获取日期的年分数时，我将得到 2022，因为根据所提供的输入，这是我所在时区的一年。

```
// getFullYear()
console.log(newYear22.getFullYear());                                        // 2022// getUTCFullYear()
console.log(newYear22.getUTCFullYear());                                    // 2021
```

但是，如果我使用该方法的 UTC 版本— getUTCFullYear()，我将获得日期中反映 UTC 时区的年份部分，作为其原始位置。记得吗？离 UTC 时区午夜还有一分钟。所以严格来说还是 2021 年。

对于获取月、日、日和小时的两个版本的方法，我们将得到相似的结果。原理是一样的，只是值会根据我们提取的日期部分而有所不同，所以我现在将一次性介绍所有其他方法。

```
// 0-based numbering of months
// 0 -> January, 1 -> February, ..., 11 -> December// getMonth()
console.log(newYear22.getMonth());                      // 0
// getUTCMonth()
console.log(newYear22.getUTCMonth());                   // 11// getDate()
console.log(newYear22.getDate());                       // 1
// getUTCDate()
console.log(newYear22.getUTCDate());                    // 31// 0 - based numbering of weekdays
// 0 - Sun, 1 - Mon, 2 - Tue, 3 - Wed, 4 - Thu, 5 - Fri, 6 - Sat// getDay()
console.log(newYear22.getDay());                        // 6
// getUTCDay()
console.log(newYear22.getUTCDay());                     // 5

// getHours()
console.log(newYear22.getHours());                      // 0
// getUTCHours()
console.log(newYear22.getUTCHours());                   // 23
```

方法 getMonth()和 getUTCMonth()从提供的日期中提取月份分数。该值不是月份的实际数字，而是其从零开始的索引，因此一月等于 0，二月等于 1，十二月等于 11。对于该方法的非 UTC 版本，我们得到索引 0，这意味着一月，对于该方法的 UTC 版本，得到索引值 11。

getDate()和 getUTCDate()为我们提供了指定一个月中某一天的日期分数。它始终是 1 到 31 之间的一个数字。在我们的例子中，对于该方法的非 UTC 版本，我们得到数字 1，对于 UTC 版本，我们得到数字 31。

getDay()和 getUTCDay()方法返回指定日期是星期几。结果总是一个介于 0 和 6 之间的数字，其中 0 代表星期日，1 代表星期一，依此类推，直到 6 代表星期六。在我们的示例中，对于非 UTC 版本，我们得到的值为 6，表示星期六；对于该方法的 UTC 版本，我们得到的值为 5，表示星期五。

最后一对受时区影响的方法是 getHours()和 getUTCHours()。它们为我们提供了所提供的日期对象的小时部分。非 UTC 版本返回 0，UTC 版本返回 23。幸运的是，这也是它的允许范围——0 到 23 之间的一个数字。

到目前为止，我们还没有介绍剩下的三对返回分钟、秒和毫秒的方法。但区别在于它们的 UTC 和非 UTC 版本实际上并没有提供不同的结果。因为时区的转换是以整小时为单位的，所以无论转换是什么，分钟、秒钟和毫秒都不会受到影响。我强烈地感觉到，这些方法的 UTC 和非 UTC 版本的实现更多地是因为一致性而不是必要性。但不管怎样，让我们把它们盖住。

```
// getMinutes()
console.log(newYear22.getMinutes());                   // 59
// getUTCMinutes()                                                                   
console.log(newYear22.getUTCMinutes());                // 59// getSeconds()
console.log(newYear22.getSeconds());                   // 14
// getUTCSeconds()
console.log(newYear22.getUTCSeconds());                // 14// getMilliseconds()
console.log(newYear22.getMilliseconds());              // 587
// getUTCMilliseconds()
console.log(newYear22.getUTCMilliseconds());           // 587
```

因此，为了保持一致，让我们继续规范。getMinutes()和 getUTCMInutes()返回给定 Date 对象的分钟分数。在我们的示例中，两种方法都返回相同的值 14。此方法可以返回的允许值是从数字 0 到数字 59。

相同范围的有效值适用于 getSeconds()和 getUTCSeconds()方法，它们返回给定 Date 对象的秒分数。在我们的示例中，这两种方法都返回值 14。

最后，方法 getMilliseconds()和 getUTCMilliseconds()返回给定日期对象的毫秒部分。允许的值是从数字 0 到数字 999。在我们的例子中，我们得到的值是 587。

到目前为止，我们已经介绍了 16 种方法，但是我们还将介绍另外三种方法。它们与我已经提到的有些不同，但它们确实以一种非常有意义的方式联系在一起。这就是为什么我把它们放在一起成为这个系列的一部分。让我们一起确保我这样做是正确的。

getTime()方法返回自 UNIX 纪元以来的毫秒数，这只是 1970 年 1 月 1 日午夜的一个花哨名称。我说的午夜是指一天的开始，不是结束。先说清楚。

这种方法在技术上使用 UTC 作为默认时区，但实际上它只是一个计数器，以毫秒为单位计算从 UNIX Epoch 到当前时刻的距离。所以时区其实没那么重要。因为一旦将 getTime()方法的值提供给 Date 构造函数，无论如何都会获得带有您的时区的 Date 对象。所以不要太担心，当你需要的时候就把它当作一个普通的数字。

```
// get number of milliseconds since 1st January 1970
console.log(new Date().getTime());                  // 1625587257784
console.log(new Date(new Date().getTime()));        // 1625587257784
```

另一个要介绍的方法是 valueOf()方法，这个方法实际上只是 getTime()方法的一个内部实现。它们都返回一个数字，表示自 UNIX 纪元以来经过的毫秒数。

```
console.log(new Date().getTime());                 // 1625587387249
console.log(new Date().valueOf());                 // 1625587387249console.log(typeof(new Date().getTime()));         // number
console.log(typeof(new Date().valueOf()));         // number
```

您可以使用其结果并将其反馈给日期对象构造函数，以获得新的日期对象实例。

最后一个要介绍的方法是 getTimezoneOffset()，它返回使用 UTC 时区表示的日期和使用本地时区表示的相同日期对象之间的差值(以分钟为单位)。

如果返回值为负，则意味着本地时区在 UTC 之前。如果返回值为正，则意味着本地时区比 UTC 晚那么多分钟。

```
// get timezone offset in minutes
console.log(newYear22.getTimezoneOffset());                // -60
console.log(new Date().getTimezoneOffset());               // -120
```

需要考虑的一件有趣的事情是，一个时区可以根据一年中的时间产生不同的结果。这是因为 UTC 不考虑夏令时，但当地时区会考虑。举个例子，在夏天，UCT 和我的当地时区的时差是 2 小时。我的时区比 UCT 早 120 分钟。但在冬天，因为夏令时的原因，它只提前 1 小时或 60 分钟。有趣的东西。幸运的是，Javascript 会自动处理这个问题——您只需要意识到这一点。如我所说，有趣的东西。

好了，至此，我们已经介绍了所有的 19 种方法，并且完成了日期对象系列的第一部分。我会给你们一两天的时间来整理，然后我会带着第 2 部分回来，这将是关于如何将东西放置到位的方法。

一如既往，感谢您的关注，我们将在下一集再见。

*更多内容看*[***plain English . io***](http://plainenglish.io/)