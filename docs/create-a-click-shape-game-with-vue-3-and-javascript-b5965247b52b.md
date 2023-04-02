# 用 Vue 3 和 JavaScript 创建一个点击形状游戏

> 原文：<https://javascript.plainenglish.io/create-a-click-shape-game-with-vue-3-and-javascript-b5965247b52b?source=collection_archive---------16----------------------->

![](img/e5ff89e1aa207f6abb58a0be9891fb68.png)

Photo by [Ostap Senyuk](https://unsplash.com/@kintecus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个点击形状的游戏。

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
vue create click-shape-game
```

并选择所有默认选项来创建项目。

# 创建点击形状游戏

这个游戏让我们通过点击随机显示的图形来得分。

为了创建点击形状游戏，我们编写:

```
<template>
  <button @click="start">start game</button>
  <button @click="end">end game</button>
  <p>score: {{ score }}</p>
  <div
    class="circle"
    v-if="circleX && circleY"
    :style="{ position: 'absolute', top: `${circleY}px`, left: `${circleX}px` }"
    @click="onClick"
  >
    &nbsp;
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      score: 0,
      circleX: undefined,
      circleY: undefined,
      timer: undefined,
    };
  },
  methods: {
    onClick() {
      this.score++;
    },
    start() {
      this.timer = setInterval(() => {
        this.circleX = Math.floor(Math.random() * window.innerWidth);
        this.circleY = Math.floor(
          Math.random() * (window.innerHeight - 50) + 50
        );
      }, 2000);
    },
    end() {
      clearInterval(this.timer);
      this.score = 0;
      this.circleX = undefined;
      this.circleY = undefined;
    },
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
};
</script><style scoped>
.circle {
  border: 1px solid black;
  width: 50px;
  height: 50px;
  border-radius: 50%;
}
</style>
```

在模板中，我们有一个带有开始游戏和结束游戏按钮的按钮来开始和结束游戏计时器。

在那下面，我们有`score`显示。

然后我们有玩家点击得分的 div。

我们用`top`和`left`值将`style`道具设置为样式。我们需要在末尾用`px`来指明位置。

在脚本标签中，我们使用了`data`方法来返回带有初始值的反应属性。

`circleX`和`circleY`分别有左值和上值。

`timer`有定时器。

`onClick`是 div 的点击处理程序。

在`start`方法中，我们用回调函数调用`setInterval`来设置`circleX`和`circleY`的值。

我们将它们设置为屏幕宽度和高度范围内的随机值。

在`end`方法中，我们调用`clearInterval`来停止计时器。

我们将其他反应属性重置为初始值。

在`beforeUnmount`钩子中，我们调用`clearInterval`来移除计时器。

然后在`style`标签中，我们用样式将带有类`circle`的 div 做成一个圆。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个点击形状的游戏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)