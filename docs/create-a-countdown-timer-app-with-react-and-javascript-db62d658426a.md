# 用 React 和 JavaScript 创建一个倒计时应用程序

> 原文：<https://javascript.plainenglish.io/create-a-countdown-timer-app-with-react-and-javascript-db62d658426a?source=collection_archive---------7----------------------->

![](img/bdcdd307412d7938f3b65abfa231c5a9.png)

Photo by [Bundo Kim](https://unsplash.com/@bundo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个倒计时应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app countdown-timer
```

和 NPM 一起创建我们的 React 项目。

# 创建倒计时定时器应用程序

为了创建倒计时器应用程序，我们编写:

```
import React, { useEffect, useState } from "react";const futureDate = new Date(2050, 0, 1);
const getDateDiff = (date1, date2) => {
  const diff = new Date(date2.getTime() - date1.getTime());
  return {
    year: diff.getUTCFullYear() - 1970,
    month: diff.getUTCMonth(),
    day: diff.getUTCDate() - 1,
    hour: diff.getUTCHours(),
    minute: diff.getUTCMinutes(),
    second: diff.getUTCSeconds()
  };
};const formatDate = (date) => {
  let d = new Date(date),
    month = (d.getMonth() + 1).toString(),
    day = d.getDate().toString(),
    year = d.getFullYear().toString(); if (month.length < 2) month = "0" + month;
  if (day.length < 2) day = "0" + day; return [year, month, day].join("-");
};export default function App() {
  const [diff, setDiff] = useState({}); useEffect(() => {
    const timer = setInterval(() => {
      setDiff(getDateDiff(new Date(), futureDate));
    }, 1000);
    return () => clearInterval(timer);
  }, []); return (
    <div className="App">
      <p>
        {diff.year} years, {diff.month} months, {diff.day} days,
        {diff.hour} hours, {diff.minute} minute, {diff.second} seconds until{" "}
        {formatDate(futureDate)}
      </p>
    </div>
  );
}
```

`futureDate`变量是我们倒计时的日期。

`getDateDiff`是计算两个日期之差的函数。

我们通过减去 UNIX 时间戳`date2`和`date1`来计算。

`getTime`获取 UNIX 时间戳。

我们将该差异传递给`Date`构造函数，以获得日期差异对象。

然后我们用各种方法得到它的各个部分。

`getUTCFullYear`大年初一。我们必须在 1970 年减去它才能得到差额。

`getUTCMonth`获取月份。

`getUTCDate`获取日期。

得到小时数。

`getUTCMinutes`获取会议记录。

`getUTCSeconds`获取秒。

`formatDate`函数格式化`date`。

我们用它来格式化`futureDate`,以人类可读的格式显示它。

我们只是得到年、月、日，然后用一个破折号把它们连起来。

在`App`组件中，我们调用`setInterval`来调用`setDiff`来设置日期和时间的秒差。

当我们卸载组件时，我们返回一个调用`clearInterval`的函数。

在 JSX 代码中，我们显示了用`formatDate`格式化的`diff`部分和`futureDate`。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个倒计时器。

*更多内容请看*[***plain English . io***](http://plainenglish.io)