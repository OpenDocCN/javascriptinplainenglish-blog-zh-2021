# 用 Vue 3 和 JavaScript 创建一个倒计时应用

> 原文：<https://javascript.plainenglish.io/create-a-countdown-timer-app-with-vue-3-and-javascript-b064642d3a12?source=collection_archive---------7----------------------->

![](img/42cef5f39d6a53e3056de93e1a0ae962.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个倒计时应用程序。

# 创建项目

我们可以用 Vue CLI 创建 Vue 项目。

要安装它，我们运行:

```
npm install -g @vue/cli
```

与 NPM 或:

```
yarn global add @vue/cli
```

用纱线。

然后我们运行:

```
vue create digital-clock
```

并选择所有默认选项来创建项目。

# 创建倒计时定时器应用程序

为了创建倒计时定时器，我们编写:

```
<template>
  <p>
    {{ diff.year }} years, {{ diff.month }} months, {{ diff.day }} days,
    {{ diff.hour }} hours, {{ diff.minute }} minute, {{ diff.second }} seconds
    until
    {{ formatDate(futureDate) }}
  </p>
</template><script>
const futureDate = new Date(2050, 0, 1);
const getDateDiff = (date1, date2) => {
  const diff = new Date(date2.getTime() - date1.getTime());
  return {
    year: diff.getUTCFullYear() - 1970,
    month: diff.getUTCMonth(),
    day: diff.getUTCDate() - 1,
    hour: diff.getUTCHours(),
    minute: diff.getUTCMinutes(),
    second: diff.getUTCSeconds(),
  };
};
export default {
  name: "App",
  data() {
    return {
      futureDate,
      diff: {},
      timer: undefined,
    };
  },
  methods: {
    getDiff() {
      this.diff = getDateDiff(new Date(), futureDate);
    },
    formatDate(date) {
      let d = new Date(date),
        month = (d.getMonth() + 1).toString(),
        day = d.getDate().toString(),
        year = d.getFullYear().toString(); if (month.length < 2) month = "0" + month;
      if (day.length < 2) day = "0" + day; return [year, month, day].join("-");
    },
  },
  beforeMount() {
    this.timer = setInterval(this.getDiff, 1000);
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
};
</script>
```

在模板中，我们显示了日期和时间差异部分以及我们正在倒计时的日期。

然后在`script`标签中，我们有`futureDate`来倒计时。

`getDateDiff`让我们得到日期的差异。

我们通过减去 UNIX 时间戳版本的`date2`和`date1`得到日期差异。

我们用`getTime`得到时间戳。

然后我们用内置的`Date` instabnce 方法得到日期差的部分。

`getUTCFullYear`获取`diff`中的年数。

我们从 1970 年开始减去这个数字，得到`diff`年。

`getUTCMonth`返回`diff`的月数。

`getUTCDate`返回`diff`的天数。

`getUTCHours`返回`diff`的小时数。

`getUTCMinutes`返回`diff`的分钟数。

`getUTCSeconds`返回`diff`的秒数。

我们将`futureDate`传入用`data`返回的对象，这样我们就可以在模板中使用它。

`getDiff`调用`getDateDiff`获取当前日期时间与`futureDate`的差值。

`formatDate`让我们将`futureDate`格式化为 yyyy-mm-dd 格式。

我们通过用`getMonth`得到`month`来做到这一点。

我们使用`getDate`来获得天数。

而我们叶`getFullYear`拿到多少年了。

如果`month`和`day`少于两位数，那么我们在`month`和`day`字符串前加一个 0。

然后在`beforeMount`钩子中，我们用`getDiff`调用`setInterval`来计算当前日期时间和`futureDate`之间的日期差。

`setInterval`定期调用第一个参数中的回调。

1000 是我们在再次调用`getDiff`方法之前等待的时间间隔，以毫秒为单位。

我们将返回的定时器对象分配给`this.timer`。

然后我们在卸载组件时调用`beforeUnmount`中的`clearInterval`来清除计时器。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个倒计时器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)