# 用 Vue 3 和 JavaScript 创建一个硬币翻转应用程序

> 原文：<https://javascript.plainenglish.io/create-a-coin-flip-app-with-vue-3-and-javascript-9d896828820?source=collection_archive---------9----------------------->

![](img/2e0086943e84404a18ac37fc7fe556cb.png)

Photo by [Jonathan Brinkhorst](https://unsplash.com/@jbrinkhorst?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个掷硬币应用程序。

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
vue create coin-flip
```

并选择所有默认选项来创建项目。

# 创建一个掷硬币应用程序

为了创建抛硬币应用程序，我们编写:

```
<template>
  <div>
    <h1>select a face</h1>
    <button @click="selectedFace = 'heads'">heads</button>
    <button @click="selectedFace = 'tails'">tails</button>
  </div>
  <p>you selected: {{ selectedFace }}</p>
  <p>computer selected: {{ computerSelectedFace }}</p>
  <button @click="flip">flip coin</button>
  <p v-if="isWin">you win</p>
  <p v-else>you lost</p>
</template><script>
const faces = ["heads", "tails"];
export default {
  name: "App",
  data() {
    return {
      selectedFace: "",
      coinFlipResult: "",
    };
  },
  computed: {
    computerSelectedFace() {
      const { selectedFace } = this;
      const face = faces.find((f) => f !== selectedFace);
      return face;
    },
    isWin() {
      const { selectedFace, coinFlipResult } = this;
      return coinFlipResult === selectedFace;
    },
  },
  methods: {
    flip() {
      let index;
      if (Math.random() < 0.5) {
        index = 0;
      } else {
        index = 1;
      }
      this.coinFlipResult = faces[index];
    },
  },
};
</script>
```

在模板中，我们有一个头像按钮，让玩家选择头像。

我们还有另一个按钮让玩家选择尾巴。

一旦点击按钮，就会设置`selectedFace`值。

然后我们有 p 元素来显示玩家和电脑选择的硬币面。

接下来，我们添加一个抛硬币按钮，让我们抛硬币。

然后我们显示玩家在 p 元素中是赢还是输。

接下来，在`script`标签中，我们有了带有`'heads'`和`'tails'`字符串的`faces`数组。

`data`返回一个对象的反应属性及其初始值。

接下来，我们有计算的属性。

我们有`computedSelectedFace`返回计算机选择的硬币正面，也就是玩家没有选择的那张。

`isWin`检查`coinFlipResult`是否与`seletedFace`相同，表示玩家获胜。

最后，我们用`flip`方法来设置`coinFlipResult`来设置掷硬币的结果。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个抛硬币应用程序。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)