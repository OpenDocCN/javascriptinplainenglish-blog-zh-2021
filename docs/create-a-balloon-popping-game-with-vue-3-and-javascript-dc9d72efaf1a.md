# 用 Vue 3 和 JavaScript 创建一个气球弹出游戏

> 原文：<https://javascript.plainenglish.io/create-a-balloon-popping-game-with-vue-3-and-javascript-dc9d72efaf1a?source=collection_archive---------13----------------------->

![](img/d0fb8b2fa297ab51e7b58d96d6a115ba.png)

Photo by [Aaron Burden](https://unsplash.com/@aaronburden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，它允许我们创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个气球弹出游戏。

# 创建项目

我们可以使用 Vue CLI 创建 Vue 项目。

要安装它，我们运行:

```
npm install -g @vue/cli
```

与 NPM 或:

```
yarn global add @vue/cli
```

纱线。

然后我们运行:

```
vue create balloon-poppinng-game
```

并选择所有默认选项来创建项目。

# 创建气球弹出游戏

为了创建气球弹出应用程序，我们写道:

```
<template>
  <div v-for="(b, index) of balloons" :key="b.id" class="balloon-container">
    <div
      v-if="!b.popped"
      class="balloon"
      :style="{ 'background-color': b.color }"
      @mouseover="onPop(index)"
    ></div>
    <div v-else>popped</div>
  </div>
</template><script>
const colors = ["red", "green", "blue"];const generateColor = () => {
  const index = Math.floor(Math.random() * colors.length);
  return colors[index];
};
export default {
  name: "App",
  data() {
    return {
      balloons: Array(25)
        .fill()
        .map((_, i) => ({ id: i, popped: false, color: generateColor() })),
    };
  },
  methods: {
    onPop(index) {
      this.balloons[index] = {
        ...this.balloons[index],
        popped: true,
      };
    },
  },
};
</script><style scoped>
.balloon-container {
  display: inline-block;
}.balloon {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 1px solid black;
}
</style>
```

在模板中，我们使用`v-for`渲染气球的草皮。

`b`是气球对象，`index`是气球入口的索引。

`key`具有唯一的气球 ID，便于 Vue 跟踪气球。

在里面，我们有一个 div 来渲染气球，如果`b.popped`是`false`，这表明它没有被弹出。

否则，我们用`v-else`显示“弹出”。

在`script`对象中，我们使用`genberateColor`函数为气球生成随机颜色。

我们将`style`道具设置为`background-color`气球的`color`属性。

此外，我们还有`@mouseover`指令来运行`onPop`方法来弹出气球。

在`data`方法中，我们返回带有气球条目的`ballons`数组。

在`onPop`方法中，我们只需要将`balloon` 条目的`popped`属性设置为`true`。

在`style`标签中，我们将气球做成圆形并并排显示。

为了让它并排显示，我们将`balloon-container`类设置为`display: inline-block`。

在`balloon`类中，我们将气球的宽度和高度设置为相同的尺寸。

`border-radius`设定为 50%使其成为圆形。

我们添加了一个带有`border`属性的边框。

现在，当我们用鼠标悬停在气球上时，我们看到弹出的文本显示在气球的位置。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个气球弹出游戏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)