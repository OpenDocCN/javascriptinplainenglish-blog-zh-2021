# 用 Vue 3 和 JavaScript 创建一个番茄定时器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-pomodoro-timer-app-with-vue-3-and-javascript-c4458a614400?source=collection_archive---------15----------------------->

![](img/8fc99327361a54377b0d3b76c3541b05.png)

Photo by [Lukas Blazek](https://unsplash.com/@goumbik?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个密码生成器应用程序。

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
vue create pomodoro-timer
```

并选择所有默认选项来创建项目。

# 创建番茄定时器

为了创建番茄定时器应用程序，我们编写:

```
<template>
  <h1>Pomodoro Timer</h1>
  <button @click="start">start</button>
  <div>{{ secondsLeft }} seconds left</div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      secondsLeft: 25 * 60,
      timer: undefined,
    };
  },
  methods: {
    start() {
      this.timer = setInterval(() => {
        this.secondsLeft--;
        if (this.secondsLeft === 0) {
          clearInterval(this.timer);
        }
      }, 1000);
    },
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
};
</script>
```

在模板中，我们有一个启动按钮，当我们点击它的时候就可以启动计时器。

div 显示时间结束前剩余的秒数。

在`data`方法中，我们用`secondsLeft`和`timer`反应属性返回反应属性。

`start`方法调用`setInterval`来启动计时器。

我们递减`secondsLeft`反应属性的值，直到`secondsLeft`为 0。

如果是 0，那么我们调用`clearInterval`来清除定时器。

1000 是回调再次运行之前等待的时间间隔。

在`beforeUnmount`钩子中，当我们卸载组件时，我们调用`clearInterval`来清除计时器。

当我们单击“开始”时，我们应该会看到页面上的倒计时。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个番茄定时器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)