# 如何用 Moment.js 将日期格式化为 ISO-8601 字符串？

> 原文：<https://javascript.plainenglish.io/how-to-format-a-date-as-an-iso-8601-string-with-moment-js-7c54bcb8695f?source=collection_archive---------9----------------------->

![](img/54a46cae121864dd03c7296dcaab9ede.png)

Photo by [Erik Brolin](https://unsplash.com/@erik_brolin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望将日期格式化为 IS0–8601 标准格式。

在本文中，我们将了解如何使用 moment.js 将日期格式化为 ISO-8601 字符串。

# `The toISOString Method`

Moment.js 附带了`toISOString`方法，允许我们将日期格式化为 ISO-8601 格式。

例如，我们可以写:

```
console.log(moment(new Date(2021, 1, 1)).toISOString())
```

然后我们得到:

```
'2021-02-01T08:00:00.000Z'
```

结果。

# `The format Method`

`format`方法还允许我们将日期格式化为 ISO-8601 日期字符串。

例如，我们可以写:

```
import moment from "moment";
console.log(moment(new Date(2021, 1, 1)).format());
```

然后我们得到和以前一样的结果。

# 时区支持

我们可以使用 Moment Timezone 库来添加对时区的支持。

然后，我们可以在应用程序中设置时区，然后使用`toISOString`方法将 moment 对象转换为 ISO-8601 字符串。

例如，我们可以写:

```
const moment = require("moment-timezone");
moment().tz("America/Los Angeles");
console.log(moment(new Date(2021, 1, 1)).toISOString(true));
```

然后控制台日志记录:

```
'2021-02-01T00:00:00.000-08:00'
```

结果。

# 解析 ISO-8601 日期

我们可以用 moment.js 解析 ISO-8601 日期

例如，我们可以写:

```
import moment from "moment";
console.log(moment("2021-01-01", moment.ISO_8601));
```

我们以 ISO-8601 格式传入一个日期字符串。

我们传入常数`moment.ISO_8601`让 moment 知道第一个参数中的日期字符串是 ISO-8601 日期。

# 结论

我们可以在 JavaScript 代码中用 moment.js 创建和解析 ISO-8601 日期字符串。

*更多内容请看*[***plain English . io***](http://plainenglish.io)