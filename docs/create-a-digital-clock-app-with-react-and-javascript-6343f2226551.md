# 用 React 和 JavaScript 创建一个数字时钟应用程序

> 原文：<https://javascript.plainenglish.io/create-a-digital-clock-app-with-react-and-javascript-6343f2226551?source=collection_archive---------3----------------------->

![](img/7097bf865f47ae119c83456b99acca51.png)

Photo by [RODOLFO BARRETO](https://unsplash.com/@rodolfobarreto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，允许我们创建前端应用程序。

在本文中，我们将了解如何使用 React 和 JavaScript 创建数字时钟应用程序。

# 创建项目

我们可以使用创建反应应用程序来创建反应项目。

要安装它，我们运行:

```
npx create-react-app digital-clock
```

与 NPM 一起创建我们的反应项目。

# 创建数字时钟应用程序

为了创建数字时钟应用程序，我们写道:

```
import React, { useEffect, useState } from "react";const date = new Date();
export default function App() {
  const [dateTime, setDateTime] = useState({
    hours: date.getHours(),
    minutes: date.getMinutes(),
    seconds: date.getSeconds()
  }); useEffect(() => {
    const timer = setInterval(() => {
      const date = new Date(); setDateTime({
        hours: date.getHours(),
        minutes: date.getMinutes(),
        seconds: date.getSeconds()
      });
    }, 1000);
    return () => clearInterval(timer);
  }, []); return (
    <div className="App">
      <div>
        {dateTime.hours}:{dateTime.minutes}:{dateTime.seconds}
      </div>
    </div>
  );
}
```

我们在`App`组件之外有`date`变量来设置初始日期。

在`App`内部，我们有`dateTime`状态，这是我们用`useState`钩子创建的。

它被设置为具有`hours`、`minutes`和`seconds`属性的对象。

我们分别用`getHours`、`getMinutes`和`getSeconds`得到小时、分钟和秒。

然后我们添加`useEffect`钩子来获取分配给`date`变量的最新日期和时间。

我们调用`setInterval`来设置第二个参数所指示的每秒钟的最新日期和时间。

然后我们用小时、分钟和秒的值调用`setDateTime`。

在`useEffect`回调的最后一行，当我们卸载组件时，我们返回一个调用`clearInterval`和`timer`的函数来清除定时器。

在 JSX 代码中，我们显示小时、分钟和秒。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个数字时钟应用程序。

*多内容于* [***浅显易懂***](http://plainenglish.io)