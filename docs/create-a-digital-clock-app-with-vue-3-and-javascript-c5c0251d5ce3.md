# 用 Vue 3 和 JavaScript 创建一个数字时钟应用程序

> 原文：<https://javascript.plainenglish.io/create-a-digital-clock-app-with-vue-3-and-javascript-c5c0251d5ce3?source=collection_archive---------7----------------------->

![](img/74a3e7b4f64e29603e80ed493c52c87f.png)

Photo by [RODOLFO BARRETO](https://unsplash.com/@rodolfobarreto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个数字时钟应用程序。

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

# 创建数字时钟应用程序

我们可以用下面的代码创建一个数字时钟应用程序:

```
<template>
  <div>{{ dateTime.hours }}:{{ dateTime.minutes }}:{{ dateTime.seconds }}</div>
</template><script>
const date = new Date();
export default {
  name: "App",
  data() {
    return {
      dateTime: {
        hours: date.getHours(),
        minutes: date.getMinutes(),
        seconds: date.getSeconds(),
      },
      timer: undefined,
    };
  },
  methods: {
    setDateTime() {
      const date = new Date();
      this.dateTime = {
        hours: date.getHours(),
        minutes: date.getMinutes(),
        seconds: date.getSeconds(),
      };
    },
  },
  beforeMount() {
    this.timer = setInterval(this.setDateTime, 1000);
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
};
</script>
```

在模板中，我们分别用`dateTime.hours`、`dateTime.minutes`和`dateTime.seconds`显示小时、分钟和秒。

在`data`方法中，我们用`hours`、`minutes`和`seconds`属性返回`dateTime`对象。

`new Date()`返回对象的当前日期和时间。

`getHours`返回日期的小时。

`getMinutes`返回日期的分钟数。

`getSeconds`返回日期的秒数。

在`setDateTime`方法中，我们用`new Date()`获取当前日期。

并且我们调用`getHours`、`getMinutes`、`getSeconds`来获取时间部分。

在`beforeMount`钩子中，我们用`this.setDateTime`方法调用`setInterval`来每秒运行一次。

第二个参数指定每 1000 毫秒运行一次，即 1 秒。

它返回我们分配给`timer`反应属性的定时器对象。

`beforeMount`在组件安装时运行。

`beforeUnmount`调用带有`timer`反应属性的`clearIntrval`方法，在组件卸载时清除定时器。

在模板中，我们显示时间，它每秒更新一次。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个数字钟。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)