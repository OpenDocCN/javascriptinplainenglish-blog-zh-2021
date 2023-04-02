# 用 Vue 3 和 JavaScript 创建一个石头剪刀布游戏

> 原文：<https://javascript.plainenglish.io/create-a-rock-paper-scissors-game-with-vue-3-and-javascript-d389b9122cf0?source=collection_archive---------12----------------------->

![](img/48dd4a6b6b53216c71952d82f7455a65.png)

Photo by [Rod Sot](https://unsplash.com/@rodsot?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个石头剪刀布游戏。

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
vue create rock-paper-scissors
```

并选择所有默认选项来创建项目。

# 创建一个石头、布、剪刀游戏

为了创建石头、剪子、布游戏，我们编写:

```
<template>
  <div>
    <button @click="selected = 'rock'">rock</button>
    <button @click="selected = 'paper'">paper</button>
    <button @click="selected = 'scissors'">scissors</button>
  </div>
  <button @click="play">play</button>
  <p>your choice: {{ selected }}</p>
  <p>computer's choice: {{ computedSeletced }}</p>
  <div>{{ result }}</div>
</template><script>
const choices = ["rock", "paper", "scissors"];
export default {
  name: "App",
  data() {
    return {
      selected: "",
      computedSeletced: "",
    };
  },
  computed: {
    result() {
      const { computedSeletced, selected } = this;
      if (computedSeletced === selected) {
        return `it's a tie`;
      } else {
        if (
          (computedSeletced === "rock" && selected === "scissors") ||
          (computedSeletced === "paper" && selected === "rock") ||
          (computedSeletced === "scissors" && selected === "paper")
        ) {
          return "computer won";
        }
        return "player won";
      }
    },
  },
  methods: {
    play() {
      if (!this.selected) {
        return;
      }
      const computerChoiceIndex = Math.floor(Math.random() * choices.length);
      this.computedSeletced = choices[computerChoiceIndex];
    },
  },
};
</script>
```

在模板中，我们有几个按钮。

顶部的 3 个按钮让玩家在石头、布和剪刀之间进行选择。

下面，我们有一个播放按钮，当我们点击按钮时，它会调用`play`。

`play`方法通过将`computedSelected`反应属性设置为随机选项，让计算机做出选择。

接下来，我们用 2 p 元素来展示玩家和电脑的选择。

然后我们有一个 div 来显示结果。

在`script`标记中，我们有一个带有选项的`choices`数组。

`data`返回反应属性及其初始值的数组。

然后我们添加`result` computed 属性来返回游戏的结果。

我们得到了`computedSelected`和`selected`反应属性，它们分别有电脑和玩家的选择。

如果它们是一样的，那就是平局。

然后在`else`块，我们按照游戏规则检查。

石头打败剪刀，布打败石头，剪刀打败布。

所以我们检查所有这些条件来返回谁赢了。

最后，我们有前面提到的`play`方法，让计算机进行选择。

在让电脑选择一个选项之前，我们检查玩家是否选择了一个选项。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个石头、剪子、布的游戏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)