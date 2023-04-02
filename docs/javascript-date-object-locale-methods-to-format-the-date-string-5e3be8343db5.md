# JavaScript Date 对象:格式化日期字符串的区域设置方法

> 原文：<https://javascript.plainenglish.io/javascript-date-object-locale-methods-to-format-the-date-string-5e3be8343db5?source=collection_archive---------2----------------------->

## JavaScript 中日期对象的基础知识第 5 部分:如何使用地区格式方法

![](img/3202364eef51d5d80130c0197bc26535.png)

这篇文章是我的免费 YouTube 系列关于网络开发基础知识的抄本。如果你更喜欢看而不是读，请随时访问我的频道“Dev Newbs”。

开发者朋友们好！这将是我们一起揭开内置 Javascript 对象日期的深层秘密的最后一次旅行。我将解释最后 3 种方法，它们允许我们根据客户端浏览器的地区进一步指定日期输出的格式。我们开始吧。

第一个方法的名称是 toLocaleString()，它返回一个带有日期的语言敏感表示的字符串。

我们已经接触到相当新的参数“locale”和“options ”,它们使得为了给定语言的格式约定而指定语言成为可能。

该方法有两个输入参数。第一个是名为“locale”的字符串，第二个是名为“options”的对象，用于保存个人设置。

该方法的返回值当然是根据所提供的特定于语言的约定格式化的日期字符串。

```
// default format of toString() method
console.log(new Date());
// Sat Jul 17 2021 22:10:00 GMT+0200 (stredoeurópsky letný čas)// default locale of my browser, which is Slovak
console.log(new Date().toLocaleString());
// 17\. 7\. 2021, 22:10:00// British English uses day-month-year order and 24-hour time without AM/PM
console.log(new Date().toLocaleString('en-GB', { timeZone: 'UTC' }));
// 17/07/2021, 20:10:00// US English uses month-day-year order and 12-hour time with AM/PM
console.log(new Date().toLocaleString('en-US', { timeZone: 'UTC' }));
// 7/17/2021, 8:10:00 PM
```

如果未指定任何区域设置，则使用默认区域设置。对我来说，它是“sk-SK”，这是斯洛伐克语。它有自己的特点，比如日期对象的日期部分的分隔符是点，后跟空格和 24 小时时间格式。

我想展示的另外两个地方是美国和英国。它们相似，但同时又不同。美国遵循月-日-年的惯例，而世界上大多数国家遵循日-月-年的顺序。另外，美国似乎喜欢用零填充他们的数字，他们更喜欢 12 小时 AM/PM 周期，而不是世界其他地区的 24 小时周期。

下面的代码块展示了多个不同地区的默认格式。

```
// US English uses month-day-year order and 12-hour time with AM/PM
console.log(new Date().toLocaleString('en-US'));
// 7/17/2021, 10:10:00 PM// British English uses day-month-year order and 24-hour time without AM/PM
console.log(new Date().toLocaleString('en-GB'));
// 17/07/2021, 22:10:00// Germans use day.month.year order and 24-hour time without AM/PM
console.log(new Date().toLocaleString('de-DE'));
// 17.7.2021, 22:10:00// Korean uses year-month-day order and 12-hour time with AM/PM
console.log(new Date().toLocaleString('ko-KR'));
// 2021\. 7\. 17\. 오후 10:10:00// Arabic in most Arabic speaking countries uses real Arabic digits
console.log(new Date().toLocaleString('ar-EG'));
// ١٧‏/٧‏/٢٠٢١, ١٠:١٠:٠٠ م
```

我选择了 5 个不同的地方——美国，因为它明显不同于其他大多数地方，英国、德国、韩国和阿拉伯。正如你所看到的，它们都有自己的特点。区域设置的完整列表非常大，包含几十个区域设置，几乎涵盖了世界上的所有语言。

除了使用区域设置之外，另一种可能性是指定甚至覆盖使用区域设置定义的格式。选项对象有许多不同的属性，允许我们修改结果格式。我选择了其中的一些，并在下一个代码示例中展示了它们。

