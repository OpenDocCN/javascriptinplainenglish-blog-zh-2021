# 两分钟后的卢森 JS

> 原文：<https://javascript.plainenglish.io/luxonjs-in-two-minutes-70c1d3ba06e0?source=collection_archive---------15----------------------->

## *现代日期和时间操作库*

![](img/0543ab13fa6a0bd6f4d453ade97db353.png)

Photo by [Marija Zaric](https://unsplash.com/@simplicity?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](/s/photos/clock?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

*你可以在我新的 YouTube 频道上* [*以视频形式*](https://www.youtube.com/watch?v=GYntzCO4dBQ) *观看这篇文章。我还在学习视频编辑的技巧，请告诉我你的想法。*

[luxojs](https://moment.github.io/luxon/)是一个强大而现代的日期和时间操作库，与[矩](https://momentjs.com/)和 [DayJS](https://day.js.org/) 同列。

让 Luxon 与其他库不同的一点是，它使用了更现代的`[Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)`对象，而不是通常的`Date`对象。

`Intl`对象是 ECMAScript 国际化 API 的命名空间，该 API 根据 Mozilla 提供对语言敏感的字符串比较、数字格式和日期时间格式。

在现有的或新的项目中使用 Luxon 非常容易，学习曲线也很小，尤其是如果您以前使用过矩。

Luxon 可以使用 NPM 安装，也可以作为节点模块、AMD 模块或 ES6 模块导入。

您可以通过调用带有函数的日期时间对象来创建一个新的日期时间对象，如`now()`或`local()`以及一些需要的参数。

有了这个对象，您可以将日期加、减或解析成您的数据库或前端可能需要的任何日期格式。

两分钟后就是卢森了。我希望这篇小文章对一些正在寻找一个好的日期操作库的程序员有用。

谢谢你的阅读，祝你度过美好的一天。