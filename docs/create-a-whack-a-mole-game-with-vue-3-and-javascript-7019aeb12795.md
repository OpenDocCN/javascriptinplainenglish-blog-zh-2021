# 用 Vue 3 和 JavaScript 创建一个打地鼠游戏

> 原文：<https://javascript.plainenglish.io/create-a-whack-a-mole-game-with-vue-3-and-javascript-7019aeb12795?source=collection_archive---------13----------------------->

![](img/87afe47a8dcde471db410320dd13b17c.png)

Photo by [Ryan Stone](https://unsplash.com/@rstone_design?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个打地鼠游戏。

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
vue create whack-a-mole
```

并选择所有默认选项来创建项目。

# 创建一个打地鼠游戏

为了创建打地鼠游戏，我们编写:

```
<template>
  <button @click="startGame">start game</button>
  <button @click="endGame">end game</button>
  <p>score: {{ score }}</p>
  <div>
    <div v-for="n of 6" :key="n" class="container">
      <img
        v-if="index === n"
        src="https://grid.gograph.com/happy-mole-cartoon-vector-art_gg68718247.jpg"
        @click="onClick(n)"
      />
      <div v-else class="hole"></div>
    </div>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      index: 0,
      timer: undefined,
      score: 0,
    };
  },
  methods: {
    generateIndex() {
      this.index = Math.floor(Math.random() * 6);
    },
    startGame() {
      this.timer = setInterval(this.generateIndex, 2000);
    },
    endGame() {
      clearInterval(this.timer);
      this.score = 0;
      this.index = 0;
    },
    onClick(n) {
      if (this.index === n) {
        this.score++;
      }
    },
  },
  beforeUnmount() {
    clearInterval(this.timer);
  },
};
</script><style scoped>
.hole {
  width: 50px;
  height: 50px;
  border: 1px solid black;
  border-radius: 50%;
}.container {
  display: inline-block;
}img {
  width: 50px;
  height: 50px;
}
</style>
```

我们有开始游戏和结束游戏按钮，让我们开始和结束游戏。

当我们点击开始游戏时，就会调用`startGame`来开始游戏。

而当我们点击开始游戏时，就会调用`endGame`来结束游戏。

然后我们向 p 元素中的玩家展示`score`。

接下来，我们渲染 div 来显示鼹鼠。

`index`是痣所在的索引。

因此，如果`index`等于`n`，那么我们就显示出鼹鼠。

否则，我们显示一个圆圈。

在图中，我们有一个点击事件监听器，它检查我们是否点击了鼹鼠。

在组件对象中，我们使用了`data`方法来返回反应属性的初始值。

`generateIndex`产生随机的`index`值。

`startGame`通过调用`setInterval`启动计时器开始游戏。

第二个参数是等待第一个参数中的回调再次运行的时间间隔。

时间间隔以毫秒为单位。

`endGame`调用`clearInterval`到定时器结束。

我们还将`score`和`index`设置回 0 来重置游戏。

`onClick`方法检查`n`是否与`this.index`相同，如果相同，则增加`score`。

现在，当我们点击开始游戏，我们应该看到鼹鼠弹出，我们可以点击它来增加分数。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个打地鼠游戏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)