```
let options = 
{ 
    weekday: 'long', 
    year: 'numeric', 
    month: 'long', 
    day: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    timeZone: 'UTC',
    timeZoneName: 'long'
};console.log(new Date().toLocaleString('en-US', options));
// Saturday, July 17, 2021, 08:10 PM Coordinated Universal Timeconsole.log(new Date().toLocaleString('en-GB', options));
// Saturday, 17 July 2021, 20:10 Coordinated Universal Timeconsole.log(new Date().toLocaleString('de-DE', options));
// Samstag, 17\. Juli 2021, 20:10 Koordinierte Weltzeitconsole.log(new Date().toLocaleString('sk-SK', options));
// sobota 17\. júla 2021, 20:10 koordinovaný svetový čas
```

其中一些选项指定是将月份输出为数字还是字符串。其他人可以指定时区及其名称或小时周期。有很多选项和组合，但是从我的经验来看，它们在不同的浏览器上仍然没有得到一致的实现。因此，您必须尝试查看特定的属性，并决定是否值得使用该方法的选项，或者自己解析日期并进行必要的更改。

下一个方法名为 toLocaleDateString()，它返回一个字符串，该字符串以语言敏感的方式表示该日期的日期部分。它可以像前面的方法一样利用“区域设置”和“选项”。

```
let optionsDate = 
{ 
    weekday: 'long', 
    year: 'numeric', 
    month: 'long', 
    day: 'numeric'
};console.log(new Date().toLocaleDateString());
// 17\. 7\. 2021console.log(new Date().toLocaleDateString('en-US'));
// 7/17/2021console.log(new Date().toLocaleDateString('en-GB'));
// 17/07/2021console.log(new Date().toLocaleDateString(undefined, optionsDate));
// sobota 17\. júla 2021console.log(new Date().toLocaleDateString('en-US', optionsDate));
// Saturday, July 17, 2021console.log(new Date().toLocaleDateString('en-GB', optionsDate));
// Saturday, 17 July 2021
```

在这种情况下，您可以获得与 toLocaleString()方法完全相同的属性和可能性。然而，只有使用以某种方式修改所提供的日期对象的日期部分的设置部分才有意义。

最后一个方法是 toLocaleTimeString()，它返回一个字符串，其中包含日期时间部分的语言敏感表示。与前两种方法完全一样，这种方法也有可用于进一步修改结果字符串的语言环境和选项。

```
let myTime = new Date(2021, 6, 8, 23, 15, 47);console.log(myTime.toLocaleTimeString());
// 23:15:47console.log(myTime.toLocaleTimeString('en-US'));
// 11:15:47 PMconsole.log(myTime.toLocaleTimeString('en-GB'));
// 23:15:47console.log(myTime.toLocaleTimeString('sk-SK', { timeZone: 'CET', timeZoneName: 'long' }));
// 23:15:47 GMT+02:00console.log(myTime.toLocaleTimeString('en-US', { hour12: false, timeZone: 'GMT' }));
// 21:15:47console.log(myTime.toLocaleTimeString('en-GB', { hour: '2-digit', minute: '2-digit' }));
// 23:15
```

我们可以指定输出的特定格式和属性，如 12 或 24 小时周期，用于显示时间部分。我们还可以使用 options 属性完全覆盖 locale 定义的格式。例如，我们可以强制美国地区使用 24 小时周期来显示时间。当然，可能性还不止于此。天空是极限，但是要小心，因为就像前面的方法一样，这个方法也允许您添加日期对象中与时间部分不完全匹配的部分。

就这样，我们结束了。这些都是一个接一个讨论的日期对象方法。现在，您离成为真正的 Javascript 专家又近了一步。或者，你知道，有点体面的程序员。绝对是那两个中的一个。

但是玩笑归玩笑，如果你能坚持到最后，谢谢你。我希望你学到了新东西。我希望能在下一期 Javascript 基础系列文章中见到你。这次也许是关于数字？谁知道呢。

*更多内容看*[***plain English . io***](http://plainenglish.io/)